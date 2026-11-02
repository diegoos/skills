# Report sample

Load only if the Phase 4 skeleton fill is unclear. Do not preload during review. Do not give this path to hunters. P1, P3, What Looks Good, and Verification Gaps extras are omitted (no items).

## Review Summary

Invoice API. One verified P0 AuthZ issue before merging. One hardening item listed as P2 follow-up. Verified 2, dropped 1 (list query already scoped by tenant), downgraded 0.

Must NOT change: tenant from session, never body; 403/404 shape on cross-tenant reads.

Domains: AuthZ, Injection, Secrets, Infra; shapes: api (AuthZ, Injection)

Checks: not run

### Threat Model (brief)

- Assets: tenant invoices, session cookie
- Critical entry points: `/api/invoices/:id`, `/api/invoices`
- Highest-privilege abuse goals considered: read another tenant's invoice
- Hotspots reviewed: `/api/invoices/:id`, password-reset
- Bypasses: none found
- auth_model: Session cookie; tenant from session, never body

### Findings Overview

| ID  | Severity | Category  | Domain | File              | Issue                         |
| --- | -------- | --------- | ------ | ----------------- | ----------------------------- |
| 1   | 🔴 P0    | 🚨 vuln   | AuthZ  | invoices.ts:42    | IDOR on invoice fetch         |
| 2   | 🟡 P2    | hardening | Infra  | rate-limit.ts:18  | Login limiter is IP-only      |

### P0 — Critical (must fix before merge)

**invoices.ts:42** — `findUnique({ id })` then return. Authenticated user supplies another tenant's id and reads the row. Provenance: user. Trace: session → GET `/api/invoices/:id` → unscoped lookup → cross-tenant invoice. Intended behavior: owner or same-tenant only; 403/404 otherwise. Trigger sketch: swap id to another tenant's invoice while logged in. Regression risk: 403/404 shape for this route; existing happy-path tenant tests.

```typescript
const invoice = await db.invoice.findFirst({
  where: { id, tenantId: session.tenantId },
});

if (!invoice) return res.status(404).end();
```

### P2 — Suggestions (optional improvements)

**rate-limit.ts:18** — Login limiter keys on IP only. Category: hardening. Not exploitable today (lockout still fires); stuffing from a pool of IPs would skip it. Regression risk: legitimate shared-NAT users hitting 429.

### Verdict

Request changes — one verified P0 before merge. Hardening follow-up is optional.

To apply: `/deep-security-review fix` (P0, P1) · `/deep-security-review fix all` · `/deep-security-review fix 2` (ids). Aliases: `apply`, `implement`.

For PR bugs and quality: `/code-review-plus` · <https://github.com/diegoos/skills/tree/main/skills/code-review-plus>
