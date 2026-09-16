# Report sample

Load only if the Phase 4 skeleton fill is unclear. Do not preload during review. Do not give this path to hunters. P1, P3, Dead Code, Test quality, and What Looks Good extras are omitted (no items).

## Review Summary

Webhook handler. One verified P0 correctness issue before merging. One hardening item listed as P2 follow-up. Verified 3, dropped 1 (CSRF covered by global middleware), downgraded 0.

Must NOT change: HTTP 2xx contract for valid payloads; idempotency key behavior.

Pipelines: Correctness, Security, Quality (tier: normal); shapes: ts (Correctness, Quality)

Mode: fresh

quality source: slim-fallback

Checks: not run

### Findings Overview

| ID  | Severity | Category  | Perspective | File                  | Issue                       |
| --- | -------- | --------- | ----------- | --------------------- | --------------------------- |
| 1   | 🔴 P0    | bug       | Correctness | webhook-handler.ts:42 | Unhandled JSON.parse crash  |
| 2   | 🟡 P2    | hardening | Quality     | webhook-handler.ts:89 | Mixed validation/processing |

### P0 — Critical (must fix before merge)

**webhook-handler.ts:42** — Request body passed to `JSON.parse()` without try-catch. Malformed payload crashes the worker. Category: current bug. Provenance: direct user input (HTTP body). Regression risk: error response shape for this route; existing happy-path tests.

```typescript
let payload;
try {
  payload = JSON.parse(req.body);
} catch {
  return res.status(400).json({ error: "Invalid JSON" });
}
```

### P2 — Suggestions (optional improvements)

**webhook-handler.ts:89** — Validation and processing mixed in one function; a reader cannot state the happy path without simulating both. Category: maintainability. Suggested fix: extract validation with a responsibility name. Regression risk: error response shape for invalid payloads.

### Verdict

Request changes — one verified P0 before merge. Quality follow-up is optional.

To apply: `/code-review-plus fix` (P0, P1, vuln) · `/code-review-plus fix all` · `/code-review-plus fix 2` (ids). Aliases: `apply`, `implement`.

make-code was not in this environment; Quality used the built-in Floor.
