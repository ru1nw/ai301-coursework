# issue plan

## diagnosis

This is a test-coverage gap, not a behavioral bug: the four safety
middleware components (prompt defense, content filter, bias detector,
PII scrubber) are each unit-tested individually, but no test exercises
them chained together as a single request would pass through them.

Confirmed by repro: running the three components with existing test
files returned "74 passed, 15 xfailed in 0.32s", with the xfails
confirmed as belonging to unrelated open issues (#58, #53, #24).
`tests/integration/test_safety_middleware.py` — the file the issue
names — does not exist. Each layer working in isolation says nothing
about whether the chain behaves correctly in sequence (e.g. whether a
later layer still runs correctly on output already transformed by an
earlier layer).

Additionally, the repro found that `ContentFilter` has no unit test
file at all, despite the issue description implying its tests already
exist alongside the other three.

## scope

In scope: creating `tests/integration/test_safety_middleware.py`,
containing one integration test that runs a request through all four
layers in order, plus fixtures covering a clean pass-through case and
a failure case for each individual layer (4 fail cases + 1 pass case).

Not in scope:
- Writing unit tests for `ContentFilter` in isolation. No such test
  file currently exists, which is a related but separate gap from
  what this issue asks for — recommend opening a new issue for it
  rather than folding it in here, consistent with what the repro
  comment already flagged.
- Any change to the implementation of the four middleware components.
  This is a test-only addition; nothing in `diagnosis` points to
  behavior that needs fixing, only to missing coverage.

## modifying files

- `tests/integration/test_safety_middleware.py` (new file)

No existing files are modified. If fixture setup needs shared
configuration (e.g. a `conftest.py` addition under `tests/integration/`),
that will be noted here and under Deviations if it comes up during the
build — not assumed now.

## approach

1. Read the existing unit tests (`test_prompt_defense.py`,
   `test_bias_detector.py`, `test_pii_scrubber.py`) to learn each
   component's call signature and expected input/output shape, since
   the integration test needs to invoke all three the same way.
2. Identify the actual orchestration point that chains the four layers
   in production code (not yet confirmed — see Risks). The integration
   test should exercise that real entry point, not reimplement the
   chaining logic itself.
3. Write fixtures: one input that should pass cleanly through all four
   layers, and one input per layer designed to fail specifically at
   that layer (4 fail fixtures total).
4. Write the integration test asserting the pass-through case succeeds
   end-to-end, and each fail fixture is caught at the expected layer.
5. For the `ContentFilter` fail case specifically, construct the input
   from the issue's own description of what the filter should reject,
   since no existing unit test gives a reference example — flagged as
   an assumption under Risks.

## test plan

Re-run the original repro command plus the new file:

```
pytest ./tests/unit/test_prompt_defense.py ./tests/unit/test_bias_detector.py ./tests/unit/test_pii_scrubber.py ./tests/integration/test_safety_middleware.py
```

Before (from repro): `74 passed, 15 xfailed`, and `test_safety_middleware.py`
does not exist — pytest would report it as not found if targeted directly.

Expected after: the same `74 passed, 15 xfailed` from the three existing files,
unchanged, plus 5 new passing tests in `test_safety_middleware.py` (1 full-chain
pass case + 4 per-layer fail cases).

## risks and unknowns

- The real chaining/orchestration entry point for the four middleware
  layers hasn't been identified yet — approach step 2 depends on
  finding it in the actual codebase rather than assuming a structure.
  If no single orchestrator exists and layers are called ad hoc per
  request path, the integration test's shape may need to change.
- No existing unit test for `ContentFilter` means its fail-case fixture
  in step 5 is built from the issue description alone, not from a
  verified reference — it may need adjusting once the component's real
  interface is inspected.
- Unknown whether the pipeline short-circuits on the first failing
  layer or runs all four regardless. This affects whether each
  per-layer fail fixture can be asserted independently or needs to
  account for earlier-layer side effects.

## deviations

**Assumed chain orchestrator (does not exist in the repo).** Approach step 2
could not be satisfied as written: a search of `api/`, `agent/`, `rag/`,
`core/`, `ingestion/` and `safety/` found no production code that calls the
four components together (`safety/__init__.py` is empty, `api/main.py`
registers no safety middleware, and `_run_safety_checks` in
`core/services/review_service.py` is a placeholder that calls none of them).

Per the scope of this issue (test-only, no changes to implementation), no
orchestrator or helper was added. Instead,
`tests/integration/test_safety_middleware.py` is written as if the
orchestrator already exists, with this **assumed** interface:

- Import path: `from safety.chain import SafetyChain`
- `SafetyChain().run(text)` returns a result with:
  - `passed: bool`: False if any layer rejected the input
  - `blocked_by: str | None`: name of the rejecting layer
  - `text: str`: final text after the layers (e.g. PII redacted)
  - `layers_run: list[str]`: layers executed, in order
- Layer names, in order: `prompt_defense`, `content_filter`,
  `bias_detector`, `pii_scrubber`.
- Behavior: the chain short-circuits on the first rejection. Prompt
  defense, content filter and bias detector reject; the PII scrubber
  redacts and does not reject.

Consequences:
- The new tests will fail with `ModuleNotFoundError` until a real
  orchestrator matching this interface exists, so the "5 new passing tests"
  expectation in the test plan is not met by this change alone.
- The names, result shape and short-circuit behavior are guesses and must be
  reconciled with the real implementation (or the orchestrator written to
  match). This resolves the third risk above by assumption, not by
  verification.
- The `ContentFilter` fail fixture is built from the component's
  `HARMFUL_PATTERNS`, since there is no unit test to reference.

**Strict xfail markers and fixture-scoped import.** Because `safety.chain`
does not exist, all 5 tests in `tests/integration/test_safety_middleware.py`
are marked `@pytest.mark.xfail(strict=True, ...)`, following the convention in
`tests/unit/test_bias_detector.py` and `tests/unit/test_pii_scrubber.py`.
For these markers to take effect, `SafetyChain` is imported inside the `chain`
fixture rather than at module level: a module-level import of a missing module
raises a collection error, which xfail cannot catch. Once the orchestrator
exists, the tests will XPASS and fail under `strict=True`, so the markers
should be removed and the import can move back to module level. Until then the
test plan's expected result is `5 xfailed` rather than 5 passing tests.
