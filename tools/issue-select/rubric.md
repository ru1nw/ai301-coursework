# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
| ----- | -------- | -------------- | ------ |
| `community-alive` – Someone still merges and replies.     | repo-facts block, comment thread | maintainers merge or reply within the past 90 days | required  |
| `unclaimed` – No assignee, no open PR, no fresh claim.    | repo-facts block, comment thread | issue is not claimed by or assigned to any user | required  |
| `ai-policy` – Allows AI contribution                      | repo-facts block                 | no explicit statement outright disallowing AI code or PR contribution | required  |
| `scope-fit` – One bounded change, spec included.          | repo-facts block, issue body     | solution does not lead to breaking or significant changes, and has less than 2 failed PR | required  |
| `shipped-recently` – Releases ship; people depend on it.  | repo-facts block                 | a release was shipped within the past year                            | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

accept only if every required check passes, reject otherwise. a `?` counts as a fail on a required check. never let preferred checks change the verdict.
