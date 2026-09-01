# Examples — kept vs dropped

Read this file only when Pass B is unsure whether to keep or drop a candidate. Do not preload.

## Dropped (classic false positives)

### CSRF on one route; global middleware covers it

- **Signal:** Route handler has no CSRF call.
- **Why drop:** `middleware.ts` (or equivalent) already applies CSRF to the matcher. Check global layer first.

### XSS while final output escapes and unescapes only literals

- **Signal:** Intermediate `replace` looks unsafe.
- **Why drop:** Final step escapes `&<>`; `replaceAll` uses only fixed literal strings. Future hardening at most.

### "If in the future a caller could…"

- **Signal:** Speculative evolution.
- **Why drop:** Not broken today. Downgrade to hardening or drop.

### Dead code without consumer search

- **Signal:** Helper looks unused in the diff.
- **Why drop:** Alternate routes or raw-envelope paths may still call it. Verify all consumers; ask before delete.

### Style rename with no consistency win

- **Signal:** Prefer different synonym.
- **Why drop:** Preference without codebase inconsistency. Skip.

## Kept (true positives)

### `JSON.parse` on HTTP body without try/catch

- **Signal:** `JSON.parse(req.body)` (or equivalent) on user input.
- **Why keep:** Malformed body throws and can take down the worker. Provenance: user. Minimal fix: catch → 400.

### Sensitive route with no authz and no covering middleware

- **Signal:** Handler mutates privileged state; no auth check on route; global middleware does not match this path.
- **Why keep:** Concrete auth gap today. Point to the handler line and the middleware matcher that misses it.

## Stack examples

### TypeScript / JavaScript

#### Dropped — floating promise already handled

- **Signal:** `fetch(...)` without `await` in an async function.
- **Why drop:** Result is voided with `.catch(...)` / `void` + documented fire-and-forget, or the framework registers the promise. Confirm the error path before flagging.

#### Kept — `any` erases a typed boundary callers rely on

- **Signal:** `as any` / untyped param at a trust boundary; downstream assumes a narrowed shape.
- **Why keep:** Callers or later code treat the value as typed today; a wrong shape breaks or bypasses checks. Point to the cast and the consuming use.

### Go

#### Dropped — ignored error with justifying comment

- **Signal:** `_ = err` after a call.
- **Why drop:** Adjacent comment explains why the error is non-actionable (best-effort close, expected miss). Do not flag when the justification holds.

#### Kept — error rewrapped without `%w`

- **Signal:** `fmt.Errorf("...: %v", err)` or `%s` / `.Error()` on a returned error in this diff.
- **Why keep:** Callers using `errors.Is` / `errors.As` lose the chain today. Prefer `%w` (or documented sentinel break).

### Rust

#### Dropped — `unwrap` / `expect` in tests only

- **Signal:** `.unwrap()` in a `#[cfg(test)]` module or `*_test.rs` / `tests/`.
- **Why drop:** Test-only panic on bad fixture is normal. Do not treat as library API risk.

#### Kept — `unwrap` on a recoverable lib path

- **Signal:** `.unwrap()` / `.expect(...)` in non-test library code on I/O, parse, or user-driven `Result`/`Option`.
- **Why keep:** Recoverable failure becomes a panic today. Prefer `?` or explicit error mapping.

### Python

#### Dropped — style owned by the configured linter

- **Signal:** Import order, line length, or naming nit on `.py` files.
- **Why drop:** Project configures ruff/black/isort (or equivalent). Tool owns style unless the line is broken or unsafe today.

#### Kept — mutable default argument

- **Signal:** `def f(x, items=[])` (or `dict`/`set` default) mutated in the body.
- **Why keep:** Default is shared across calls; state leaks today. Use `None` + assign inside.

### Tests (Quality)

#### Dropped — mock of slow I/O, no assert on the mock

- **Signal:** Network/DB/startup mocked; assertion is on the real component's result.
- **Why drop:** Mock sits below the side effects the test needs. Structure is complete. The mock earns no assertion.

#### Dropped — no test on a trivial getter

- **Signal:** Diff adds a getter/reexport with no validate, default, or side effect.
- **Why drop:** Trivial code earns no test. Do not emit "missing tests".

#### Kept — mirror assertion

- **Signal:** `expect(fn(x)).toEqual(fn(x))` or both sides from the same builder/helper.
- **Why keep:** The assertion passes no matter what the code does. Use a literal or hand-checked fixture.

#### Kept — mock-as-SUT

- **Signal:** `expect(mock).toHaveBeenCalledTimes(n)` (or `*-mock` test id) while the real unit is not observed.
- **Why keep:** The test proves the double, not the component. Assert real behavior or drop the test.

#### Kept — getter-only test in the diff

- **Signal:** New test whose only assertion is a trivial getter/reexport.
- **Why keep:** Coverage theater. List as removable; ask before delete.
