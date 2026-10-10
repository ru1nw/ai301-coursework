# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| silent-drift | The diff's changed files and hunks read against the plan's stated scope and files (plus any deviation notes recorded in the plan), then the description's fidelity claims ("implements the plan exactly", "no changes outside X", "docs now document Y") read against what the diff actually contains. | Pass if (a) every hunk falls inside the plan's scope plus its recorded deviation notes: no new flag, config option, rename, or rewrite the plan does not name, including adjacent work and edits to files the plan never touches; (b) everything the plan promises is in the diff, or the shortfall is disclosed in the plan's deviation notes or the description; and (c) no claim in the description is contradicted by the diff, in either direction (more than planned, or less than claimed). A disclosed, deferred shortfall passes; an undisclosed extra or missing piece fails, however small or well-meant. | required |
| not-tested | The test evidence (commands, output, transcripts) read against the plan's test plan and the issue's repro; the diff's added tests read against the fix; the repo-facts block's stated checks (tests, pre-commit, linters, build) against what the evidence shows was run. | Two tiers. Primary: the plan's repro and each failure mode its test plan names must show an observable before/after on the path the fix changes, with output quoted from the unfixed code and from the branch. Secondary: the plan's controls ("unchanged"), the expected-after side clauses (a warning is printed, a successful save still clears), and the repo's stated checks pass when the evidence states the specific outcome (the command and its result, such as a test count or "clean") or an added test in the diff exercises that behavior; they do not need quoted before/after output. Fail if a primary item is only asserted or never re-run, if the evidence exercises only the unchanged path or a control case, if an added test would pass without the fix, or if a secondary item is silent or only vague ("tests pass", "works locally", "colors work now") with no command or outcome named, or a repo check named in the repo's asks never appears. | required |
| unreviewable | The diff read hunk by hunk for content that is not the planned change: debug prints, commented-out code, dead or unused functions, stray TODOs, whitespace or re-indent churn, reordered or restructured imports, re-printed identical lines, and hunks unrelated to the fix. | Pass if every hunk in the diff is the fix, its test, or a change the repo's stated asks require (such as a changelog entry), so a reviewer reads only the change. Fail if any debris or churn is folded in, even when the underlying fix is correct and even when the churn is mechanical. Judge each hunk by what it changes, not by line text repeated in the diff: lines that appear as both removed and re-added inside a hunk that also edits a line of that same statement (for example `clear=clear` becoming `clear=False` in a multi-line call) are the change as the diff renders it, not churn. Churn is a hunk or lines whose only effect is whitespace, reordering, or re-printing with no change in meaning. Judge the diff's content, not the commit messages or the number of commits. | required |
| standards-wall | The repo-facts block (live: the repo's PR template and `docs/CONTRIBUTING.md`) for the template's required sections and the contribution policy, read against the PR description and the diff (for asks that live in the diff, such as a changelog or whatsnew entry, tests, or type annotations). | Pass if every required template item is visibly satisfied in the description or diff (issue link or "closes" line, checklist items, required file entries) and, where the repo states an AI-disclosure policy, the description contains a disclosure of AI use that meets it. Treat every package as AI-assisted work, so a stated disclosure policy always applies. If the repo states no AI policy, none is required. Fail if a required template section is ignored or left blank, if a stated ask is absent from the diff, or if a stated disclosure policy is unmet. A terse description passes when every stated ask is met. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if every required check passes. `unclear` or `?` on a
required check counts as a fail (proof that cannot be verified is not
ready to post). Preferred checks are recorded but never change the
verdict either way.
