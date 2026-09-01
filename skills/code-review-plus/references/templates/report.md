# Phase 4 — Report template

Fill the Template skeleton below with synthesized findings. The skeleton is the deliverable shape. Do not send it to the user until Phase 4.5 persist is done. Emit a heading only when that section has content. Only `kept` / adjusted `downgraded` findings appear. Report secrets as `file:line` + type only. When kept count is **0**, state that nothing was found, Approve (or Approve with follow-ups if only hardening remains), and leave Findings Overview with header + separator only (no invented data rows).

If the heading order is unclear, READ `../examples/report-sample.md`. Do not preload it.

## Render rules

1. **Skeleton fill** — emit Template headings in order, only those with a body. Always emit `## Review Summary`, `### Findings Overview`, `### Verification`, and `### Verdict`. Severity detail sections expand findings; they do not replace Findings Overview. Complexity scores stay in the finding body (`parseOrder` CC 14→4), never as a seventh Overview column or a separate heading.
2. **Findings Overview is a Markdown pipe table** — six columns exactly: `ID | Severity | Category | Perspective | File | Issue`. One data row per kept/downgraded finding. Severity/category cells use: 🚨 vulnerability · 🔴 P0 · 🟠 P1 · 🟡 P2 · ⚪️ P3. Use 🚨 only when `category` is vulnerability/vuln.
3. **Heading strings** — when a section is present, use the Template's English heading text (`## Review Summary`, `### Findings Overview`, `### P0 — Critical (must fix before merge)`, `### P1 — Important (should fix)`, `### P2 — Suggestions (optional improvements)`, `### P3 — Nits (optional)`, `### Dead Code (if any)`, `### Test quality`, `### What Looks Good`, `### Verification`, `### Verdict`). Translate prose inside sections when the user language differs. Omit the heading when the body would be empty: P0–P3 with no findings at that severity, Dead Code with no verified unused items, `### Test quality` when the review source has no tests, `### What Looks Good` when there is no specific positive that does not contradict findings.
4. **Pipelines line** — under Review Summary, include `Must NOT change: …`, `Pipelines: … (tier: …)` and `shapes:` when shapes were attached.
5. **Verification blocks** — emit Author claimed only when the author claimed something. Emit the Manual / UI line only when the review source has a UI. Always emit P0 verifier ran/skipped. Emit `serial: yes` only when Phase 2 ran hunters in series.
6. **Verdict** — end with one of Approve / Approve with follow-ups / Request changes per the Template rules, plus the fix hint when actionable findings remain.

## Template

```markdown
## Review Summary

[2-3 sentences. Direct assessment: ship it, minor fixes needed, or serious issues. State how many findings were verified vs downgraded/dropped.]

Must NOT change: [concrete APIs, contracts, UX, callers from Phase 1]

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

Omit this section entirely if none exist.

**file.ts:67** — Issue, rationale, regression_risk.

### P2 — Suggestions (optional improvements)

Omit this section entirely if none exist.

Keep focused. If more than 5, keep the most impactful. Label hardening items explicitly.

### P3 — Nits (optional)

Omit this section entirely if none exist.

Max 3. Pick the most impactful only.

### Dead Code (if any)

Omit this section entirely if none exist.

List candidates only after verifying all consumers. Ask: "Should I remove these now-unused items: [list]?"

### Test quality

Omit this section entirely when the review source has no tests.

- Useful: yes | no — [which are not, with file:line]
- Efficient: yes | no — [which are not, with file:line]
- Removable (non-critical): [list] | none. Ask before delete.

### What Looks Good

Omit this section entirely when there is no specific positive that does not contradict findings.

1-2 specific positives (e.g. stable vocabulary, no unshipped compat stubs, no PR-history comments).

### Verification

Author claimed:

- …

Agent confirmed:

- [ ] Tests — ran / not run (list commands if ran)
- [ ] Build — ran / not run
- [ ] Manual / UI — done / not done

P0 verifier: ran | skipped (reason: …)

serial: yes

State what was **not** verified. "I did not run the build" is better than an unproven "tests pass". Omit the `serial:` line when hunters ran in parallel.

### Verdict

- **Approve** — ready to merge (no verified P0)
- **Approve with follow-ups** — no verified P0; hardening/style items listed by priority
- **Request changes** — at least one **verified** P0 exists

If Scope set `Oversized: yes`, ask for a split before further review rounds.

To apply fixes: `/code-review-plus fix` (aliases: `apply`, `implement`).
```

## Calibration (optional)

If the user asks to calibrate after the report, follow `../examples/eval-notes.md` in the conversation. Do not preload it during Phase 4. Do not create that file in the reviewed target repo unless they ask.

## Completion criterion

Phase 4 is done when the skeleton is filled and **not yet sent**: always-on headings (`## Review Summary`, `### Findings Overview`, `### Verification`, `### Verdict`) with English strings; a Findings Overview pipe table with columns `ID | Severity | Category | Perspective | File | Issue` (header + separator always; one data row per kept finding, or header-only when kept is 0); `Must NOT change` plus pipelines/tier line (shapes when used); verified-vs-dropped counts in Review Summary; Verification with P0 verifier ran/skipped, explicit unverified claims, and `serial: yes` only when Phase 2 ran serial; optional headings (P0–P3, Dead Code, Test quality, What Looks Good) present only when they have a body. Apply hint included when actionable findings remain. Emit only after Phase 4.5.
