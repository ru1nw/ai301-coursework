# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[Add integration tests for the full safety middleware chain #31](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/31)

**Verdict output**

```
Fit profile in scope.md is now filled in: "Experienced web developer using React JS/TS, HTML/CSS, Python (Flask), and Django. Well-versed in fetching API and performing web requests and scrubbing." All three issues live in the Python backend (none touch the React frontend), so ranking comes down to which backend work matches the profile's specific keywords.

Ranked read-out (all three accept):

1. #31 — Add integration tests for the full safety middleware chain. Best fit: the profile names "scrubbing" directly, and this issue's own scope is testing the PII scrubber (plus prompt defense, content filter, bias detector) end-to-end. community-alive pass / unclaimed pass / ai-policy pass / scope-fit pass (1 named file, 4–7h, 0 failed PRs).
2. #9 — Implement a caching layer for repeated identical portfolio queries. Fit: touches rag/generator/review_generator.py, which drives the LLM-facing "fetching API and performing web requests" side of the profile. community-alive pass / unclaimed pass / ai-policy pass / scope-fit pass (2 named files, 4–7h, 0 failed PRs).
3. #3 — Add a content hash to detect unchanged documents and skip re-embedding. Fit: same caching pattern as #9 but on the ingestion/parsing side, which the profile doesn't call out — still solid Python backend work, just the weaker keyword match. community-alive pass / unclaimed pass / ai-policy pass / scope-fit pass (2 named files, 4–6h, 0 failed PRs).

All three share the same repo-level evidence: last commit by the repo's own account (Aburke225, COLLABORATOR) on 2026‑09‑16 (6 days ago), 0 open PRs referencing any of the three issue numbers (the repo's only PR, #74, is unrelated), no assignees or comments on any of them, and no AI-contribution ban anywhere in README.md, docs/CONTRIBUTING.md, or .github/. All three also fail the preferred shipped-recently check (0 GitHub releases) — that never changes the verdict.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/31",
    "checks": [
      {"name": "community-alive", "grade": "pass", "evidence": "Repo's account (Aburke225, COLLABORATOR) committed 2026-09-16T21:48:27Z, 6 days before today"},
      {"name": "unclaimed", "grade": "pass", "evidence": "0 comments, assignees: [], repo's only PR (#74) is unrelated"},
      {"name": "ai-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and README contain no AI-contribution ban; no AI_POLICY.md found"},
      {"name": "scope-fit", "grade": "pass", "evidence": "Body names 1 file (tests/integration/test_safety_middleware.py), 4-7h estimate, 0 failed PRs referencing #31"},
      {"name": "shipped-recently", "grade": "fail", "evidence": "GET /releases returns 0 releases"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/9",
    "checks": [
      {"name": "community-alive", "grade": "pass", "evidence": "Repo's account (Aburke225, COLLABORATOR) committed 2026-09-16T21:48:27Z, 6 days before today"},
      {"name": "unclaimed", "grade": "pass", "evidence": "0 comments, assignees: [], repo's only PR (#74) is unrelated"},
      {"name": "ai-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and README contain no AI-contribution ban; no AI_POLICY.md found"},
      {"name": "scope-fit", "grade": "pass", "evidence": "Body names 2 files (rag/generator/review_generator.py, core/services/review_service.py), 4-7h estimate, 0 failed PRs referencing #9"},
      {"name": "shipped-recently", "grade": "fail", "evidence": "GET /releases returns 0 releases"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/3",
    "checks": [
      {"name": "community-alive", "grade": "pass", "evidence": "Repo's account (Aburke225, COLLABORATOR) committed 2026-09-16T21:48:27Z, 6 days before today"},
      {"name": "unclaimed", "grade": "pass", "evidence": "0 comments, assignees: [], repo's only PR (#74) is unrelated"},
      {"name": "ai-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and README contain no AI-contribution ban; no AI_POLICY.md found"},
      {"name": "scope-fit", "grade": "pass", "evidence": "Body names 2 files (ingestion/pipeline.py, core/models/ingested_source.py), 4-6h estimate, 0 failed PRs referencing #3"},
      {"name": "shipped-recently", "grade": "fail", "evidence": "GET /releases returns 0 releases"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

```
15/20
2/5
3/3
13/20
1/5
1/5
2/5
0/3
15/20
2/5
0/3
0/3
2/3
15/20
1/5
4/7
4/7
3/7
3/7
4/7
3/7
3/7
5/7
16/20
17/20
0/1
0/1
1/1
12/20
0/1
1/1
14/20
18/20
```

**Issue analysis**

```
{
  "rubric": "/Users/ianwen/.claude/skills/issue-select/rubric.md",
  "model": "sonnet",
  "agreement": [
    0,
    1
  ],
  "results": [
    {
      "id": "issue-19",
      "verdict": "reject",
      "failed_checks": [
        "scope-fit"
      ],
      "checks": [
        {
          "name": "community-alive",
          "grade": "pass",
          "evidence": "Merges landed 2026-08-04 (#554, #551), one day before capture on 2026-08-05."
        },
        {
          "name": "unclaimed",
          "grade": "pass",
          "evidence": "assignees: none; linked PRs: none"
        },
        {
          "name": "ai-policy",
          "grade": "pass",
          "evidence": "CONTRIBUTING.md has no statement on AI or contribution tooling"
        },
        {
          "name": "scope-fit",
          "grade": "fail",
          "evidence": "Issue lists 2 potential root causes plus 3 open-ended suggestions (multi-processing, conditional matching, separate-thread rewrite application) \u2014 an unscoped concurrency/perf investigation, not one bounded change"
        },
        {
          "name": "shipped-recently",
          "grade": "pass",
          "evidence": "latest release v1.0.0 (2026-04-29), within a year of the 2026-08-05 capture"
        }
      ],
      "error": null
    }
  ]
}
```

My rubric rejects issue-19, even though the gold label is accept. `scope-fit`
failed due to listing various potential causes and suggestions, which the model
deemed too broad to be a limited scope.

**Check rationale**

```
| `scope-fit` – One bounded change, spec included.          | repo-facts block, issue body     | solution does not lead to breaking or significant changes, and has less than 2 failed PR | required  |
```

This one gave me the most issue. I first approached it with the given language about
"bounded change", "limited scope", etc., but that was still giving me a lot of
disagreement. I also tried approaching it with more specific language such as "change
less than 1 aspect of project" or "necessary code change clearly listed", but that could
not capture all the accept cases. I landed with the first part after comparing the accept
issues that kept getting falsely rejected, namely issue-01, issue-04, issue-11, and
issue-19, then issue-15 started getting accepted when it should not have, which prompted me
to add the second part of the pass condition.

**Trade-offs**

The check gives up small scope changes that says too much or too little in the issue body,
both of which prompted the model to assume that the scope is not limited.

---

## Selection rationale

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

1. Fits my interest in improving security features, in this case adding safety test cases.
   Time required is 4-7 hours, which is doable in separate work sessions in 1-2 days.
2. Although the issue named only 1 file to fix, writing test cases requires understanding
   the files that need to be tested, which is going to take longer.
3. Medium difficulty, but unsure until the final scope of the files that need to be tested
   is clear.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
