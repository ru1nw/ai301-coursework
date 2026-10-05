# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

`ru1nw`

**Plan comment**

[https://github.com/codepath/pathreview-ai301-fa26-s1/issues/31#issuecomment-5998384271](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/31#issuecomment-5998384271)

> Reproduced the gap: running the existing unit tests for prompt defense, bias detector, and PII scrubber gives `74 passed, 15 xfailed` (xfails confirmed unrelated, tied to issues 58/53/24), and `tests/integration/test_safety_middleware.py` doesn't exist. Each layer is tested alone, but nothing exercises the full chain.
> 
> Plan: add that integration test file with one full-pass-through case and one fail fixture per layer (4 fail cases + 1 pass case). Test-only change, no modifications to the middleware components themselves.
> 
> Also found while reproducing: `ContentFilter` has no unit tests at all, despite the issue implying all four layers are already covered individually. That's a separate gap from what this issue asks for — I'll flag it as a candidate for its own issue rather than fold it in here.
> 
> Will report back once the test file is in.

---

## Your branch

**Branch**

`test/31-safety-chain-tests`

**Evidence**

[Your Unit 2 reproduction steps re-run against the built change: the before, then the
after. Paste both, including the commands you ran and their output.]

Before:

```
% pytest ./tests/unit/test_prompt_defense.py ./tests/unit/test_bias_detector.py ./tests/unit/test_pii_scrubber.py 
========================================================================================== test session starts ===========================================================================================
platform darwin -- Python 3.13.15, pytest-9.1.1, pluggy-1.6.0
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /Users/***/Downloads/codepath/pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: platformdirs-4.12.2, hypothesis-6.168.3, cov-7.1.0, asyncio-1.4.0, benchmark-5.3.0, pytest_httpserver-1.1.5, anyio-4.15.1
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 89 items                                                                                                                                                                                       

tests/unit/test_prompt_defense.py ......................x.........                                                                                                                                 [ 35%]
tests/unit/test_bias_detector.py xx.....x.............x.xxx.x...x                                                                                                                                  [ 71%]
tests/unit/test_pii_scrubber.py ..xx.......x.....x....x..                                                                                                                                          [100%]

===================================================================================== 74 passed, 15 xfailed in 0.32s =====================================================================================
```

After:

```
% pytest ./tests/unit/test_prompt_defense.py ./tests/unit/test_bias_detector.py ./tests/unit/test_pii_scrubber.py ./tests/integration/test_safety_middleware.py
========================================================================================== test session starts ===========================================================================================
platform darwin -- Python 3.13.15, pytest-9.1.1, pluggy-1.6.0
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /Users/ianwen/Downloads/codepath/pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: platformdirs-4.12.2, hypothesis-6.168.3, cov-7.1.0, asyncio-1.4.0, benchmark-5.3.0, pytest_httpserver-1.1.5, anyio-4.15.1
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 94 items                                                                                                                                                                                       

tests/unit/test_prompt_defense.py ......................x.........                                                                                                                                 [ 34%]
tests/unit/test_bias_detector.py xx.....x.............x.xxx.x...x                                                                                                                                  [ 68%]
tests/unit/test_pii_scrubber.py ..xx.......x.....x....x..                                                                                                                                          [ 94%]
tests/integration/test_safety_middleware.py xxxxx                                                                                                                                                  [100%]

===================================================================================== 74 passed, 20 xfailed in 0.37s =====================================================================================
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

```
18/20
```

**Package analysis**

```
{
  "name": "consistency",
  "grade": "pass",
  "evidence": "Plan follows the repro and the maintainer's thread direction, cites the issue's cases and the #11249 corpus, and states the unmeasured cost and open question as unknowns."
}
```

The rubric acccepted `pkg-20` when its gold label is reject. My rubric, specifically
the `consistency` rule, did not check for the absence of AI-use disclosure when the
project has a strict AI-use disclosure policy, hence the accept when the plan should
be rejected due to missing AI-use disclosure.

**Check rationale**

`| consistency  | plan, plan comment, repro evidence | passes if the proposed fix plan is consistent with the issue listed in repro evidence and can point to data source to prevent hallucinative data | required |`

This line was added after reading `calib-03` in class, which shows valid reproduction
evidence and candidate plan, but the plan doesn't match the evidence.

**Trade-offs**

Nothing changed, the skill evaluated to 18/20 the first time.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
