# Phase 4 — Report template

Render the review report from synthesized findings. Skip empty severity sections. Only `kept` / adjusted `downgraded` findings appear.

## Template

```markdown
## Review Summary

[2-3 sentences. Direct assessment: ship it, minor fixes needed, or serious issues. State how many findings were verified vs downgraded/dropped.]

### Findings Overview

| ID  | Severity | Category | Perspective | File            | Issue             |
| --- | -------- | -------- | ----------- | --------------- | ----------------- |
| 1   | P0       | vuln     | Security    | path/file.ts:42 | Brief description |

### P0 — Critical (must fix before merge)

Omit this section entirely if none exist.

**file.ts:42** — What is wrong, why it is exploitable today, data provenance. Include regression_risk for the suggested fix.

[Optional: corrected code block]

### P1 — Important (should fix)

**file.ts:67** — Issue, rationale, regression_risk.

### P2 — Suggestions (optional improvements)

Keep focused. If more than 5, keep the most impactful. Label hardening items explicitly.

### P3 — Nits (optional)

Max 3. Pick the most impactful only.

### Dead Code (if any)

List candidates only after verifying all consumers. Ask: "Should I remove these now-unused items: [list]?"

### What Looks Good

1-2 specific positives. Not generic praise. Must not contradict findings above.

### Verification

- [ ] Tests pass and cover the change
- [ ] Build succeeds
- [ ] Manual verification done (UI: screenshots if applicable)

State what was **not** verified. "I did not run the build" is better than an unproven "tests pass".

### Verdict

- **Approve** — ready to merge
- **Approve with follow-ups** — no verified P0; hardening/style items listed by priority
- **Request changes** — at least one **verified** P0 exists

To apply fixes: `/code-review-plus fix` (aliases: `apply`, `implement`).
```

## Sample output

### Review Summary

Solid webhook handler implementation. One verified P0 correctness issue before merging. Two hardening items deferred as P2 follow-ups. Verified 3, dropped 1 (CSRF covered by global middleware), downgraded 0.

### Findings Overview

| ID  | Severity | Category  | Perspective | File                  | Issue                       |
| --- | -------- | --------- | ----------- | --------------------- | --------------------------- |
| 1   | P0       | bug       | Correctness | webhook-handler.ts:42 | Unhandled JSON.parse crash  |
| 2   | P2       | hardening | Performance | webhook-handler.ts:67 | Fixed retry delay           |
| 3   | P2       | style     | Quality     | webhook-handler.ts:89 | Mixed validation/processing |

### P0 — Critical

**webhook-handler.ts:42** — Request body passed to `JSON.parse()` without try-catch. Malformed payload crashes the worker. Category: current bug. Provenance: direct user input (HTTP body). Regression risk: error response shape for this route; existing happy-path tests.

```typescript
let payload;
try {
  payload = JSON.parse(req.body);
} catch {
  return res.status(400).json({ error: "Invalid JSON" });
}
```

### P2 — Suggestions

**webhook-handler.ts:67** — Fixed 1-second retry delay. Category: hardening. Use exponential backoff to avoid hammering downstream during outages. Not exploitable today. Regression risk: retry timing assumptions in integration tests.

### What Looks Good

Idempotency key check at line 35 prevents duplicate processing during retries.

### Verification

- [ ] Tests pass — not run in this review
- [ ] Build succeeds — not run in this review

### Verdict

Request changes — one verified P0 before merge. Hardening items are follow-ups.

To apply fixes: `/code-review-plus fix` (aliases: `apply`, `implement`).

## Completion criterion

Findings Overview, verdict, verified-vs-dropped counts, and explicit unverified claims are present. Apply hint included when actionable findings remain.
