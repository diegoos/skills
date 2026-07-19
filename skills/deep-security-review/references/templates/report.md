# Security Review Report Template

Render Phase 4 using this template. Omit empty severity sections.

```markdown
## Security Review Summary

[2–3 sentences. Direct assessment: ship it, minor fixes, or serious issues. State how many findings were verified vs downgraded/dropped. Note residual runtime risk if any.]

### Threat Model (brief)

- Assets: …
- Critical entry points: …
- Highest-privilege abuse goals considered: …

### Findings Overview

| ID  | Severity | Security | Category | Domain | File            | Issue             |
| --- | -------- | -------- | -------- | ------ | --------------- | ----------------- |
| 1   | P0       | CRITICAL | vuln     | AuthZ  | path/file.ts:42 | Brief description |

### P0 — Critical (must fix before ship)

Omit entirely if none.

**file.ts:42** — What is wrong, why exploitable today, provenance, impact.

[Optional: minimal fix code block]

### P1 — Important (should fix)

**file.ts:67** — Issue, path, fix.

### P2 — Hardening / needs runtime

Keep focused. Label hardening vs needs-runtime explicitly. Cap at the most impactful ~5 if many.

### P3 — Nits (optional)

Max 3.

### Open Questions / Assumptions

Only what blocks stronger claims. List what must be verified at runtime.

### What Looks Good

1–2 specific positive controls. Must not contradict findings above.

### Verification Gaps

- [ ] Auth: unauthenticated → 401
- [ ] AuthZ: wrong tenant/user → 403/404
- [ ] Validation: malformed input → 400, no mutation
- [ ] Secrets: none in logs/errors/client bundles
- [ ] Tooling: secret scan / SCA / SAST status (if in scope)

State what was **not** verified.

### Verdict

- **Approve** — no verified P0/P1 vulns; residual risk documented
- **Approve with follow-ups** — no verified P0; P1 deferred with plan or only hardening
- **Request changes** — at least one **verified** P0 (or blocking P1 if user set that bar)
```
