# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

Where it lives: the plan's diagnosis/cause statement, read against the
repro-evidence block's recorded behavior
  - In an eval bundle/package: the repro-evidence block, the candidate plan
    comment
  - In live mode on GitHub/draft: the issue thread, the student's posted repro
    comment, the draft plan and comment

What good looks like: the stated cause explains the exact behavior the repro
evidence shows — not an adjacent symptom. A diagnosis that stops at the visible
failure point (e.g. "render breaks") without tracing back through the actual
broken stage (e.g. "merge" in the parse→merge→cache→render chain) is
symptom-level, not root-cause. A diagnosis that contradicts or ignores what the
repro evidence actually recorded fails outright, even if it sounds plausible.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

Where it lives: the plan's explicit in-scope / not-in-scope statement (not just
a file list — the boundary line itself), read against the diagnosis and the
files-to-touch list.
  - In an eval bundle/package: the candidate plan's scope statement or test
    plan, the plan comment
  - In live mode on GitHub/draft: the issue thread, the student's posted repro
    comment, the repo's docs, the draft plan and comment

What good looks like: one bounded change with a stated boundary a reviewer could
hold the diff to, e.g. "in: page_count() rounding / not in: the pagination API."
A plan with no not-in-scope line, or one whose approach visibly drifts into
unrelated files ("while I'm here" renames, unrelated config changes, docs passes
not needed by the fix), fails regardless of how good the core fix is — scope
creep is a maintainer no even when the code is right.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

Where it lives: the plan's named files/areas and its approach/order of
work section.
  - In an eval bundle/package: the candidate plan's scope statement or test
    plan, the plan comment
  - In live mode on GitHub/draft: the student's posted repro comment, the draft
    plan and comment

What good looks like: a stranger could start making the change without asking
the author anything — specific files are named (not "the relevant files"), and
the approach states what will actually change, in what order, not just the end
goal. "Fix the bug" is not executable; "replace floor-divide with ceil-divide
in pager.py line X" is.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

Where it lives: the plan's test-plan section, read against the repro
evidence's original steps and artifact.
  - In an eval bundle/package: the candidate plan's scope statement or test
    plan, the plan comment
  - In live mode on GitHub/draft: the student's posted repro comment, the draft
    plan and comment

What good looks like: re-runs the same repro steps and states the expected
observable result *before* the fix is built — a concrete, checkable number or
output, not "verify it works." Example:
"run demo --items 6 --size 2 / today 4 pages / expect 3 pages" — a stated
before/after a stranger can independently confirm. A test plan that doesn't map
back to the original repro steps, or that only promises to "test thoroughly,"
fails.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

Where it lives:
  - In an eval bundle/package: the issue context, the repro-evidence block, the
    candidate plan's scope statement or test plan, the plan comment
  - In live mode on GitHub/draft: the issue thread, the student's posted repro
    comment, the draft plan and comment

What good looks like: stated uncertainty reads as uncertainty — real risks and
unknowns are named, not smoothed into false confidence. A deviation recorded
honestly in plan.md after a build diverges from the original plan is a pass; a
deviation that exists only in the diff and was never written down is not. "No
deviations" stated plainly after a clean build is also a complete, honest
answer.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

Where it lives: the plan comment read against the issue thread's maintainer
signals and the repo-facts block's stated conventions.
  - In an eval bundle/package: the issue context, the repro-evidence block, the
    candidate plan's scope statement or test plan, the plan comment, the
    repo-facts block
  - In live mode on GitHub/draft: the issue thread, the student's posted repro
    comment, the repo's docs, the draft plan and comment

What good looks like: the comment engages what a maintainer already said in the
thread (e.g. "keep the current API, no new flags") rather than ignoring it, and
promises only what the plan itself contains — no scope or fix promised beyond
stated in the plan and comments. Repo-stated conventions (templates,
AI-disclosure policy) are followed. A generic "I can fix this, please assign me"
with no plan-specific content fails.