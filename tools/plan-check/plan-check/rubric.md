# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| cause-grounded | The plan's stated cause, read against the repro evidence, including every control run. See evidence-guide Diagnosis and grounding. | Pass when the stated cause explains the behavior the repro evidence actually shows, and every control in that evidence is consistent with the cause. Fail when a control rules the cause out: the symptom appears in a run where the blamed component is not involved, or a working control uses the component the plan blames. Also fail when the plan ignores the repro and adopts a different theory, including one the thread states confidently. A terse cause passes when it names the mechanism the repro isolates. | required |
| scope-bounded | The plan's in-scope changes and its not-in-scope line, read against the behavior the repro evidence isolates. See evidence-guide Scope. | Pass when every in-scope change is required to fix that behavior or to lock it in with a test, and any larger idea is explicitly left out. Updating or un-xfailing the test that covers this bug is part of the fix. Fail when in-scope work adds a migration, a subsystem rewrite, a new user-facing option, a new cross-cutting abstraction, or several fronts the repro does not require, even if a correct small fix is also listed. Discussing a deferred idea does not fail. | required |
| executable | The files or areas and the chosen change in the plan. See evidence-guide Executability. | Pass when a stranger can start from a named file, function, or area and one chosen change, without the author still picking the layer. A terse plan that names both passes. An open question about the exact line, inside a named file and a chosen change, passes. Fail when the plan names no file or area, or leaves the real decision open ("somewhere", "not sure which layer", "upstream or vendored, whichever is easier", "optimize whatever profiling finds"). | required |
| test-decisive | The plan's test, read against the repro evidence's steps and the symptom those steps produced. See evidence-guide Test plan. | Pass when the test re-runs the reproduced case, or the issue's failing input, and states an observable result for that case: an exit code, a returned value, a rendered change, an assertion, or the absence of the reproduced error. A control that must stay unchanged counts. Fail when success is only a feeling ("feel fast", "feel broken", "should work") or only a whole-suite or overnight run with no result named for the reproduced case. | required |
| thread-and-conventions | The plan comment, read against the thread highlights and against the repo-facts contribution policy, including any AI-use rule. See evidence-guide Comms. | Pass only when both parts pass. Thread: if the highlights contain an explicit maintainer direction (a named culprit file or function, a posted patch with a request to test it, an agreed fix, or a rejected approach), the plan comment refers to that direction. If the highlights contain no such direction, the thread part passes. A comment that proposes other work and never mentions the direction fails. Disclosure: pass when the comment satisfies the policy that is actually stated. If repo-facts requires contributors to disclose AI assistance, the plan comment must disclose it; in an eval bundle, treat the plan comment as AI-assisted work, so silence is a fail. If repo-facts has no AI policy, or the policy allows AI without requiring disclosure (including "you are responsible for understanding the work", "comments must be written in your own words", or a disclosure ask that applies to the pull request and not to issue comments), this part passes. Fail the disclosure part only for a stated disclosure requirement the plan comment does not meet. | required |
| unknowns-honest | The plan's risks and unknowns, read against the repro evidence. See evidence-guide Honesty. | Pass when the plan does not state an unmeasured cost, an untested input class, or a caller dependency as settled fact. A plan that simply has no risks section passes. Fail when the plan asserts a measurement or an edge-case result the repro evidence does not show. | preferred |

## Verdict rule

Accept only when every `required` check passes. A `preferred` check never changes the verdict, whether it passes, fails, or is `unclear`. `unclear` on a required check counts as fail: a plan you cannot verify from the package is not ready to build from.
