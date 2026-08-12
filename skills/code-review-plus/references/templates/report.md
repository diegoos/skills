# Phase 4 — Report template

Fill the Template skeleton below with synthesized findings. The skeleton is the deliverable shape — emit those headings and the Findings Overview pipe table in the user-facing reply. Skip empty severity sections. Only `kept` / adjusted `downgraded` findings appear. Report secrets as `file:line` + type only. When kept count is **0**, state that nothing was found, Approve (or Approve with follow-ups if only hardening remains), and leave Findings Overview with header + separator only (no invented data rows).

## Render rules

1. **Skeleton fill** — paste the Template headings in order; put content under each heading. Severity detail sections expand findings; they do not replace Findings Overview.
2. **Findings Overview is a Markdown pipe table** — six columns exactly: `ID | Severity | Category | Perspective | File | Issue`. One data row per kept/downgraded finding. Severity/category cells use: 🚨 vulnerability · 🔴 P0 · 🟠 P1 · 🟡 P2 · ⚪️ P3. Use 🚨 only when `category` is vulnerability/vuln.
3. **Heading strings** — keep the Template's English heading text (`## Review Summary`, `### Findings Overview`, `### P0 — Critical (must fix before merge)`, `### P1 — Important (should fix)`, `### P2 — Suggestions (optional improvements)`, `### P3 — Nits (optional)`, `### Dead Code (if any)`, `### What Looks Good`, `### Verification`, `### Verdict`). Translate prose inside sections when the user language differs; keep these heading strings so the shape stays stable.
4. **Pipelines line** — under Review Summary, include `Pipelines: … (tier: …)` and `shapes:` when shapes were attached.
5. **Verdict** — end with one of Approve / Approve with follow-ups / Request changes per the Template rules, plus the fix hint when actionable findings remain.

## Template

```markdown
## Review Summary

[2-3 sentences. Direct assessment: ship it, minor fixes needed, or serious issues. State how many findings were verified vs downgraded/dropped.]

Pipelines: [list] (tier: trivial | normal | large/sensitive)[; shapes: …]

### Findings Overview

| ID  | Severity | Category | Perspective | File            | Issue             |
| --- | -------- | -------- | ----------- | --------------- | ----------------- |
| 1   | 🔴 P0    | 🚨 vuln  | Security    | path/file.ts:42 | Brief description |

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

1-2 specific positives (e.g. stable vocabulary, no unshipped compat stubs, no PR-history comments). Must not contradict findings above.

### Verification

Author claimed:

- …

Agent confirmed:

- [ ] Tests — ran / not run (list commands if ran)
- [ ] Build — ran / not run
- [ ] Manual / UI — done / not done

State what was **not** verified. "I did not run the build" is better than an unproven "tests pass".

### Verdict

- **Approve** — ready to merge (no verified P0)
- **Approve with follow-ups** — no verified P0; hardening/style items listed by priority
- **Request changes** — at least one **verified** P0 exists

If Scope marked the diff oversized, ask for a split before further review rounds.

To apply fixes: `/code-review-plus fix` (aliases: `apply`, `implement`).
```

## Calibration (optional)

If the user asks to calibrate after the report, follow `../examples/eval-notes.md` in the conversation. Do not preload it during Phase 4. Do not create that file in the reviewed target repo unless they ask.

## Sample output

### Review Summary

Webhook handler. One verified P0 correctness issue before merging. Two hardening items deferred as P2 follow-ups. Verified 3, dropped 1 (CSRF covered by global middleware), downgraded 0.

Pipelines: Correctness, Security, Architecture, Quality, Performance (tier: normal)

### Findings Overview

| ID  | Severity | Category  | Perspective | File                  | Issue                       |
| --- | -------- | --------- | ----------- | --------------------- | --------------------------- |
| 1   | 🔴 P0    | bug       | Correctness | webhook-handler.ts:42 | Unhandled JSON.parse crash  |
| 2   | 🟡 P2    | hardening | Performance | webhook-handler.ts:67 | Fixed retry delay           |
| 3   | 🟡 P2    | style     | Quality     | webhook-handler.ts:89 | Mixed validation/processing |

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

Author claimed:

- (none in context)

Agent confirmed:

- [ ] Tests — not run
- [ ] Build — not run

### Verdict

Request changes — one verified P0 before merge. Hardening items are follow-ups.

To apply fixes: `/code-review-plus fix` (aliases: `apply`, `implement`).

## Completion criterion

Phase 4 is done when the user-facing reply is a skeleton fill of this Template: English heading strings above, a Findings Overview pipe table with columns `ID | Severity | Category | Perspective | File | Issue` (header + separator always; one data row per kept finding, or header-only when kept is 0), pipelines/tier line (shapes when used), verified-vs-dropped counts in Review Summary, Verification with explicit unverified claims, and Verdict. Apply hint included when actionable findings remain.
