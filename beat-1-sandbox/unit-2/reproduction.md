# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

`ru1nw`

---

## Posted upstream

**Claim comment**

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

[`https://github.com/codepath/pathreview-ai301-fa26-s1/issues/31#issuecomment-5901768088`](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/31#issuecomment-5901768088)

> I'd like to take a run at this one as a first contribution. I'll read and run what the testcases for each layer look like currently in `tests/unit/test_prompt_defense.py`, `tests/unit/test_bias_detector.py`, `tests/unit/test_pii_scrubber.py`, then report back my findings. There also seems to be no test cases for `ContentFilter` despite the implication of the issue description.

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

[`https://github.com/codepath/pathreview-ai301-fa26-s1/issues/31#issuecomment-5902120027`](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/31#issuecomment-5902120027)

<blockquote>
  environment: PathReview v0.1.0, Python 3.13.15, pytest v9.1.1, macOS 26.5.1 (arm64)
  
  run related test cases
  
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
  
  confirmed that xfails are unrelated issues (58, 53, 24) that are not yet resolved.
  
  expected: a pytest file `tests/integration/test_safety_middleware.py` that covers all components in the safety pipeline
  
  actual: no full pipeline test file
  
  out-of-scope: confirmed that there is no test file that tests ContentFilter. will not be resolved in this issue. recommend to open a separate issue to address this.
</blockquote>

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

```
16/20
19/20
19/20
```

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

The rubric was failing `pkg-03` because it leaned too hard on AI-disclosure statement, so it failed
the repo that did not ask for AI disclosure even if the policy only mandates human-written comments.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

In the check Conventions / Disclosure:

> Distinguish what the policy actually asks for: if it explicitly requires a disclosure statement naming the AI tool and extent of use, treat every candidate package as AI-assisted work regardless of what the draft claims, and fail this check if no such statement appears in the comment text. If the policy instead only asks that comments be written by a human in their own words (no explicit disclosure-statement requirement), pass as long as the comment reads as specific and human-voiced rather than templated.

This was expanded from the simple "fail this if no explicit disclosure statement appears in comment",
which failed `pkg-03`.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

`pkg-10` failed "Behavior Match" even though it's an accept possibly because the repro report
focused too much on how much the reproduction result differed from the issue description, while
the check for Behavior Match specified that the report has to target "the issue's own trigger
condition".

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
