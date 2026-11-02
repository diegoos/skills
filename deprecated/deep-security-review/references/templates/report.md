# Phase 4 — Report template

Fill the Template skeleton below with verified findings. The skeleton is the deliverable shape. Emit a heading only when that section has content. Always emit `## Review Summary`, `### Threat Model (brief)`, `### Findings Overview`, and `### Verdict`. Severity detail sections expand findings; they do not replace Findings Overview. Report secrets as `file:line` + type only. When kept count is **0**, state that nothing was found in this pass, Approve (residual risk documented if any), and leave Findings Overview with header + separator only (no invented data rows).

If the heading order is unclear, READ `../examples/report-sample.md`. Do not preload it.

## Render rules

1. **Skeleton fill** — emit Template headings in order, only those with a body. Always emit `## Review Summary`, `### Threat Model (brief)`, `### Findings Overview`, and `### Verdict`. Severity detail sections expand Findings rows; they do not replace Findings Overview. Verification Gaps stay a separate bucket (`needs-runtime` / process), never a table row.
2. **Findings Overview is a Markdown pipe table** — six columns exactly: `ID | Severity | Category | Domain | File | Issue`. One data row per kept finding (vulnerability and hardening). Severity/category cells use: 🚨 vulnerability · 🔴 P0 · 🟠 P1 · 🟡 P2 · ⚪️ P3. Use 🚨 only when `category` is vulnerability/vuln. Label hardening items `hardening`.
3. **Heading strings** — when a section is present, use the Template's English heading text (`## Review Summary`, `### Threat Model (brief)`, `### Findings Overview`, `### P0 — Critical (must fix before merge)`, `### P1 — Important (should fix)`, `### P2 — Suggestions (optional improvements)`, `### P3 — Nits (optional)`, `### What Looks Good`, `### Verification Gaps`, `### Verdict`). Translate prose inside sections when the user language differs. Omit the heading when the body would be empty: P0–P3 with no findings at that severity, `### What Looks Good` when there is no specific positive that does not contradict findings, `### Verification Gaps` when there is no gap.
4. **Summary lines** — under Review Summary, include `Must NOT change: …`, `Domains: …` and `shapes:` when shapes were attached, `serial: yes` only when two or more domains ran in series, and `Checks: ran … | not run …`. Counts: kept / downgraded / dropped and residual runtime risk when present.
5. **Verdict** — end with one of Approve / Approve with follow-ups / Request changes per the Template rules, plus the fix hint when actionable findings remain.

## Template

```markdown
## Review Summary

[2–3 sentences. Direct assessment: ship it, minor fixes, or serious issues. State counts: kept / downgraded / dropped. Note residual runtime risk if any.]

Must NOT change: [auth_model, contracts, intended_behavior named in the threat model]

Domains: [list][; shapes: …]

serial: yes

Checks: ran … | not run …

### Threat Model (brief)

- Assets: …
- Critical entry points: …
- Highest-privilege abuse goals considered: …
- Hotspots reviewed: … # from manifest
- Bypasses: … # or "none found"
- auth_model: …

### Findings Overview

Kept findings (`vulnerability` and `hardening`). Severity/category cells use: 🚨 vulnerability · 🔴 P0 · 🟠 P1 · 🟡 P2 · ⚪️ P3.

| ID  | Severity | Category | Domain | File            | Issue             |
| --- | -------- | -------- | ------ | --------------- | ----------------- |
| 1   | 🔴 P0    | 🚨 vuln  | AuthZ  | path/file.ts:42 | Brief description |

### P0 — Critical (must fix before merge)

Omit this section entirely if none exist.

**file.ts:42** — What is wrong, why exploitable today, provenance, impact. Include trace / intended_behavior / trigger_sketch / regression_risk.

[Optional: minimal fix code block]

### P1 — Important (should fix)

Omit this section entirely if none exist.

**file.ts:67** — Issue, path, fix. Include trace / intended_behavior / trigger_sketch / regression_risk.

### P2 — Suggestions (optional improvements)

Omit this section entirely if none exist.

Label hardening items explicitly. List every kept P2.

### P3 — Nits (optional)

Omit this section entirely if none exist.

List every kept P3.

### What Looks Good

Omit this section entirely when there is no specific positive that does not contradict findings.

1–2 specific positive controls.

### Verification Gaps

Omit this section entirely when there is no gap.

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
- **Request changes** — at least one **verified** P0

To apply: `/deep-security-review fix` (P0, P1) · `/deep-security-review fix all` · `/deep-security-review fix 2,3` (ids). Aliases: `apply`, `implement`.

[code-review-plus line, last line] For PR bugs and quality: `/code-review-plus` · <https://github.com/diegoos/skills/tree/main/skills/code-review-plus>
```

Omit the `serial:` line unless two or more domains ran in series.

**code-review-plus line.** Emit it when this conversation has no prior `code-review-plus` report. Omit it when a CRP report already exists. Leave `code-review-plus` unstarted. The line includes the Skill links URL.

## Completion criterion

Phase 4 is done when the user-facing reply is a skeleton fill of this Template: always-on headings (`## Review Summary`, `### Threat Model (brief)`, `### Findings Overview`, `### Verdict`) with English strings; a Findings Overview pipe table with columns `ID | Severity | Category | Domain | File | Issue` (header + separator always; one data row per kept finding, or header-only when kept is 0); P0–P3 sections list every kept finding at that severity (no hide-cap); `Must NOT change` plus Domains line (shapes when used; `serial: yes` when serial fallback ran); verified-vs-dropped counts in Review Summary; optional headings (P0–P3, What Looks Good, Verification Gaps) present only when they have a body. Apply hint included when actionable findings remain. CRP last line when this conversation has no prior CRP report (includes Skill links URL; omit when a CRP report already exists).
