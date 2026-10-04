# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. In live mode, read `scope.md` first and confirm the issue is inside the scoped repo. Note the house rules. If the `Repo:` line is still a placeholder, stop without grading. In eval mode, skip `scope.md`.
2. Read `rubric.md` and list every check name, the evidence it names, its pass condition, and its weight. Read the verdict rule, including how `unclear` is treated.
3. Read `references/evidence-guide.md` and keep its "where it lives" lines next to the matching checks.
4. Read the package in this order, before grading any check: the issue context, then the repo-facts block, then the thread highlights, then the repro evidence (steps, output, and controls), then the candidate plan, then the plan comment. In live mode the same order uses the live issue, the repo's contributing docs, the live thread, the posted repro comment, then `plan.md`, then `comment.md`.
5. While reading the repro evidence, write down the behavior it pins: the symptom, the control results, and what those controls rule out. Do this before reading the plan's cause, so the thread's theory cannot replace the repro.

## Evidence gathering

1. Diagnosis: from the repro evidence, record the symptom and each control result. From the plan, record the stated cause in one sentence. The pair is the evidence for `cause-grounded`.
2. Scope: from the plan, list the changes it will make and the changes it says it will not make. From the repro, record the one behavior those changes have to affect. That pair is the evidence for `scope-bounded`.
3. Executability: from the plan, record the file, function, or area named and the change it chooses. If it offers alternatives and does not choose, record the alternatives. That note is the evidence for `executable`.
4. Test plan: from the plan, record the command, input, or case it will re-run and the result it expects. From the repro evidence, record the steps and the symptom. That pair is the evidence for `test-decisive`.
5. Honesty: from the plan, record any cost, input class, or caller claim stated as fact. Compare each to the repro evidence. A missing risks section is recorded as "no risks section", which the preferred check allows. That note is the evidence for `unknowns-honest`.
6. Comms: from the thread highlights, record any explicit maintainer direction (a named culprit, a posted patch with a test request, an agreed fix, or a rejected approach). Record "none" when there is no such direction. From repo-facts, copy the contribution policy sentence that mentions AI, or record "no AI disclosure requirement" when the policy does not require disclosure in an issue comment. From the plan comment, record whether it refers to the direction and whether it discloses AI use. That trio is the evidence for `thread-and-conventions`.
7. In live mode, gather issue-side facts from GitHub and the repo docs at the locations the evidence guide names. The drafts are the candidate side. In eval mode, quote from the bundle only. Do not fetch anything.

## Check execution

1. Grade the checks in this order: `cause-grounded`, `scope-bounded`, `executable`, `test-decisive`, `unknowns-honest`, `thread-and-conventions`. The cause is graded from the notes in Evidence gathering, not from a fresh read of the thread.
2. For each check, apply that row's pass condition to the gathered note. Grade `pass` or `fail`. Attach one line of evidence: a quote or a fact from the note, not a description of the writing.
3. Grade `unclear` only when the evidence the check names is absent from the package. Not looking is not `unclear`. A missing risks section is not `unclear` for `unknowns-honest`; the pass condition says that case passes.
4. Do not re-read the whole package for a later check. Use the gathered notes. Re-open the bundle only to copy a quote for the evidence line.
5. In live mode, after the checks, hold `comment.md` against `voice-guide.md` and note any broken rule. Voice notes do not change a check grade. In eval mode, ignore `voice-guide.md`.

## Verdict assembly

1. Apply the verdict rule in `rubric.md`. Accept only when every required check is `pass`. A `preferred` check never changes the verdict. `unclear` on a required check counts as fail.
2. In the summary, quote the evidence line of the check that decided a reject. On an accept, quote the evidence line for `cause-grounded`.
3. Emit the fenced JSON block last, with one object per check in the order above, then nothing after the block.
