# Security Review Report Template

Render Phase 4 using this template. Omit empty severity sections. Findings, Hardening notes, and Verification Gaps are mutually exclusive — one item in exactly one section. When kept count is **0**, state that nothing was found, Approve (residual risk documented if any), and leave Findings Overview empty — do not invent rows.

```markdown
## Security Review Summary

[2–3 sentences. Direct assessment: ship it, minor fixes, or serious issues. State counts: kept / downgraded / dropped. Note residual runtime risk if any.]

### Threat Model (brief)

- Assets: …
- Critical entry points: …
- Highest-privilege abuse goals considered: …
- Hotspots reviewed: … # from manifest
- Bypasses: … # or "none found"
- auth_model: …

### Findings Overview

Kept vulnerabilities only (`category = vulnerability`). Severity/category cells use: 🚨 vulnerability · 🔴 P0 · 🟠 P1 · 🟡 P2 · ⚪️ P3. Security column is the 1:1 map of P (P0→CRITICAL · P1→HIGH · P2→MEDIUM · P3→LOW).

| ID  | Severity | Security | Category | Domain | File            | Issue             |
| --- | -------- | -------- | -------- | ------ | --------------- | ----------------- |
| 1   | 🔴 P0    | CRITICAL | 🚨 vuln  | AuthZ  | path/file.ts:42 | Brief description |

### P0 — Critical (must fix before ship)

Omit entirely if none.

**file.ts:42** — What is wrong, why exploitable today, provenance, impact. Include trace / intended behavior / trigger sketch.

[Optional: minimal fix code block]

### P1 — Important (should fix)

**file.ts:67** — Issue, path, fix. Include trace / intended behavior / trigger sketch.

### P2 — Limited-impact vulnerabilities

Real vulns with limited blast radius. Cap at the most impactful ~5 if many.

### P3 — Low-risk current issues

Max 3. Not speculative hardening.

### Hardening notes

Defense-in-depth and downgraded items that are **not** exploitable today. Cap ~5. Never duplicate a Findings row here.

### Open Questions / Assumptions

Only what blocks stronger claims. List what must be verified at runtime.

### What Looks Good

1–2 specific positive controls. Must not contradict findings above.

### Verification Gaps

- [ ] Auth: unauthenticated → 401
- [ ] AuthZ: wrong tenant/user → 403/404
- [ ] AuthZ fail-open: auth dependency error → deny
- [ ] Validation: malformed input → 400, no mutation
- [ ] Secrets: none in logs/errors/client bundles
- [ ] Audit/alert: auth failures and high-risk actions leave an auditable trail (else Gaps)
- [ ] Tooling: secret scan / SCA / SAST status (if in scope)
- [ ] needs-runtime claims listed below (no P0–P3 assigned)

State what was **not** verified. Route `needs-runtime` candidates here — not into Findings.

### Verdict

- **Approve** — no verified P0/P1 vulns; residual risk documented
- **Approve with follow-ups** — no verified P0; P1 deferred with plan or only hardening
- **Request changes** — at least one **verified** P0 (or blocking P1 if user set that bar)

To apply fixes: `/deep-security-review fix` (aliases: `apply`, `implement`).
```
