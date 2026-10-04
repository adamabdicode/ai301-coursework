# Voice guide: how I talk upstream

<!--
Carried forward from week 2, then extended for the plan-comment
register. The week-2 rules still apply. The added rule covers a plan
comment, which commits to an approach.
-->

## Who I am in threads

I am a student making a first contribution to this repo. I am new to the codebase, and I am here to investigate one issue and report what I actually ran. Readers can expect a claim that names this bug, then a report of the environment, the steps, and the output, including a clear cannot-reproduce when that is what happened. A plan comment is the next thing they can expect: the change I will make, tied to that report.

## Rules I write by

### Rule: promise the investigation

A claim says what I will look into and that I will report back. It never promises a fix, a pull request date, or that the issue is mine. A plan comment is allowed to name the change I will make. It still never promises a date or that the issue is reserved.

- Wrong: "Kindly assign this to me. I will fix it within 2 days guaranteed."
- Right: "I can reproduce the missing Content-Type on 3.2.4 with one custom header. Next I will read apply_missing_repeated_headers() and report what I find."

### Rule: name this issue

The first comment has to mention a detail that exists only on this issue: the error text, the command, the version, or the file. A greeting that could be pasted onto any issue is not a claim.

- Wrong: "Great project, I love this repo and this issue looks like a good one for me."
- Right: "I am looking into the FES TypeError when the browser language is Japanese first and the sketch uses the reserved name value."

### Rule: claim only the run

I state a result only when the report shows that result. If I could not reproduce the bug, I say that, and I say what I did see.

- Wrong: "Confirmed, this crash is guaranteed reproducible. The root cause is a debounce race."
- Right: "I could not reproduce the reorder. Every run wrote all ONE batches before any TWO. My ARG_MAX is 2097152 and the filenames were uniform length, which may be why."

### Rule: write the proof myself

On a shared issue I still post my own environment, steps, and output. I do not point at someone else's comment and call that my reproduction. I also do not point at someone else's plan and call that mine.

- Wrong: "Same as above, I can confirm."
- Right: "On ghostty 1.3.1 (Fedora 42 RPM, GTK, Wayland) the single-theme config returned CSI ? 997 ; 2 n. The conditional theme returned 997 ; 1 n. Commands are below."

### Rule: disclose when the repo requires it

If the repo's contributing guide says AI assistance must be disclosed, the comment says that I used a tool, what it helped with, and that I ran the steps myself. If the repo does not require disclosure, I do not add a disclosure paragraph for its own sake.

- Wrong: "Here is my reproduction." (posted on a repo whose policy says all AI use must be disclosed, with no mention of the assistant)
- Right: "I used an AI assistant to help me organize this report. I ran every step on ghostty 1.3.1 myself and I understand the output below."

### Rule: state the approach, not a date

A plan comment names the change I will make and the file, and it points at my own repro. It does not promise when the pull request will land, and it does not say "same approach as above."

- Wrong: "Same approach as above. PR by Friday."
- Right: "On the repro, verify_password(\"password\", \"not_a_valid_bcrypt_hash\") raises UnknownHashError from core/security.py line 37. I will catch that error in verify_password and return False, and I will remove the #72 xfail marker so the existing test locks the result in."

## Things I never post

- A promise to open the PR by a date, or to finish in a number of days.
- "Assign this to me" or "please keep this issue reserved."
- "Same as above", "same approach as above", or "+1" with no environment, steps, or output.
- "Guaranteed reproducible", a root cause, or a crash, unless the output in the same comment shows that.
- A reproduction I did not run, including a cannot-reproduce written as if I had produced the bug.
- A disclosure paragraph on a repo whose contributing guide does not require one.
