# Review Checklists

Cues for Step 2 when the diff touches security, performance, architecture, or dependencies. Apply what fits the diff alongside your own judgment.

## Security cues

Trace untrusted input (requests, uploads, webhooks, third-party APIs, LLM output) from entry to sink:

- **AuthN vs AuthZ:** authentication on protected endpoints, plus ownership, tenant, or role proof on every resource read or mutation (IDOR).
- **Input and sinks:** allowlist validation at trust boundaries; parameterized queries; encoded HTML output; validated redirect targets (open redirect); allowlisted server-side fetch URLs blocking private/reserved IPs (SSRF); symlink resolution (`realpath`) and allowlisted root checks before destructive path operations.
- **Fail closed:** error paths and `catch` blocks around auth or validation deny access on failure.
- **Secrets and data exposure:** hardcoded secrets, or sensitive fields (`passwordHash`, tokens, session headers, stack traces, raw SQL, PII) exposed in responses or logs.
- **AI / LLM boundaries:** model output treated as untrusted before `eval`, SQL, shell, HTML, or file paths; tool and tenant permissions enforced in server code rather than the system prompt; bounded tokens, rates, and loop depth.

### False-positive defaults (override only with a concrete exploit path today)

- Missing security headers, CSP, or non-session cookie flags with no exploit path → `hardening` at most.
- Generic DoS, resource exhaustion, or missing rate limit → drop unless one untrusted request crashes or stalls the service, or a concrete abuse gain exists (for example, unlimited attempts on a short OTP).
- XSS in React/JSX with no `dangerouslySetInnerHTML` or raw HTML sink → drop.
- Route missing CSRF or auth call when global middleware already covers its path matcher → drop after checking middleware.
- Attack requiring control of env vars, CLI flags, deploy config, or guessing a random UUID → drop.
- TypeScript types treated as runtime validation → keep the finding when untrusted input has no runtime check.

## Performance cues

Flag when the hot path or production-scale cost is visible in the diff today:

- **Database and backend:** N+1 queries or I/O in loops (batch, join, or load once); queries or list endpoints without `LIMIT` or pagination; connection pool created per request instead of per process; synchronous heavy compute in request handlers.
- **Caching:** cache key missing a varying dimension (tenant, viewer, locale, permissions — cross-user leak); unbounded in-memory cache with no eviction or ceiling; origin errors cached as negative entries.
- **Frontend and UI:** expensive work in hot event handlers (long tasks >50ms hurting INP); layout thrashing (interleaved DOM reads and writes); unvirtualized large lists; hero/LCP images lazy-loaded or missing `width`/`height` (CLS).

## Structural remedies

Pair a structural finding with a concrete move:

- Replace chained conditionals on the same shape with a typed model, lookup table, or dispatcher.
- Flatten nesting ≥3 with guard clauses, or extract the inner block under a responsibility name.
- Collapse duplicate branches into one flow.
- Move feature-specific logic out of a shared module into its owning layer.
- Reuse an existing canonical helper instead of a near-duplicate.
- Make a type boundary explicit so downstream casts and silent fallbacks disappear.
- Delete a pass-through wrapper or single-implementation interface.

## Dependency cues

When the diff modifies manifests or lockfiles:

- Prefer the standard library, platform APIs, or an already-installed package over a new dependency for a few lines.
- Flag bulk multi-package upgrades, hand-edited lockfiles, or competing lockfiles that obscure breaking changes.
- On major or risky version bumps, check that breaking changes are handled and covered by tests.
