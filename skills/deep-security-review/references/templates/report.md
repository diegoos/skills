# Phase 4 — Security review report template

Fill the Template skeleton below with verified findings. The skeleton is the deliverable shape — emit those headings and the Findings Overview pipe table in the user-facing reply. Omit empty severity sections. Findings, Hardening notes, and Verification Gaps are mutually exclusive — one item in exactly one section. Report secrets as `file:line` + type only. When kept count is **0**, state that nothing was found, Approve (residual risk documented if any), and leave Findings Overview with header + separator only (no invented data rows).

## Render rules

1. **Skeleton fill** — paste the Template headings in order; put content under each heading. Severity detail sections expand Findings rows; they do not replace Findings Overview. Hardening notes and Verification Gaps stay separate buckets.
2. **Findings Overview is a Markdown pipe table** — seven columns exactly: `ID | Severity | Security | Category | Domain | File | Issue`. One data row per kept vulnerability (`category = vulnerability`) only. Severity/category cells use: 🚨 vulnerability · 🔴 P0 · 🟠 P1 · 🟡 P2 · ⚪️ P3. Security column is the 1:1 map of P (P0→CRITICAL · P1→HIGH · P2→MEDIUM · P3→LOW).
3. **Heading strings** — keep the Template's English heading text (`## Security Review Summary`, `### Threat Model (brief)`, `### Findings Overview`, `### P0 — Critical (must fix before ship)`, `### P1 — Important (should fix)`, `### P2 — Limited-impact vulnerabilities`, `### P3 — Low-risk current issues`, `### Hardening notes`, `### Open Questions / Assumptions`, `### What Looks Good`, `### Verification Gaps`, `### Verdict`). Translate prose inside sections when the user language differs; keep these heading strings so the shape stays stable.
4. **Counts** — Security Review Summary states kept / downgraded / dropped and residual runtime risk when present.
5. **Verdict** — end with one of Approve / Approve with follow-ups / Request changes per the Template rules, plus the fix hint when actionable findings remain.

## Template

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

## Completion criterion

Phase 4 is done when the user-facing reply is a skeleton fill of this Template: English heading strings above, a Findings Overview pipe table with columns `ID | Severity | Security | Category | Domain | File | Issue` (header + separator always; one data row per kept vulnerability, or header-only when kept is 0), Threat Model brief, Hardening notes or explicit none, Verification Gaps, Verdict, and kept/downgraded/dropped counts in Security Review Summary. Apply hint included when actionable findings remain.
