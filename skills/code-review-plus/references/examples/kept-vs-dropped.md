# Examples — kept vs dropped

Pass B reads this file (`./references/phases/verify.md` says when). Do not preload.

## Contents

- [Dropped (classic false positives)](#dropped-classic-false-positives)
- [Kept (true positives)](#kept-true-positives)
- [Security precedents](#security-precedents)
- [Stack examples](#stack-examples)

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

### Dropped — same behavior and Match; reviewer would have written it differently

- **Signal:** Alternative structure the reviewer prefers; neighbor and Floor already hold; no load cost.
- **Why drop:** Preference. Not a finding.

## Kept (true positives)

### `JSON.parse` on HTTP body without try/catch

- **Signal:** `JSON.parse(req.body)` (or equivalent) on user input.
- **Why keep:** Malformed body throws and can take down the worker. Provenance: user. Minimal fix: catch → 400.

### Sensitive route with no authz and no covering middleware

- **Signal:** Handler mutates privileged state; no auth check on route; global middleware does not match this path.
- **Why keep:** Concrete auth gap today. Point to the handler line and the middleware matcher that misses it.

### Authenticated lookup by id without owner or tenant scope

- **Signal:** Route requires login, then loads a record by the id from the request and returns or mutates it.
- **Why keep:** Any user reads or changes another tenant's record today (IDOR). Fix: scope the query by owner or tenant; return 403/404.

### `catch` around a permission check that grants access

- **Signal:** Permission lookup throws or times out; the `catch` continues or returns allow.
- **Why keep:** Reachable error path plus privilege gain (fail-open). Fix: deny on any authorization failure.

### Tool authorization only in the system prompt

- **Signal:** Prompt says "do not call admin tools"; the server runs the tool with service credentials and no per-user check.
- **Why keep:** Untrusted content steers the model to an action the caller cannot take through the normal API. Fix: authorize each tool call in server code for the caller.

## Security precedents

| Pattern                                                                       | Verdict                                                            |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| DoS, resource exhaustion, missing rate limit, memory or FD leak               | Drop                                                               |
| Missing headers, CSP, or non-session cookie flags; no exploit path            | Hardening at most                                                  |
| Outdated dependency or advisory                                               | `./references/dependency-review.md` owns it                        |
| Attack needs control of env vars, CLI flags, or deploy config                 | Drop                                                               |
| Attack needs guessing a UUID or other random id                               | Drop                                                               |
| XSS in React/JSX with no `dangerouslySetInnerHTML` or other raw sink          | Drop                                                               |
| Missing authz, SSRF, or path traversal in browser-only code                   | Drop; the server enforces                                          |
| Open redirect, tabnabbing, XS-Leaks, prototype pollution                      | Drop unless it leaks a token or session                            |
| Logging non-secret, non-PII data; log spoofing                                | Drop. Secrets, tokens, request headers, or PII in logs: keep       |
| Theoretical race or timing attack                                             | Drop unless the interleaving and the gain are concrete             |
| Command injection in a shell script or CI workflow                            | Keep only with a concrete path for untrusted input                 |
| TypeScript types treated as runtime validation                                | Not a control; keep the finding when no runtime check exists       |
| Helper named `auth()` treated as authorization                                | AuthN is not AuthZ; require owner or tenant proof at the data line |

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

### Complexity / YAGNI / Match

#### Dropped — extract helper only to lower a complexity score

- **Signal:** Hunter proposes splitting a readable function because CC is 12 (or the linter said so).
- **Why drop:** CC ≤ 20 Floor; no nesting ≥3 and no third use. A score move without a responsibility name is gaming. Keep the function unless a reader is slower today.

#### Dropped — Go `if err != nil` series as complexity

- **Signal:** Function CC is high; most branches are `if err != nil { return err }`.
- **Why drop:** Explicit error paths inflate CC. They are not nested jungle. Inspect remaining business branches only.

#### Kept — new or rewritten function with CC > 20

- **Signal:** Diff adds or substantially rewrites a function; CC is above the Floor cap (20) with no project bar, or above the project's configured bar.
- **Why keep:** Maintainability today. Suggested fix: local split, table, or tests — not a wholesale rewrite. Cite the counted score in the finding body.

#### Kept — new function with nesting ≥3

- **Signal:** Diff adds (or substantially rewrites) a function; control structures nest three or more levels; a reader cannot state the happy path without simulating the tree.
- **Why keep:** Readability today. Suggested fix: guard clauses or extract the inner block with a name that states the responsibility. Cite CC in the finding body if counted; the keep reason is the nesting.

#### Kept — plugin / strategy with one implementer

- **Signal:** Diff adds an interface, factory, or provider enum with a single live implementation and no second caller or shipped contract.
- **Why keep:** YAGNI. Carry starts now. Suggested fix: call the concrete type. P2 for a type tree; P3 for a dead field.

#### Kept — Match miss vs neighbor of the same kind

- **Signal:** New helper names errors or imports unlike the neighbor of the same kind; a reader must learn a second pattern in this slice.
- **Why keep:** Match cost today. Suggested fix: follow the neighbor. P2/P3 maintainability.
