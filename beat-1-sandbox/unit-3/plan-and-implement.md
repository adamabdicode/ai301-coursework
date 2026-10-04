# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

adamabdicode

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5982735975

Reproduced on my fork, in my posted reproduction on this issue: `verify_password("password", "not_a_valid_bcrypt_hash")` raises `passlib.exc.UnknownHashError: hash could not be identified` from `core/security.py` line 37, `pwd_context.verify(...)`. The xfail test `test_verify_with_wrong_hash_format` reports `XFAIL`. A wrong password against a real `$2b$12$` hash returns `False` with no exception, so only the malformed stored hash raises.

Plan: catch `UnknownHashError` in `verify_password` and return `False`. I will also remove the `#72` `@pytest.mark.xfail(strict=True)` marker on that test. `docs/CONTRIBUTING.md` says leaving a `strict=True` marker fails CI with `XPASS` once the test passes, and the issue says to remove it as part of the fix. I will not change `hash_password`, the bcrypt warning, or `api/routes/auth.py`.

A truncated `$2b$` hash is untested on my run, so I am not catching anything broader than `UnknownHashError`.

---

## Your branch

**Branch**

fix/72-unknown-hash-returns-false

**Evidence**

Before, from the Unit 2 reproduction on issue #72. Command, from the repo root:

.venv/bin/pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v -m unit --tb=short

Output:

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL [100%]
1 xfailed, 2 warnings in 0.91s

The same call outside pytest:

from core.security import verify_password
verify_password("password", "not_a_valid_bcrypt_hash")

passlib.exc.UnknownHashError: hash could not be identified

After the fix, the same pytest command:

.venv/bin/pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v -m unit --tb=short

Output:

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED [100%]

======================== 1 passed, 2 warnings in 0.48s =========================

Direct call after the fix:

from core.security import verify_password
print(verify_password("password", "not_a_valid_bcrypt_hash"))

False

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

One full run, with `--save-run eval-run.txt`: 20/20. That is the agreement line in `eval-run.txt`: `agreement: 20/20 scored items  (bar: 18/20: PASS)`. No earlier run and no `--only` re-run.

**Package analysis**

pkg-20. The gold label is reject. My rubric also returned reject. The candidate plan is bounded and follows the thread: it recomputes `prev` only when page capacity changes, names the files, and the test plan says both fuzz cases pass with the control unchanged. The only failed required check was `thread-and-conventions`. The repo-facts block says all AI usage must be disclosed, stating the tool and the extent of the assistance. The plan comment does not disclose it. Eval comments are treated as AI-assisted, so silence fails that check, and a failed required check rejects the package.

**Check rationale**

| thread-and-conventions | The plan comment, read against the thread highlights and against the repo-facts contribution policy, including any AI-use rule. See evidence-guide Comms. | Pass only when both parts pass. Thread: if the highlights contain an explicit maintainer direction (a named culprit file or function, a posted patch with a request to test it, an agreed fix, or a rejected approach), the plan comment refers to that direction. If the highlights contain no such direction, the thread part passes. A comment that proposes other work and never mentions the direction fails. Disclosure: pass when the comment satisfies the policy that is actually stated. If repo-facts requires contributors to disclose AI assistance, the plan comment must disclose it; in an eval bundle, treat the plan comment as AI-assisted work, so silence is a fail. If repo-facts has no AI policy, or the policy allows AI without requiring disclosure (including "you are responsible for understanding the work", "comments must be written in your own words", or a disclosure ask that applies to the pull request and not to issue comments), this part passes. Fail the disclosure part only for a stated disclosure requirement the plan comment does not meet. | required |

I rejected a disclosure-only check. That would catch pkg-20 and miss pkg-04, whose repo-facts block has no AI policy and whose comment ignores the owner's named culprit, `src/tui/light_windows.go`, and the patched binary the owner asked to be tested. I also rejected failing every comment that never mentions AI. A policy that only says the author must understand the work, or that asks for disclosure on the pull request and not on the issue comment, is a pass.

**Trade-offs**

`thread-and-conventions` gives up catching a comment that is rude or generic when the thread has no explicit maintainer direction and the repo does not require disclosure. It also gives up failing a package that never mentions AI unless repo-facts states a disclosure requirement. Nothing was loosened after the run. The one full run scored 20/20, including `thread-convention 2/2` (pkg-04 and pkg-20), which is how I know that choice did not flip a package.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
