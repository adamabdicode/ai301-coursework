# Plan: verify_password returns False for an unrecognizable stored hash (#72)

## Diagnosis

`verify_password` passes the stored hash straight to `pwd_context.verify` and does not handle the error passlib raises when it cannot recognize the hash. The cause is that unhandled `UnknownHashError`, not the password comparison.

Repro evidence, from my posted report on issue 72: calling `verify_password("password", "not_a_valid_bcrypt_hash")` raises `passlib.exc.UnknownHashError: hash could not be identified`. The traceback ends in `core/security.py` line 37, `pwd_context.verify(...)`, which passlib raises from `identify_record`. `verify_password` does not catch it.

The same call under pytest is the xfail test:

```
.venv/bin/pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v -m unit --tb=short
```

```
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL [100%]
1 xfailed, 2 warnings in 0.91s
```

Control from that same report: `hash_password("password")` produced a hash starting `$2b$12$`, and `verify_password("other-password", that_hash)` returned `False` with no exception. A wrong password against a real bcrypt hash fails closed. A malformed stored hash does not. The trapped `AttributeError` (`bcrypt` has no `__about__`) printed while hashing that control did not change the result, and it is not the error the malformed hash raised.

## Scope

Will change: `verify_password` catches `passlib.exc.UnknownHashError` and returns `False`.

Will change: remove the `@pytest.mark.xfail(strict=True, ...)` marker on `test_verify_with_wrong_hash_format` (issue #72, manifest H-05). `docs/CONTRIBUTING.md` says a `strict=True` marker fails CI with `XPASS` once the test passes, and the issue itself says to remove the marker as part of the fix.

Will not change: `hash_password`, the bcrypt or passlib versions, the trapped `AttributeError` warning, `api/routes/auth.py` (its only caller already treats `False` as a failed login), or any broader exception handling. No bare `except Exception`.

## Files I'll touch

- `core/security.py` (`verify_password`)
- `tests/unit/test_security.py` (the xfail marker on `test_verify_with_wrong_hash_format`)

## Approach

1. Import `UnknownHashError` from `passlib.exc`.
2. Wrap the `pwd_context.verify` call in `try/except UnknownHashError` and return `False`.
3. Delete the `@pytest.mark.xfail` decorator on `test_verify_with_wrong_hash_format`. Leave the test body as it is: it already calls `verify_password("password", "not_a_valid_bcrypt_hash")` and asserts `False`.

## Test plan

Re-run the Unit 2 repro from the repo root.

Before, the command reports `1 xfailed`. After the marker is removed, the same command reports `1 passed`, and the direct call `verify_password("password", "not_a_valid_bcrypt_hash")` returns `False` instead of raising `UnknownHashError`.

Control, expected unchanged: `verify_password("other-password", <real $2b$12$ hash>)` still returns `False` with no exception.

## Risks and unknowns

- Unknown: whether a truncated `$2b$` hash raises a different exception, such as `ValueError`. The repro only covers the unrecognizable string `"not_a_valid_bcrypt_hash"`. That other input stays out of scope unless I observe it.
- I am not adding a log line when the hash cannot be identified. The issue asks for `False`.

## Deviations

The build followed this plan. `verify_password` catches `UnknownHashError` and returns `False`, and the `#72` xfail marker is gone. I did not change `hash_password`, the bcrypt warning, or `api/routes/auth.py`. The after run matches the test plan: the same pytest command reports `1 passed`, and the direct call returns `False`.
