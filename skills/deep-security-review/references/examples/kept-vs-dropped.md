# Examples — kept vs dropped

Read this file only when Phase 3 is unsure whether to keep or drop a candidate. Do not preload. Do not give this file to hunters.

## Dropped (classic false positives)

### Auth missing on a route; global middleware covers it

- **Signal:** Handler has no `requireAuth` call.
- **Why drop:** Middleware matcher already applies AuthN/AuthZ to the path. Check the global layer first.

### CSRF "missing" on one POST

- **Signal:** Route has no CSRF helper.
- **Why drop:** Framework CSRF middleware or `SameSite=strict` session cookies already cover the matcher. Verify the real strategy.

### XSS while the final encoder escapes and only literal unescape remains

- **Signal:** Intermediate string replace looks unsafe.
- **Why drop:** Final HTML/attribute encoder escapes `&<>`; `replaceAll` uses only fixed literals. Hardening at most.

### Mass assignment; schema already strips privileged fields

- **Signal:** Body includes `role` / `isAdmin`.
- **Why drop:** Runtime schema rejects/strips unknown or privileged keys before persistence. Confirm the field never reaches the write.

### SSRF; URL is constant or allowlisted after redirects

- **Signal:** Server fetches a URL-shaped field.
- **Why drop:** Host allowlist re-checked after DNS + redirects; private/metadata blocked. Keep only with rebind/TOCTOU or missing post-redirect check.

### Dependency CVE without a reachable call path

- **Signal:** Advisory on a transitive package.
- **Why drop:** Not imported on the prod path, or only a `devDependency`. Route to process/gap unless reachability is shown.

### "If a future caller skips the guard…"

- **Signal:** Speculative evolution.
- **Why drop:** Not exploitable today. Downgrade to hardening or drop.

### Incomplete CSP / missing HSTS with no exploit path

- **Signal:** Header inventory gap.
- **Why drop:** Hardening note — not a kept vulnerability without a concrete browser exploit path.

## Kept (true positives)

### IDOR — `findUnique({ id })` then return without ownership

- **Signal:** Authenticated user supplies another tenant's id.
- **Why keep:** Proven cross-tenant read/write today. Fix: scope by `tenantId`/`ownerId`; add 403/404 test.

### AuthZ fail-open on error

- **Signal:** `catch` around permission lookup grants access or continues.
- **Why keep:** Reachable error path + privilege gain. Fix: deny on AuthZ failure.

### JWT decode without verify / `alg` confusion

- **Signal:** Library accepts `none` or unverified payload claims drive AuthZ.
- **Why keep:** Attacker forges identity. Fix: pin algorithms; verify signature before trust.

### SSRF with redirect to metadata after allowlist check

- **Signal:** Allowlist checked on pre-redirect URL only.
- **Why keep:** TOCTOU/rebind path to `169.254.169.254` or private ranges. Fix: re-resolve after redirects; block link-local/private.

### Prompt-only tool AuthZ

- **Signal:** System prompt says "do not call admin tools"; server uses service credentials with no per-user check.
- **Why keep:** Confused deputy / boundary-crossing. Fix: server-side per-resource AuthZ for the caller.
