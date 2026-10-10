# Procedure: how this tool grades a PR package

Execute these steps in order, as written. Where a step is silent on
something you need, report the gap in the summary; do not invent a
step. Source names below are the live-mode sources, with the eval
bundle section in parentheses. In eval mode, take every fact from the
bundle text only.

## Read order

Read the plan before the diff and the diff before the description, so
each later read is judged against something already fixed and the
description's claims cannot shape what you see in the diff.

1. Live mode only: read `scope.md` first (stop per SKILL.md if the repo
   line is a placeholder or the PR is for another repo), then
   `voice-guide.md`. Skip both in eval mode.
2. Read the issue: its body and thread (bundle: the issue block and
   thread highlights). Note the reported failure, the repro, and any
   direction a maintainer gave.
3. Read the plan (live: `plan.md`; bundle: the plan-context block). Note
   four things: the stated scope and files, what is explicitly out of
   scope, the test plan (every repro or failure mode it says it will
   re-run), and every deviation note, if any.
4. Read the diff (live: the output of `git diff main...HEAD`; bundle:
   the diff field) hunk by hunk. For each hunk note its file, what it
   does, and whether it is code, test, docs, or neither. Read the
   commit list alongside it.
5. Read the test evidence (live: the captured output the description
   cites; bundle: the test-evidence field). Note each command run, what
   was observed before and after, and which repo checks it claims.
6. Read the repo's asks (live: the PR template and
   `docs/CONTRIBUTING.md`; bundle: the repo-facts block). Note each
   required template item, each file entry it requires, and any stated
   AI-disclosure policy.
7. Read the PR title and description last (live: the draft; bundle:
   the pr title and description fields). Note every claim it makes
   about the plan, the diff, and the evidence, and which template
   sections and disclosure it contains.

## Evidence gathering

Gather for every check before grading any of them. Record each fact
with its source so each grade can quote it.

1. silent-drift. Build two lists. List A: every changed file and hunk
   from step 4 of the read order. List B: the plan's named files and
   scope, plus the deviation notes. Pair them: mark each hunk "in
   plan" or "not in plan", and each promised plan item "present" or
   "absent". Then list every fidelity claim in the description ("exactly
   as planned", "no changes outside X", "docs now document Y") and mark
   each "backed by the diff" or "contradicted by the diff". A promised
   item marked absent counts as covered only if a deviation note or the
   description discloses the shortfall.
2. not-tested. Pair the plan's test plan against the evidence: for each
   repro or failure mode the test plan names, find the quoted run on
   the unfixed code and the quoted run on the branch, and mark it
   "shown before and after", "shown once", or "not shown". Do this for
   primary items only (the repro and each named failure mode). Then
   list the secondary items: the plan's controls, the expected-after
   side clauses (a warning printed, a successful save still clears),
   and the repo checks. Mark each "outcome stated" (the evidence names
   the command and its result), "covered by an added test" (a hunk in
   the diff exercises it), or "silent or vague". Note whether the
   primary run exercises the path the fix changes or a control or
   unchanged path. Read the added test in the diff and ask whether it would pass
   without the fix. Compare the repo checks the repo-facts block (live:
   the template and `docs/CONTRIBUTING.md`) says must run against the
   checks the evidence shows were run, and note any never run.
3. unreviewable. From the hunk-by-hunk read, judging each hunk by what
   it changes (a removed and re-added line inside a hunk that edits
   that same statement is the change, not churn), list every debug print,
   commented-out block, dead or unused function, stray TODO,
   whitespace or re-indent change, import reorder, re-printed
   identical line, and hunk unrelated to the fix or its test. Quote the
   line for each. A hunk the repo's stated asks require (a changelog
   entry, say) is not debris.
4. standards-wall. Pair the repo's asks against the PR: for each
   required template item and file entry from the read order, find it
   in the description or the diff and mark "met" or "missing"; if a
   disclosure policy is stated, find the disclosure in the description
   and mark "met" or "missing". Treat every package as AI-assisted. If
   no policy is stated, mark disclosure "not required".
5. If a needed fact is absent (no test plan in the plan, no evidence
   section, no diff, no repo asks), record it as "absent". Do not fill
   it from memory, from other files in the working directory, or, in
   eval mode, from anywhere outside the bundle.

## Check execution

1. Run the checks in the rubric's table order: silent-drift,
   not-tested, unreviewable, standards-wall. Run all four even after
   one fails; the output reports every check.
2. Grade each check `pass`, `fail`, or `unclear` by applying the pass
   condition in `rubric.md` to the pairings from evidence gathering,
   not to your impression of the PR. Use the pairings only; do not
   re-read the whole package for a check, except to resolve a fact
   you recorded as uncertain.
3. Grade `fail` when any pairing breaks the pass condition: a hunk
   marked "not in plan", a promised item "absent" and undisclosed, a
   claim "contradicted", a test-plan item "not shown" or "shown
   once", an evidence run on a control path, an unrun repo check, any
   debris line, any ask marked "missing". For not-tested, `fail` means
   a primary item marked "shown once" or "not shown", or a secondary
   item marked "silent or vague"; a secondary item marked "outcome
   stated" or "covered by an added test" does not fail the check.
4. Grade `unclear` only when the evidence for a check is genuinely
   absent or cannot be read (for example, the diff is truncated or the
   test plan is missing), and say which fact is missing. Do not use
   `unclear` to avoid a close call; decide it by the pass condition. A
   disclosed, deferred shortfall passes. Do not fail a package for
   being terse or for doing less than everything when the plan or the
   description says so honestly.
5. Write one evidence line per check: the single fact or quote that
   decided it (the offending hunk's file, the unmatched claim, the
   missing run, the debris line, the missing ask). For a pass, quote
   the fact that satisfied the condition, such as the before/after
   output.
6. Live mode only: compare the title and description to each rule in
   `voice-guide.md` and list every rule broken in the summary, quoting
   the rule. These notes never change a grade.

## Verdict assembly

1. Apply the rubric's verdict rule: all four checks are required, so
   the verdict is `accept` only if all four are `pass`.
2. Any `fail`, or any `unclear`, on any check makes the verdict
   `reject`. `unclear` is treated as `fail`.
3. When more than one check fails, the deciding check is the first
   failing check in rubric order (silent-drift, not-tested,
   unreviewable, standards-wall). Name it first in the summary and
   quote its evidence line. The other failing checks are still graded
   and reported.
4. Output the readable summary (one line per check, then any
   voice-guide notes and procedure gaps), then the fenced JSON block
   from `SKILL.md`: one entry per check in rubric order, each with its
   grade and evidence line, then the verdict. Nothing follows the
   block.
