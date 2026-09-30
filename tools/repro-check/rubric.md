# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment Recorded | The repro report's stated environment (OS, tool/runtime version, install method, any other version the issue depends on) | Every environment detail needed to place the run relative to the issue's target is stated explicitly — no "latest," no omission of a detail the issue's behavior turns on (e.g. build profile, driver, OS) | required |
| Steps Reproducible | The repro report's commands/actions, read against its stated environment and starting state | A stranger with no other context, starting from the stated environment, could run these exact steps in this order and land in the same state — no missing setup, no skipped trigger condition | required |
| Behavior Match | The report's shown artifact (output, log, screenshot) read against the issue's description of the bug, and against the steps that produced it | If the report claims reproduction, the artifact shows the *same* behavior the issue reports, not a different code path, error, or exit condition that merely looks similar. If the report claims it could NOT reproduce, this check passes as long as the steps taken genuinely targeted the issue's own trigger condition (not a substituted or adjacent one) — a faithful attempt that comes up empty is not a Behavior Match failure; a botched or substituted trigger narrated as a negative result still fails | required |
| Honest Outcome | The report's stated conclusion read against what its own artifact actually shows | The conclusion is no stronger than the evidence: a cannot-reproduce backed by a real, faithful attempt passes, an "accept"/certainty claim resting on the wrong-target artifact or on no artifact fails | required |
| Conventions / Disclosure | The repo-facts block's stated bug-report template and contribution/AI-disclosure policy, read against the actual claim comment and repro report text | The comments meet every convention the repo states as required. Distinguish what the policy actually asks for: if it explicitly requires a disclosure statement naming the AI tool and extent of use, treat every candidate package as AI-assisted work regardless of what the draft claims, and fail this check if no such statement appears in the comment text. If the policy instead only asks that comments be written by a human in their own words (no explicit disclosure-statement requirement), pass as long as the comment reads as specific and human-voiced rather than templated. A repo with no stated AI policy cannot fail on disclosure | required |
| Claim Scope | The claim comment's own wording | The comment states intent to investigate and promises a report; it does not promise a fix, a timeline, or assert a result not yet obtained in the report | required |

## Verdict rule

Accept only if every required check passes. `unclear` on a required
check counts as a fail (proof that cannot be verified is not ready to
post). Preferred checks are recorded but never change the verdict
either way.
