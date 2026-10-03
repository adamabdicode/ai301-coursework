# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:
- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives: In an eval bundle, the environment lines of the candidate repro report, read against the version, OS, runtime, driver, or build named in the issue body. In live mode, the same lines in the draft repro comment, read against the issue body and the version the repo's own docs say to install.

What good looks like: The report names the tool or project version that was actually run and the OS or runtime it ran on. If that version or platform is not the one the issue targets, the report says so in the same place. "Latest", a log clock time, or a banner that only proves the program starts does not record an environment.

## Steps

Where it lives: In an eval bundle, the commands, inputs, config, and starting state in the candidate repro report, read against the steps in the issue body. In live mode, those same lines in the draft repro comment, read against the issue body. The repo's setup docs matter only for what a stranger would need to install; they do not replace the trigger.

What good looks like: Someone who does not have the author's machine can start from a public project, file, or command and hit the same trigger. The steps include a condition the issue says changes the result, such as the driver, the language, or the build profile. Steps that point at a private repo or an unshared config are not followable. A short report still passes when the exact trigger is written out.

## Behavior shown

Where it lives: In an eval bundle, the output excerpt, log, exit code, or other observation inside the candidate repro report, read against the actual behavior and the expected behavior in the issue body. In live mode, that observation in the draft repro comment, read against the issue body. A control or comparison, when the issue includes a working case, is the same kind of artifact.

What good looks like: The quoted output is the symptom the issue describes, such as the same missing header, the same error text, the same crash, or the same wrong value. An honest miss still shows an artifact: the output of the attempt, plus what differed from the issue. Output that only shows a healthy start, a different error, or a nearby command is not the issue's behavior.

## Honesty

Where it lives: In an eval bundle, the result sentence of the candidate repro report (the line that says reproduced, cannot-reproduce, root cause, crash, or fix), read against the artifact in that same report. The claim comment is a second place to look when it already asserts a result. In live mode, those sentences in the draft comments.

What good looks like: The words and the artifact agree. "Reproduced" is backed by the issue's symptom in the excerpt. "Could not reproduce" names what was observed and what differed, and does not claim a cause the run did not show. A labeled next step or hypothesis is fine. A root cause, a crash, or a guaranteed repro with no matching artifact is not.

## Comms

Where it lives: In an eval bundle, the candidate claim comment read against the issue title and the concrete symptom, command, version, or file in the issue body, and both comments read against the repo-facts contribution policy. In live mode, the draft claim and draft repro, read against the live issue body, the repo's contributing guide, and any AI-use policy the repo states.

What good looks like: The claim names a detail that belongs to this issue and says what the author will investigate or report next. It does not promise a fix, a date, or that the issue is reserved. For conventions, apply only the rule repo-facts actually states. When that policy says AI assistance must be disclosed, at least one comment discloses it. In an eval bundle, treat the candidate comments as AI-assisted work, so a required disclosure that never appears is a miss. When repo-facts states no AI policy, or allows AI without requiring disclosure, missing a disclosure sentence is not a miss.
