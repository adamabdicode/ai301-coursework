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
| env-recorded | The environment facts in the repro report (version, OS, runtime, driver, or build), read against the issue body. See evidence-guide Environment. | Pass when the report names the tool or project version that was run and the OS or runtime it ran on. Also pass when an evidenced cannot-reproduce names those same facts. Fail when a stranger cannot tell what was run: no version and no OS or runtime. A log timestamp, a version banner that only shows the program starts, or "latest" with no version is not a record. | required |
| target-faithful | The version, platform, and trigger in the repro report, read against the version, platform, and trigger in the issue body. See evidence-guide Environment and Steps. | Pass when the attempt targets the behavior the issue describes: the named version or platform matches the issue, or the report explicitly says how it differs, and the steps use the issue's trigger rather than a nearby command, expression, flag, or input. Fail on a silent mismatch, such as an older version than the issue's confirmed range with no mention of the gap, or steps that run a different syntax than the one the issue reports. | required |
| steps-rerunnable | The reproduction steps in the repro report, from the starting state through the trigger, read against the issue's steps. See evidence-guide Steps. | Pass when a stranger can reach the same trigger from a public starting state using the commands, inputs, or config written in the report. Fail when the steps depend on a private repo, an unshared config, or a machine-only file, or when they omit a condition the issue itself says changes the result (for example the driver, the language, or the build profile). Do not fail a short report that still contains the exact trigger. | required |
| behavior-matches | The output excerpt, log, screenshot description, or other observation in the repro report, read against the actual and expected behavior in the issue body. See evidence-guide Behavior shown. | Pass when the artifact shows the issue's symptom (the same error, missing field, crash, wrong value, or repeated action), or when the report says the symptom did not occur and the artifact shows the outcome that did occur. Fail when there is no observation of what happened, when the artifact shows only that the program runs, or when the artifact is a different symptom (a different error, a successful unrelated run, a syntax error instead of the reported panic) while the report treats the issue's bug as shown. | required |
| honest-outcome | The result sentence in the repro report (reproduced, cannot-reproduce, root cause, crash, or fix), read against the artifact in that same report. See evidence-guide Honesty. | Pass when the stated result matches the artifact. An evidenced cannot-reproduce passes when it names what was observed and what differed from the issue. Fail when the report asserts a reproduction, a crash, a root cause, or a fix that the artifact does not show, including a confident "reproduced" whose excerpt is a different error or only a healthy run. | required |
| claim-specific | The candidate claim comment, read against the issue title and the concrete symptom, command, version, or file in the issue body. See evidence-guide Comms. | Pass when the claim names a concrete detail of this issue and states what the author will investigate or report next. Fail when the claim is a generic +1, a me-too, or assign-me boilerplate that could sit on any issue, or when it promises a fix, a date, or that the issue will be reserved. Promising to look and report back passes. | required |
| conventions | The repo-facts contribution policy, including any AI-use rule, read against the claim comment and the repro report. See evidence-guide Comms. | Pass when the comments satisfy the policy that is actually stated. If repo-facts requires contributors to disclose AI assistance, at least one comment must disclose it; in an eval bundle, treat the candidate comments as AI-assisted work, so silence is a fail. If repo-facts has no AI policy, or the policy allows AI without requiring disclosure (including "you are responsible for understanding the work" or "comments must be written in your own words"), this check passes. Fail only for a stated disclosure requirement that neither comment meets. | required |
| comparison-noted | A control or comparison run in the repro report, when the issue body itself includes a working case beside the failing one. See evidence-guide Behavior shown. | Pass when the report notes what the working case did, or when the issue has no such comparison. A missing comparison never blocks posting. | preferred |

## Verdict rule

Accept only when every `required` check passes. A `preferred` check never changes the verdict, whether it passes or fails. `unclear` on a required check counts as fail, because proof that cannot be verified is not ready to post.

On a claim-only draft, grade `env-recorded`, `target-faithful`, `steps-rerunnable`, `behavior-matches`, `honest-outcome`, and `comparison-noted` as `unclear` with evidence `not yet applicable: claim-only draft`, and leave those checks out of this rule. The claim-only verdict is accept only when every remaining required check (`claim-specific` and `conventions`) passes.
