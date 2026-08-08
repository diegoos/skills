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
