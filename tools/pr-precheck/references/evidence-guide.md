# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

**Where it lives**

- *Eval bundle* (e.g. `calib-01.md`): the plan lives in `## Plan context`. Its `Plan:` paragraph gives the steps, the `Not in scope:` sentence and the `Files:` line give the boundary, and any deviation note sits in the same block. What the PR changed is `### Diff` under `## Candidate PR`, with `### Commits` beside it. The claims to check are in `### Description` and `### Title`.
- *Live*: the plan is your `plan.md`, with its deviation notes. The change is the output of `git diff main...HEAD`, not the diff pasted into `pr_draft.md`, which can go stale. The claims are in `pr_draft.md`: the change summary, the change deviation section, and the out-of-scope issues section.

**What good looks like**

- Every changed file and hunk falls inside the plan's `Files:` and steps, or is covered by a deviation note. In `calib-01` the one deleted line is in `themes.gitconfig`, the only planned file.
- Everything the plan promises is in the diff, or the shortfall is disclosed in a deviation note or the description. A deferral stated in both the plan and the description is honest, not drift.
- Work the plan scopes out stays out. In live mode, an idea you left out belongs in the out-of-scope issues section of `pr_draft.md`, not in the diff.
- Each fidelity claim in the description ("exactly as planned", "no changes outside X", "docs now document Y") is backed by the diff. Drift runs both ways: extra work, and a claim of more than the diff delivers. A deviation recorded only in the diff, with no note in `plan.md` or the draft's change deviation section, is silent drift.

## Test evidence (harness category: not-tested)

**Where it lives**

- *Eval bundle*: the proof is `### Test evidence` under `## Candidate PR`. Read it against the plan's `Test plan:` sentence in `## Plan context` and the repro in the issue and the plan's repro-evidence paragraph. Added tests appear as hunks in `### Diff`. The repo's stated checks are in `## Repo facts`.
- *Live*: the proof is `test_evidence.md` (the pytest result and the output of `make test-unit`, `make test-integration`, `make lint`, and `make typecheck`) and the before and after test results and screenshots in `pr_draft.md`. Read them against the test plan in `plan.md` and the repro in your issue. Added tests are hunks in `git diff main...HEAD`. The repo's required checks come from the PR template and `docs/CONTRIBUTING.md`.

**What good looks like**

- Decisive, for primary items: each repro or failure mode the plan's test plan names is run on the unfixed code and on the branch, with the output quoted, the expected result stated and the observed result matching it.
- Enough, for secondary items (controls, expected-after side clauses such as a warning or a successful save still clearing, the suite): the evidence names the command and its result ("`go test ./...` passes (4108 tests)"; "`cargo test -p nu-protocol` passes (312 tests); fmt and clippy clean"), or an added test in the diff exercises the behavior (a test asserting the one-time warning). These do not need quoted before/after output. `calib-01` shows `DuplicateOptionError` before and `parsed OK` after, and also the `git config --get-all` and `--show-syntax-themes` checks the plan named.
- The run exercises the path the fix changes, not a control or unchanged path. An added test fails without the fix.
- The repo's stated checks were run and their outcomes are visible. In live mode that means each of `make test-unit`, `make test-integration`, `make lint`, and `make typecheck` appears in `test_evidence.md` with its result. A target missing from the file counts as not run.
- Not decisive: "tests pass" or "works locally" with no command or output named, a single run with no before, or evidence for one failure mode when the plan names two.

## Diff quality (harness category: unreviewable)

**Where it lives**

- *Eval bundle*: `### Diff` under `## Candidate PR` (read every hunk) and `### Commits`.
- *Live*: the output of `git diff main...HEAD` from your working copy, and `git log main..HEAD` for the commits. Do not grade the diff pasted into `pr_draft.md` in place of the real one.

**What good looks like**

- The fix is visible and nothing else rides along: every hunk is the fix, its test, or a change the repo's asks require (a changelog entry, say). `calib-01` is one removed line.
- No debug prints or leftover logging, commented-out code, dead or unused functions, stray TODOs, whitespace or re-indent churn, import reordering, re-printed identical lines, or hunks unrelated to the fix. Mechanical churn around a correct fix still counts as debris. A unified diff can show `-`/`+` pairs with the same text when one line of a multi-line statement is edited (for example `clear=clear` to `clear=False` inside a call); that is the change, not churn. Read what each hunk changes, not whether lines repeat.
- Judge the content of the diff, not the commit messages or their count. Commit messages are context for finding debris, not a grade.

## Standards and comms (harness category: standards-wall)

**Where it lives**

- *Eval bundle*: the repo's asks are in `## Repo facts`: the `pull requests:` line (PR template sections and required file entries, or "no PR template" with the contribution docs' asks) and the `contribution policy` line (including any AI policy). Whether the PR honors them is in `### Description` and `### Diff`. Maintainer direction is in `## Thread highlights`.
- *Live*: the repo's PR template and `docs/CONTRIBUTING.md` give the asks, and `scope.md` adds the house rules (the template is always used, PR from `fix/<issue-number>-<slug>` on your fork, one PR per issue). The PR's side is `pr_draft.md`: the issue number, the change summary, the AI disclosure section, and the other template sections. Asks that live in the diff, such as a changelog entry, tests or type annotations, are checked in `git diff main...HEAD`. Maintainer direction is in your issue's thread.

**What good looks like**

- Every required template item is visibly satisfied with real content: the issue link or "closes" line, each checklist item, each required file entry in the diff. Boilerplate left blank, or a checklist ignored, is a miss.
- Where the repo states an AI-disclosure policy, the description contains a disclosure that meets it. Treat every package as AI-assisted. If the repo states no AI policy, nothing is required; `calib-01` has none and passes. In live mode, AI disclosure must be present in `pr_draft.md`, either in its own section or under `Notes for Reviewers`, and in your own words wherever the repo states a policy.
- Explicit maintainer direction in the thread is engaged, not ignored.
- A terse description passes when every stated ask is met. Whether its claims match the diff is plan fidelity, above.
