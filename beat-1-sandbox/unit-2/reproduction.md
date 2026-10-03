# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

adamabdicode

---

## Posted upstream


**Claim comment**


https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5971399015

I'd like to investigate this as a first contribution. The issue reports that `verify_password` in `core/security.py` lets passlib's `UnknownHashError` escape when the stored hash is not a recognizable format, and that verification against a malformed hash should return `False` instead of raising. Next I will set the project up from `docs/SETUP.md`, run the xfail test in `tests/unit/test_security.py` (manifest id H-05) against a malformed stored hash, and report what I observe, including a cannot-reproduce if that is what happens.


**Reproduction comment**
Reproduced on my fork of pathreview-ai301-fa26-s1, commit checked out from main today. I did not change any code.

Environment: Python 3.12.3 (docs/SETUP.md asks for 3.11 or newer), passlib 1.7.4, bcrypt 4.3.0, pytest 9.1.1, Linux 7.0.0-28-generic x86_64. Setup was the venv portion of make setup: cp .env.example .env, python3 -m venv .venv, then .venv/bin/pip install -e ".[dev]". I did not start Docker. This bug is the unit test named in the issue, and that test does not need Postgres.

Steps, from the repo root:

.venv/bin/pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v -m unit --tb=short

The test calls verify_password("password", "not_a_valid_bcrypt_hash") and expects False. It is marked @pytest.mark.xfail for issue #72, manifest H-05, so pytest reports the failure as expected:

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL [100%]
1 xfailed, 2 warnings in 0.91s

The same call outside pytest shows the exception. From the repo root, .venv/bin/python:

from core.security import verify_password
verify_password("password", "not_a_valid_bcrypt_hash")

passlib.exc.UnknownHashError: hash could not be identified

The traceback ends in core/security.py line 37, pwd_context.verify(...), which passlib raises from identify_record when it cannot recognize the stored hash. verify_password does not catch it.

Control: hash_password("password") produced a hash starting $2b$12$, and verify_password("other-password", that_hash) returned False with no exception. A wrong password against a real bcrypt hash fails closed. A malformed stored hash does not.

Expected, per the issue: verify_password returns False for "not_a_valid_bcrypt_hash".
Actual: it raises passlib.exc.UnknownHashError: hash could not be identified.

While hashing the control password, passlib printed a trapped AttributeError (bcrypt has no __about__). That warning did not change the control result, and it is not the error the malformed hash raised.

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5971579038

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

One full run, before --save-run: 20/20, and every category matched (clear-accept 8/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4). Nothing disagreed with the gold labels, so there was no --only re-run.
One confirming full run with --save-run: 20/20. That is the agreement line in eval-run.txt.

**Package analysis**

pkg-20. The gold label is reject. My rubric also returned reject. The report itself had an environment, followable steps, and an output that matched the issue, so the proof checks passed. The only failed check was conventions. The repo-facts block says all AI use must be disclosed, and neither comment discloses it. Eval comments are treated as AI-assisted, so silence fails that check, and a failed required check rejects the package.


**Check rationale**

| conventions | The repo-facts contribution policy, including any AI-use rule, read against the claim comment and the repro report. See evidence-guide Comms. | Pass when the comments satisfy the policy that is actually stated. If repo-facts requires contributors to disclose AI assistance, at least one comment must disclose it; in an eval bundle, treat the candidate comments as AI-assisted work, so silence is a fail. If repo-facts has no AI policy, or the policy allows AI without requiring disclosure (including "you are responsible for understanding the work" or "comments must be written in your own words"), this check passes. Fail only for a stated disclosure requirement that neither comment meets. | required |

**Trade-offs**

conventions gives up catching a comment that is rude or generic. Those failures belong to claim-specific. It also gives up failing every package that never mentions AI. Only a stated disclosure rule can fail it, so a permissive policy is not punished for silence. comparison-noted is preferred, so a missing control run cannot reject a package that is otherwise proven. Nothing was loosened after the first full run, and the confirming run scored 20/20 on the same files, which is how I know that choice did not flip a package that had already agreed.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
