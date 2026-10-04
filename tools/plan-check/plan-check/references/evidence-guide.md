# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

Where it lives: In an eval bundle, the cause sentence in the candidate plan, read against the repro-evidence block (the steps, the actual output, and any control run). The issue body is context for what the bug report claims. It does not outrank a control in the repro evidence. In live mode, the Diagnosis section of `plan.md`, read against the posted repro comment on the issue.

What good looks like: The stated cause names a mechanism that produces the symptom the repro output shows, and it still fits after each control. A control that succeeds without the blamed component, or that fails where the cause says the component is not involved, means the cause is not grounded. A cause copied from the thread that the repro's own controls contradict is not grounded.

## Scope

Where it lives: In an eval bundle, the in-scope and not-in-scope lines of the candidate plan (sometimes labeled Change, Scope, or Proposed changes), read against the single behavior the repro-evidence block isolates. In live mode, the Scope and Files sections of `plan.md`, read against the posted repro comment.

What good looks like: The in-scope list is the change that stops the reproduced symptom, plus the test that locks that symptom in. A larger idea that the plan explicitly puts out of scope is still bounded. A migration, a rewrite, a new option, or a second subsystem added to the in-scope list is not one bounded change, even when the small fix is also on the list.

## Executability

Where it lives: In an eval bundle, the files, functions, or areas named in the candidate plan, and the step that says what change will be made there. In live mode, the Files and Approach sections of `plan.md`.

What good looks like: A stranger can open the named file or function and make the chosen change without asking which layer to edit. Naming the file and the change is enough. A plan that offers two real options and does not pick one, or that says the work happens "somewhere", is not executable.

## Test plan

Where it lives: In an eval bundle, the test paragraph of the candidate plan, read against the steps and the actual output in the repro-evidence block. In live mode, the Test plan section of `plan.md`, read against the commands and output in the posted repro comment.

What good looks like: The test runs the reproduced case again and names the observable result that replaces the symptom, such as an exit code, a returned value, a color, or the error no longer being raised. "The suite passes" or "it should feel faster", with no result for the reproduced case, does not decide anything.

## Honesty

Where it lives: In an eval bundle, the risk or unknown sentences in the candidate plan, read against what the repro-evidence block actually measured. In live mode, the Risks and unknowns section and the Deviations section of `plan.md`. A deviation recorded after the build is part of the plan.

What good looks like: An unknown stays worded as unknown. A stated cost, an untested input, or a caller behavior is not written as a measured fact unless the repro evidence shows it. Leaving the risks section out is not the same as dressing an unknown up as certainty.

## Comms

Where it lives: In an eval bundle, the candidate plan comment, read against the thread highlights and against the contribution-policy line in the repo-facts block. In live mode, `comment.md`, read against the live issue thread and against `docs/CONTRIBUTING.md` in the Path Review repo, including any AI-use rule that file actually states.

What good looks like: When a maintainer has named a culprit file, posted a patch and asked for a test, agreed a fix, or rejected an approach, the plan comment refers to that direction. When the highlights have no such direction, the comment does not need one. On disclosure, apply only the rule repo-facts states. When that policy requires AI assistance to be disclosed, the plan comment discloses it. In an eval bundle the plan comment is AI-assisted work, so a required disclosure that never appears is a miss. When repo-facts states no such requirement, or asks for disclosure only on the pull request, a comment with no disclosure sentence is fine.
