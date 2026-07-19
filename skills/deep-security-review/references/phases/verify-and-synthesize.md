# Phase 3 — Verify & Synthesize

Apply after all hunters return. Single source of truth for severity, false positives, and required finding fields.

## Verify checklist (every candidate)

```text
- [ ] Did I read the entire cited file (not just a snippet)?
- [ ] Did I read shared authz/validation middleware before flagging a route?
- [ ] What is the data provenance (user input / LLM / backend)?
- [ ] Did I trace entry → sink / final output?
- [ ] Can I point to the exact line that makes this exploitable TODAY?
- [ ] Is the proposed fix local and consistent with existing controls?
- [ ] Evidence level stated (proven / likely / needs-runtime)?
```

Drop or downgrade any item that fails. `needs-runtime` is never P0.

## Recurring false positives

| Pattern                                                                | Why it is usually wrong                       |
| ---------------------------------------------------------------------- | --------------------------------------------- |
| Route "missing auth" when global middleware covers it                  | Check middleware / shared guards first        |
| "Missing CSRF" without checking framework defaults + cookie `SameSite` | Verify the actual CSRF strategy               |
| ORM use treated as always-safe                                         | Flag only when raw/dynamic queries are unsafe |
| TypeScript types as runtime validation                                 | Types are not a control                       |
| LLM system prompt as access control                                    | Server must enforce tool/data permissions     |
| P0 from "if in the future" or "any evolution could"                    | Future risk is hardening (P2)                 |
| Helper named `auth()` treated as authorization                         | AuthN ≠ AuthZ; require ownership/tenant proof |

## Synthesize steps

1. Verify — run checklist; drop or downgrade failures
2. Deduplicate — merge overlapping findings across domains
3. Categorize — assign exactly one category
4. Prioritize — map to P0–P3 and CRITICAL–LOW
5. Self-consistency — no contradictions with "What Looks Good"
6. Gaps — skipped domains / needs-runtime called out
7. Strengths — note 1–2 specific controls done well

## Categories

| Category                         | Definition                                       | Typical severity |
| -------------------------------- | ------------------------------------------------ | ---------------- |
| **Current vulnerability**        | Exploitable **today**, with a pointable line     | P0/P1            |
| **Hardening / defense-in-depth** | Not exploitable today; protects future evolution | P2               |
| **Process / residual risk**      | Missing tests, tooling, or runtime evidence      | P2/P3            |

## Severity

| Prefix | Meaning                                                                       | Author action                    |
| ------ | ----------------------------------------------------------------------------- | -------------------------------- |
| P0     | Verified critical — account/tenant/secret/payment compromise or RCE **today** | Must fix before ship             |
| P1     | Real vuln with lower blast radius, or clear authz/injection gap               | Should fix; defer only with plan |
| P2     | Hardening, limited-impact gap, or needs-runtime confirmation                  | Optional follow-up               |
| P3     | Nit — docs/config drift, non-sensitive hardening                              | Can ignore                       |

**Calibration:** P0 blocks ship — demonstrated only. Prefer one well-supported High over many speculative Mediums. Hardening is follow-up, not blocker.

## Security classification

| Level    | Meaning                                                 | Typical P |
| -------- | ------------------------------------------------------- | --------- |
| CRITICAL | Exploitable in production with high impact **today**    | P0        |
| HIGH     | Significant risk with a concrete path; needs prompt fix | P1        |
| MEDIUM   | Defense-in-depth gap, lower immediate risk              | P2        |
| LOW      | Hardening / observability / non-sensitive drift         | P2/P3     |

## VerifiedFinding fields

1. Exact **file:line**
2. **Category** (vulnerability / hardening / process)
3. **Why it is exploitable** — concrete attacker path
4. **Data provenance**
5. **Severity** (P0–P3) and **security level** (CRITICAL–LOW)
6. **Evidence level** (proven / likely / needs-runtime)
7. **Proposed fix** — local when possible; say if unverified to compile/pass
8. **verification_note** — why it survived (or drop reason)

```yaml
status: kept | dropped | downgraded
drop_reason: optional
# plus all VerifiedFinding fields when kept/downgraded
```

## Verification probes (shared)

- Auth: unauthenticated → `401`
- AuthZ: wrong tenant/user → `403`/`404`
- Validation: malformed input → `400`, no mutation
- Injection: payload treated as data
- Rate limit: abuse-prone flows → `429`
- Secrets: none in logs/errors/client bundles
- LLM tools: prompt cannot call unauthorized tools or cross-tenant data

## Completion criterion

Every surviving finding has all required fields; dropped/downgraded counts are recorded for the summary.
