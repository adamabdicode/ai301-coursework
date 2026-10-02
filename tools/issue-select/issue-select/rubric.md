# Rubric: is this a good first issue?

All recency thresholds are measured against the capture date shown in the repo-facts block (eval mode) or against today (live mode).

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer_commits | Repo facts: "last 5 default-branch commits" (dates and authors) | At least 1 of the 5 commits is dated within 90 days of the capture date AND was authored by a human, or is a bot commit that merged a human's pull request. All 5 older than 90 days, or all 5 plain bot commits, fails. | required |
| maintainer_response | Repo facts: "maintainer first-response sample"; Comments section author_association values | The sample shows at least 1 first reply from an Owner, Member, or Collaborator that arrived within 60 days of that issue being opened. An empty or missing sample is unclear. | preferred |
| repo_in_use | Repo facts: "archived:" on the repo line and "last push to any branch" | The repo is not archived AND the last push to any branch is within 180 days of the capture date. | required |
| scope_bounded | Issue body and the Comments section | Pass unless one of these is true. (a) Umbrella: the issue says the work should be split into separate issues or PRs, or it is a list of other issues to pick from. A numbered list of causes or implementation ideas for one bug is not an umbrella. (b) Unsettled history: the issue was opened more than 2 years before the capture date AND at least 2 linked PRs are closed and unmerged. A "good first issue" or "help wanted" label does not override this. (c) A maintainer says the fix touches core internals. (d) Undecided feature: a feature request marks the asset, design, or result as TBD, or asks for a new capability without stating the specific behavior to build. A short body, a checklist, or a bug report without reproduction steps still passes when the requested behavior is specific, including a maintainer-filed bug that names its causes. | required |
| is_contribution | Issue title and body | The issue asks for a change to code, docs, tests, or configuration. A pure usage question ("how do I get this to work?") fails. | required |
| no_abandoned_attempts | Repo facts: "linked PRs:" with state per PR, plus any PRs mentioned in the Comments section | Fewer than 3 closed-and-unmerged PRs are linked or mentioned as attempts at this issue. | required |
| no_assignee | Repo facts: "this issue: assignees:" | The assignees list is empty. | required |
| no_active_pr | Repo facts: "linked PRs:" with state per PR, plus any PRs mentioned in the Comments section | No linked PR is open, and no comment mentions an open PR working on this issue. If the linked-PR list and the thread disagree, believe the thread. | required |
| no_live_claim | The Comments section: claim phrases such as "I'll take this", "can I work on this", "working on this", with comment dates | No claim comment is dated within 60 days of the capture date, unless the claimant later withdrew or a maintainer said the issue is still open. A claim older than 60 days with no PR and no later activity from the claimant is stale and passes. | required |
| ai_policy_allows | Repo facts: "contribution policy" line (CONTRIBUTING.md, AI policy files, templates) | The line does not state an outright ban on AI-generated contributions. Conditions (disclose AI use, personally test, human review) pass. A missing or empty policy line passes. | required |
| newcomer_label | Issue labels | The issue carries the "good first issue" or "help wanted" label. | preferred |
| maintainer_in_thread | The Comments section: author_association of each commenter | At least 1 comment in this thread is from an Owner, Member, or Collaborator. | preferred |
| adoption_scale | Repo facts: stars on the repo line | The repo has at least 100 stars. | preferred |
| recent_release | Repo facts: "latest release" | The latest release is dated within 365 days of the capture date. | preferred |

## Verdict rule

Accept if every required check passes. Reject if any required check fails. A required check graded `unclear` counts as fail, with two exceptions: a missing or empty contribution-policy line passes (silence is not a restriction), and a "linked PRs:" list showing none passes. `unclear` means the evidence needed to apply the check is absent or ambiguous; finding nothing that looks like a claim, an assignee, or an open PR is a pass, not unclear. Preferred checks never change the verdict. Among accepted issues, rank by the number of preferred checks passed, most first.
