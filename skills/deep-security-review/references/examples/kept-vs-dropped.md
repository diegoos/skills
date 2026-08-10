# Examples — confirmation gates, FPs, kept vs dropped

Orchestrator-only. Read when keep/drop is unclear, when a candidate matches a gate or recurring FP pattern, or when disprove needs a worked case. Do not preload. Do not give this file to hunters. Single source of truth for confirmation gates and recurring false positives.

## Confirmation gates

| Gate                                | Keep only when                                                                |
| ----------------------------------- | ----------------------------------------------------------------------------- |
| Parser / framing disagreement       | Two components + divergent parse with concrete cross-boundary effect          |
| Token / JWT claim                   | Verify line present **and** a required claim missing or unchecked             |
| Host / cache                        | Cross-user or cross-tenant impact demonstrated                                |
| Mitigating layer already blocks     | Downgrade to hardening (not keep as vuln)                                     |
| Unknown library / framework default | `needs-runtime` or unverifiable — do not invent P0/P1                         |
| AuthZ fail-open on error path       | Reachable error path **and** concrete privilege or data consequence           |
| Second-order / chained injection    | Both store and later sink proven; otherwise one finding or drop the weak half |

## Recurring false positives

| Pattern                                                                           | Why it is usually wrong                                                              |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Route "missing auth" when global middleware covers it                             | Check middleware / shared guards / matcher first                                     |
| "Missing CSRF" without framework defaults + cookie `SameSite`                     | Verify the actual CSRF strategy                                                      |
| ORM use treated as always-safe                                                    | Flag only when raw/dynamic queries are unsafe                                        |
| Schema/allowlist already strips privileged fields                                 | Mass-assignment FP — confirm the field reaches persistence                           |
| TypeScript types as runtime validation                                            | Types are not a control                                                              |
| LLM system prompt as access control                                               | Server must enforce tool/data permissions                                            |
| Helper named `auth()` treated as authorization                                    | AuthN ≠ AuthZ; require ownership/tenant proof                                        |
| XSS while final output escapes and unescapes only fixed literals                  | Not exploitable today — hardening at most                                            |
| Self-XSS only (attacker must paste into own session)                              | Drop unless it becomes stored/reflected for another user                             |
| `credentials: "include"` as cross-origin cookie leak                              | Browser sends cookies only for the destination origin                                |
| CORS `*` without credentials                                                      | Often intentional for public reads — keep only with credentialed or sensitive impact |
| Incomplete security headers / missing CSP with no exploit path                    | Hardening note, not vulnerability                                                    |
| Open redirect when redirect URI/host is allowlisted                               | Confirm allowlist is enforced server-side                                            |
| SSRF when URL is constant or allowlisted after DNS+redirects                      | Confirm rebind/TOCTOU actually bypasses the check                                    |
| GraphQL introspection "enabled" without checking production config                | Verify the deployed/prod path                                                        |
| Dependency CVE / advisory without reachability                                    | Triage via call graph / prod vs devDependency — else process/gap                     |
| IDOR when query already scopes by owner/tenant                                    | Re-read the data access line before keep                                             |
| Missing rate limit without an abuse-prone flow                                    | Hardening unless stuffing/spray path is concrete                                     |
| Missing cookie flags on a non-session / non-sensitive cookie                      | Drop or hardening                                                                    |
| JWT claim nit (`nbf` only) without forge/escalation path                          | Downgrade unless verify is missing or alg/key confused                               |
| Scanner finding (SAST/DAST) without a code-backed exploit path                    | Cite `file:line` or drop                                                             |
| P0 from "if in the future" / "any evolution could"                                | Future risk is hardening                                                             |
| Praise a global control in "What Looks Good" and flag the same control as missing | Self-consistency — drop one of them                                                  |
| suggested_fix that relaxes auth, validation, or error handling                    | Over-simplify — rewrite the fix fail-closed                                          |

## Worked cases — dropped

### Auth missing on a route; global middleware covers it

- **Signal:** Handler has no `requireAuth` call.
- **Why drop:** Middleware matcher already applies AuthN/AuthZ to the path. Check the global layer first.

### XSS while the final encoder escapes and only literal unescape remains

- **Signal:** Intermediate string replace looks unsafe.
- **Why drop:** Final HTML/attribute encoder escapes `&<>`; `replaceAll` uses only fixed literals. Hardening at most.

### Dependency CVE without a reachable call path

- **Signal:** Advisory on a transitive package.
- **Why drop:** Not imported on the prod path, or only a `devDependency`. Route to process/gap unless reachability is shown.

### "If a future caller skips the guard…"

- **Signal:** Speculative evolution.
- **Why drop:** Not exploitable today. Downgrade to hardening or drop.

## Worked cases — kept

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
