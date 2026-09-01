# Report sample

Load only if the Phase 4 skeleton fill is unclear. Do not preload during review. Do not give this path to hunters. P1, P3, Dead Code, Test quality, and Author claimed are omitted (no items).

## Review Summary

Webhook handler. One verified P0 correctness issue before merging. Two hardening items deferred as P2 follow-ups. Verified 3, dropped 1 (CSRF covered by global middleware), downgraded 0.

Must NOT change: HTTP 2xx contract for valid payloads; idempotency key behavior.

Pipelines: Correctness, Security, Architecture, Quality, Performance (tier: normal); shapes: ts (Correctness, Architecture, Performance), web (Security, Quality)

### Findings Overview

| ID  | Severity | Category  | Perspective | File                  | Issue                       |
| --- | -------- | --------- | ----------- | --------------------- | --------------------------- |
| 1   | 🔴 P0    | bug       | Correctness | webhook-handler.ts:42 | Unhandled JSON.parse crash  |
| 2   | 🟡 P2    | hardening | Performance | webhook-handler.ts:67 | Fixed retry delay           |
| 3   | 🟡 P2    | style     | Quality     | webhook-handler.ts:89 | Mixed validation/processing |

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

**webhook-handler.ts:67** — Fixed 1-second retry delay. Category: hardening. Use exponential backoff to avoid hammering downstream during outages. Not exploitable today. Regression risk: retry timing assumptions in integration tests.

### What Looks Good

Idempotency key check at line 35 prevents duplicate processing during retries.

### Verification

Agent confirmed:

- [ ] Tests — not run
- [ ] Build — not run

### Verdict

Request changes — one verified P0 before merge. Hardening items are follow-ups.

To apply fixes: `/code-review-plus fix` (aliases: `apply`, `implement`).
