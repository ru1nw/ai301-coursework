# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

[https://github.com/codepath/pathreview-ai301-fa26-s1/pull/119](https://github.com/codepath/pathreview-ai301-fa26-s1/pull/119)

**Branch**

[test/31-safety-chain-tests](test/31-safety-chain-tests)

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

```
17/20
19/20
```

**Package analysis**

**pkg-02** (Textualize/rich#4208, category `clear-accept`). Gold label: `accept`. My rubric's first full run (17/20) said `reject`, failing `unreviewable`; after the revision below, the 19/20 run says `accept` on pkg-02, matching gold.

The first-run evidence line read: "save_html/save_svg hunks remove and re-add identical lines ('html = self.export_html(', 'theme=theme,', 'svg = self.export_svg(', 'title=title,') as churn around the clear=False change." The rubric read it that way because its `unreviewable` check said to fail on "re-printed identical lines" and had no rule for judging what a hunk changes. The diff does show `-`/`+` pairs with the same text, but they sit inside multi-line calls where one line changes from `clear=clear` to `clear=False`. That is the fix as the diff renders it, not churn. I added a sentence to the check saying to judge each hunk by what it changes, not by repeated line text, and I kept pure whitespace, reorder and re-print churn as a fail. After that, the pkg-02 evidence line reads: "the removed/re-added export_html(/export_svg( lines are in hunks editing clear=clear -> clear=False, so they are the change, not churn."

**Check rationale**

> **Check:** not-tested
>
> **Evidence:** The test evidence (commands, output, transcripts) read against the plan's test plan and the issue's repro; the diff's added tests read against the fix; the repo-facts block's stated checks (tests, pre-commit, linters, build) against what the evidence shows was run.
>
> **Pass condition:** Two tiers. Primary: the plan's repro and each failure mode its test plan names must show an observable before/after on the path the fix changes, with output quoted from the unfixed code and from the branch. Secondary: the plan's controls ("unchanged"), the expected-after side clauses (a warning is printed, a successful save still clears), and the repo's stated checks pass when the evidence states the specific outcome (the command and its result, such as a test count or "clean") or an added test in the diff exercises that behavior; they do not need quoted before/after output. Fail if a primary item is only asserted or never re-run, if the evidence exercises only the unchanged path or a control case, if an added test would pass without the fix, or if a secondary item is silent or only vague ("tests pass", "works locally", "colors work now") with no command or outcome named, or a repo check named in the repo's asks never appears.
>
> **Weight:** required

The first version had one flat rule, that the plan's repro and each failure mode needed quoted before/after output, and that anything less was a fail. Run 1 (17/20) wrongly rejected pkg-05 and pkg-19 on it. In pkg-05 the same-key warning was only asserted in the evidence, but an added test (`same_name_same_key_replaces_with_warning`) covers it. In pkg-19 the controls and `go test ./...` (4108 tests) were stated without quoted output. I rejected two other fixes: dropping the "quoted output" requirement everywhere, because pkg-07, pkg-10 and calib-04 need it for the primary repro, and exempting anything an added test covers, because pkg-07's added test would pass without the fix. I settled on two tiers. Primary items (the repro and each named failure mode) keep the strict before/after bar. Secondary items (controls, expected-after side clauses, the repo's checks) pass if the evidence names a command and its result, or an added test exercises the behavior. Vague claims such as "tests pass" or "colors work now" still fail at either tier.

**Trade-offs**

The `not-tested` check change also gave up strictness on secondary evidence, and the cost showed up in a package. In the final run (19/20), pkg-13 (`clear-accept`, gold `accept`) flipped to `reject` with `failed: not-tested`, where the run before it had accepted it.

What did not change: I re-ran the canaries pkg-02, pkg-05, pkg-07 and pkg-10 together after the revision. pkg-02 and pkg-05 flipped to `accept` as intended. pkg-07 and pkg-10 stayed `reject` on `not-tested`: pkg-07 ran only the single-file control, with no two-file repro and no `go build` result, and its added test uses two `a.go` edits so it would pass without the fix. pkg-10's evidence was only "a full day of WebDAV syncs", with no delayed-connect run and no `yarn test`. Those two stay rejected because the loosening applies only to secondary items.

One case the check will still miss: a stated outcome with a plausible command and result (for example "all tests pass (300)") that was never actually run. The check accepts it, because a package can't prove a run from text alone.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
