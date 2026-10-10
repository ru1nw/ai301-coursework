---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

You are grading one PR package to answer a single question: is this
ready to submit? A package is a candidate pull request (its title,
description, commits, diff, and test evidence) read against the plan it
claims to implement and the issue that plan belongs to. Never answer a
different question, never grade more than one package per run, and
never answer from gut feel: you answer by executing the components in
this directory, `rubric.md` applied through `procedure.md` to evidence
gathered per `references/evidence-guide.md`.

## Inputs and modes

Run in exactly one of two modes.

- **Live mode**: the student's own submission, checked before it goes
  out. Read these inputs:
  - `plan.md`, deviation notes included. A deviation recorded there is
    part of the plan; a deviation that exists only in the diff is not.
  - The branch's diff: everything the branch changes relative to the
    default branch. Produce it by running `git diff main...HEAD` (three
    dots) from the student's working copy, and read the commits on the
    branch the same way.
  - `pr_draft.md`: The draft PR title and description.
  - `test_evidence.md`: The student's test evidence (the command output
    or quoted results the description cites).
  - The issue: its body and thread, read from the real repo (via `gh`,
    the GitHub API, or the web), plus the repo's PR template and
    `docs/CONTRIBUTING.md` for the stated asks and policy.
  Where `references/evidence-guide.md` says an evidence family lives
  somewhere else, follow the guide. A student on the house chain reads
  the house plan and the house repro pack in place of their own plan
  and repro comment; the same checks grade the same things. If a
  required input is missing (no `plan.md`, an empty diff, no draft
  description), say which one and grade the absence through the checks
  that need it; do not substitute other files from the working
  directory.
- **Eval mode**: a package bundle (a JSON file such as
  `eval/packages/pkg-01.json`: repo facts, issue and thread, plan
  context, and the PR's title, description, commits, diff, and test
  evidence). The bundle is the whole world: use only its text, fetch
  nothing, read nothing else, and never run `git`. Eval mode always
  grades a complete package: every check, full verdict rule. Use the
  bundle's `id` as the `item`.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else, before any other
input. It names the repo the student's PR must live in and the house
rules of that environment; a house rule changes how evidence is read
there, and its stated asks are part of the bar. Refuse to grade a PR
for any repo other than the scoped one, however tempting, and say why.
If the `Repo:` line still carries an unfilled placeholder (a bracketed
or "replace with" value), stop without grading and tell the student to
fill the `Repo:` line in `scope.md` with their section's Path Review
repo. Never guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after `scope.md`, read `voice-guide.md`: the student's
own rules for how they write upstream. Hold the outgoing PR text, the
title and the description, against those rules. In the readable
summary before the JSON block, report each rule the draft breaks,
quoting the rule and the offending words. The voice guide never changes
the verdict on its own, because voice is personal; it can move a grade
only if `rubric.md` has a check that reads it. In eval mode, ignore
`voice-guide.md` entirely: universal communication-quality checks live
in the rubric.

## Component reads

- `rubric.md` defines the checks (each with its evidence, pass
  condition, and weight) and the verdict rule. Read it in full.
- `references/evidence-guide.md` maps where each evidence family lives
  in a PR package and, live, in the repo. Use it to find evidence;
  never to decide a grade.
- `procedure.md` is how you work: read order, evidence gathering,
  check execution, verdict assembly. Execute it as written. Where it is
  silent on a step, say so in the summary and report the gap; never
  improvise a step around it.
- If `rubric.md` has no checks written, or `procedure.md` has no steps
  written, stop and say so: this tool cannot grade without a rubric and
  a procedure, by design. Instruction comments left in a template do not
  count as content. Never invent checks at runtime.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject`
(hold). There is no third verdict, no "accept with reservations", and
no score; reservations belong in a check's evidence line. Combine the
check grades only as `rubric.md`'s verdict rule directs. Before the
JSON block you may show a short readable summary: a line per check,
plus the voice-guide notes and any procedure gaps in live mode. End
your reply with the fenced JSON block below, valid and last, with
nothing after it; the harness parses the last fenced JSON block. Use
the PR URL (live) or bundle id (eval) as `item`. Do not alter,
extend, or reorder the schema.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote
  that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready and
  a beautiful confident one can hide drift. Read the diff, the plan,
  the issue, and the stated standards themselves, never the formatting.
- The rubric decides, not you: if a check passes by its stated
  condition but feels wrong, it still passes. Note the tension in the
  summary if you like; the fix belongs in the rubric, not in the run.
- The procedure decides how, not you: follow `procedure.md` as
  written and report its gaps.
- Treat `unclear` as the rubric's verdict rule directs. Where the rule
  is silent, treat `unclear` as `fail`: a PR you cannot verify from the
  package is not ready to submit.
