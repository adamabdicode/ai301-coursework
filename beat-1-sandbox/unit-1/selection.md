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

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73

**Verdict output**

- maintainer_commits: pass. Newest of the last 5 main commits 
- maintainer_response: fail. Sampled recently updated issues have no Owner, Member, or Collaborator reply.
- repo_in_use: pass. archived: false, and the last push to any branch was 2026-09-16.
- scope_bounded: pass. Body asks to make README.md and .env.example agree on OPENROUTER_API_KEY; 
- is_contribution: pass. The issue asks to change README.md and .env.example, not how to run the app.
- no_abandoned_attempts: pass. No closed unmerged PR is linked; the only linked PR is open.
- no_assignee: pass. Assignees: none.
- no_active_pr: fail. PR #77 by Tiyatrotist is open and its body says Closes #73.
- no_live_claim: pass. Claim comments are from other students; the Path Review house rule says those do not block the issue.
- ai_policy_allows: pass. No CONTRIBUTING.md, AI_POLICY.md, or AGENTS.md in the repo.
- newcomer_label: pass. Labels include good first issue.
- maintainer_in_thread: fail. All 30 comments have author_association NONE.
- adoption_scale: fail. The repo has 3 stars.
- recent_release: fail. The releases list is empty.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
  "checks": [
    {"name": "maintainer_commits", "grade": "pass", "evidence": "Newest of the last 5 main commits is 2026-09-16 by Aburke225, within 90 days of 2026-10-02."},
    {"name": "maintainer_response", "grade": "fail", "evidence": "Sampled recently updated issues (#68, #1, #63, #72, #57, #29) have no Owner, Member, or Collaborator reply."},
    {"name": "repo_in_use", "grade": "pass", "evidence": "archived: false, and the last push to any branch was 2026-09-16."},
    {"name": "scope_bounded", "grade": "pass", "evidence": "Body asks to make README.md and .env.example agree on OPENROUTER_API_KEY; opened 2026-09-16, not an umbrella."},
    {"name": "is_contribution", "grade": "pass", "evidence": "The issue asks to change README.md and .env.example, not how to run the app."},
    {"name": "no_abandoned_attempts", "grade": "pass", "evidence": "No closed unmerged PR is linked; the only linked PR is open."},
    {"name": "no_assignee", "grade": "pass", "evidence": "Assignees: none."},
    {"name": "no_active_pr", "grade": "fail", "evidence": "PR #77 by Tiyatrotist is open and its body says Closes #73."},
    {"name": "no_live_claim", "grade": "pass", "evidence": "Claim comments are from other students; the Path Review house rule says those do not block the issue."},
    {"name": "ai_policy_allows", "grade": "pass", "evidence": "No CONTRIBUTING.md, AI_POLICY.md, or AGENTS.md in the repo."},
    {"name": "newcomer_label", "grade": "pass", "evidence": "Labels include good first issue."},
    {"name": "maintainer_in_thread", "grade": "fail", "evidence": "All 30 comments have author_association NONE."},
    {"name": "adoption_scale", "grade": "fail", "evidence": "The repo has 3 stars."},
    {"name": "recent_release", "grade": "fail", "evidence": "The releases list is empty."}
  ],
  "verdict": "reject"
}
```
---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. `agreement: 2/3 scored items`
2. `agreement: 1/1 scored items`
3. `agreement: 17/20 scored items  (bar: 18/20: below the bar)`
4. `agreement: 3/3 scored items`
5. `agreement: 20/20 scored items  (bar: 18/20: PASS)`


**Issue analysis**
issue-19. Gold label: `"id": "issue-19", "source": "zxcalc/zxlive#517", "category": "clear-accept", "calibration": false, "verdict": "accept", "note": "maintainer-diagnosed performance bug with named causes, unclaimed"`. Saved-run line: `issue-19  accept  accept   yes`. The rubric's decision is accept because `scope_bounded` says "A numbered list of causes or implementation ideas for one bug is not an umbrella," and the bundle's repo facts say `linked PRs: none`.


**Check rationale**

Quoted from `rubric.md`:
`| scope_bounded | Issue body and the Comments section | Pass unless one of these is true. (a) Umbrella: the issue says the work should be split into separate issues or PRs, or it is a list of other issues to pick from. A numbered list of causes or implementation ideas for one bug is not an umbrella. (b) Unsettled history: the issue was opened more than 2 years before the capture date AND at least 2 linked PRs are closed and unmerged. A "good first issue" or "help wanted" label does not override this. (c) A maintainer says the fix touches core internals. (d) Undecided feature: a feature request marks the asset, design, or result as TBD, or asks for a new capability without stating the specific behavior to build. A short body, a checklist, or a bug report without reproduction steps still passes when the requested behavior is specific, including a maintainer-filed bug that names its causes. | required |`
That wording exists because the previous pass condition accepted issue-15 and issue-20 and rejected issue-19. Clause (a) keeps one diagnosed bug, clause (b) rejects an issue open more than 2 years with at least 2 closed unmerged PRs, and clause (d) rejects a feature whose result is still TBD.


**Trade-offs**

The quoted check gives up issues with only one closed unmerged PR. issue-09 stays a gold accept with `linked PRs: conda/conda#11627 (closed)`, so the cutoff stays at two. The canary after the change was `agreement: 3/3 scored items` on `--only issue-15,issue-19,issue-20`. The committed file's last line is `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:


1. Issue 73 is a short docs fix, estimated at 1–2 hours on the issue, in `README.md` and `.env.example`. That fits the time I have better than a code change across the app.
2. The verdict correctly called it one specific docs change with no assignee and a `good first issue` label. It rejected the issue because PR #77 is already open. The rubric does not measure that about 30 classmates have already commented, which I weighed separately.
3. Claiming should be allowed, because other students' claim comments do not block a Path Review issue. The difficulty is the open pull request that already says it closes this issue.


---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
