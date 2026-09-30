# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

| Signal | In the eval bundle | In live mode | What good looks like |
|---|---|---|---|
| Runtime/tool versions | the repro report's environment section | the repro comment on the issue, or a linked CI/local run | exact versions stated (not "latest"), matching or explicitly diverging from what the issue's repo-facts block or issue body targets |
| OS / platform | same environment section | same comment | named explicitly when the issue is platform-sensitive; can be omitted only when the bug is clearly platform-independent |
| Install method / build profile | environment section, or a setup-command block above the repro steps | same comment, or a linked commit/branch | stated when it affects the bug (e.g. built from source vs. installed release, debug vs. release build) |

A report that skips a version the issue's own behavior depends on (e.g. the issue is version-gated but the report says nothing) fails Environment Recorded regardless of how much else it states.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

| Signal | In the eval bundle | In live mode | What good looks like |
|---|---|---|---|
| Starting state | the top of the repro report, before the numbered steps | the comment's setup description | states what exists before step 1 (fresh clone, specific branch, seeded data) — not assumed |
| Ordered actions | the repro report's steps/commands block | the comment's numbered steps or code block | each step is a literal command or action, in the order run, with no "and then configure it as usual"-style gaps |
| Trigger condition | wherever the steps say the bug appears | same | the exact action that flips from normal to broken is named, not left implicit |

What good looks like, overall: a stranger with zero prior context, given only the environment section and this steps block, could reach the same state without guessing or asking a question.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

| Signal | In the eval bundle | In live mode | What good looks like |
|---|---|---|---|
| Output/log excerpt | the repro report's output or artifacts section, read against the issue's description | pasted terminal output or a linked log in the comment | the excerpt is read side-by-side with the issue's stated symptom, not just present |
| Screenshot | same section | attached image on the issue | shows the specific failure state named in the issue, not a generic error screen |
| Error identity | compare exact error text/exit code/stack trace to the issue | same | matches the issue's reported error — same message, same failure point — not a similar-looking but distinct error from a different code path |

What good looks like, overall: the artifact, read on its own with no narration, actually shows the behavior the issue describes — you shouldn't need the reporter's summary to see it.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

| Signal | In the eval bundle | In live mode | What good looks like |
|---|---|---|---|
| Stated conclusion | the report's final verdict line ("reproduced" / "could not reproduce") | the closing line of the comment | present explicitly — not left for the reader to infer from the artifacts alone |
| Conclusion vs. evidence | compare the conclusion against the Behavior-shown artifact directly above it | same | the conclusion claims no more than the artifact supports — a "cannot reproduce" backed by a genuine, described attempt is a pass; an "I reproduced it" resting on a wrong-target artifact, or on no artifact, is a fail |
| Uncertainty disclosed | any hedge language in the report | any hedge language in the comment | genuine uncertainty is stated as uncertainty, not smoothed into false confidence |

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

| Signal | In the eval bundle | In live mode | What good looks like |
|---|---|---|---|
| Repo conventions | the repo-facts block's contribution policy / issue-template line | `CONTRIBUTING.md`, `AI_POLICY.md`/`AI_USAGE_POLICY.md`, or a template checkbox, per Unit 1's fifth surface | every stated convention is followed in the actual comment text — not just acknowledged |
| AI-use disclosure | same repo-facts line | same files | Two different policy shapes look similar but grade differently — read the repo-facts line carefully before picking one: (1) **explicit disclosure requirement** — the policy says usage must be disclosed, naming the tool and extent (e.g. "all AI usage must be disclosed, stating the tool used and the extent of the assistance"). Here, treat every candidate package as AI-assisted work regardless of what the draft claims about itself, and fail if the comment text contains no explicit disclosure statement, even if the rest of the package is excellent. (2) **human-voice requirement, no disclosure ask** — the policy only asks that comments be written by a human in their own words (AI help with wording/proofreading is fine, no statement required). Here, nothing is owed beyond the comment reading as specific and human-voiced rather than templated or robotic; do not fail it for lacking a disclosure line it was never asked to include. A repo with no stated AI policy at all owes neither (silence passes, per Unit 1) |
| Comment specificity | the claim comment's own wording, read against the issue | same | names this issue's specifics — not a boilerplate "I'll take a look," and (for the claim comment specifically) promises investigation and a report, not a fix or a date |