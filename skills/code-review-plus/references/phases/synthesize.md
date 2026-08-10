# Phase 3 — Synthesize

Assign categories, severity, and required finding fields after Pass B verification.

If manifest/lockfile is in scope, read `../dependency-review.md` and fold dependency findings that survive the same evidence bar.

## Steps

1. Take only `kept` and `downgraded` candidates from Phase 2.5
2. Deduplicate: merge overlapping findings across pipelines
3. Categorize: assign exactly one category
4. Prioritize: map category + impact to P0/P1/P2/P3
5. Attach **regression_risk** on every kept finding's suggested fix
6. Self-consistency: no contradictions with "What Looks Good"
7. Gaps: fill only if clearly warranted and verified
8. Strengths: note 1–2 specific things done well

## Categories

| Category                         | Definition                                                                      | Typical severity |
| -------------------------------- | ------------------------------------------------------------------------------- | ---------------- |
| **Current vulnerability/bug**    | Exploitable or reproducible breakage today, with a pointable line               | P0/P1            |
| **Hardening / defense-in-depth** | Not exploitable today; protects against future evolution or hypothetical caller | P2               |
| **Maintainability / style**      | Fragile, duplicated, inconsistent; no functional impact                         | P2/P3            |

## Severity

| Prefix | Meaning                                                                                | Author action                          |
| ------ | -------------------------------------------------------------------------------------- | -------------------------------------- |
| P0     | Verified critical: exploitable bug, active vuln, data loss, broken functionality today | Must fix before merge                  |
| P1     | Important: real bugs with lower blast radius, resilience gaps                          | Should fix; defer only with clear plan |
| P2     | Hardening or minor improvement                                                         | Optional follow-up                     |
| P3     | Nit: style or formatting preference                                                    | Can ignore                             |

**Calibration:**

- P0 blocks merge only after the Pass B P0 bar (full verify + exploit/break path today with `file:line`). `needs-runtime` without code proof is not P0.
- One structural finding outweighs ten nits; order and cap accordingly.
- Structural smells default to P2/maintainability; P1 only when the change worsens structure today (more concepts, feature logic into shared, clear boundary break).
- Clarity is comprehension, not LOC; naming/layout are typically P3; P2 only with a concrete navigation or consistency win.
- Structural findings name a remedy (see `../remedies.md`) or mark follow-up with high `regression_risk`.
- If more than 5 combined P2/P3 items remain, keep only the most impactful; P3 max 3.
- Legitimate hardening (CSP, HSTS, pagination, `.catch()` on floating promise, defensive `try/finally`) is follow-up, not blocker.

## Security classification

For each security finding, also classify:

| Level    | Meaning                                                 |
| -------- | ------------------------------------------------------- |
| CRITICAL | Exploitable in production with high impact today        |
| HIGH     | Significant risk with a concrete path; needs prompt fix |
| MEDIUM   | Defense-in-depth gap, lower immediate risk              |

Include: scenario, impact, data provenance, recommended mitigation. Report secrets as `file:line` + type only.

## Required fields per finding

1. Exact **file:line**
2. **Category** (vulnerability/bug, hardening, maintainability)
3. **Why it is exploitable/breaks** — concrete path with a pointable line
4. **Data provenance** when it is a security issue
5. **Severity** per tables above
6. **Proposed fix** — minimal and local when possible; consistent with existing logic and intentional design. If not verified to compile/pass, say so.
7. **regression_risk** — callers, contracts, tests, or Phase 1 "what must NOT change" the fix could alter. If a safe fix is not local, mark structural risk and prefer follow-up over a must-fix structural change.
8. **verification_note** — why it survived Pass B

## Regression gate (on suggested fixes)

- Prefer a **minimal local fix** over a broad refactor
- Name what must stay true after the fix
- Structural or cross-cutting fixes → follow-up unless the finding is P0 and no local fix exists

## Approval standard

Approve (or Approve with follow-ups) when there is no verified P0, even if P2/P3 remain. Do not block solely because the change is not how you would have written it.

## Completion criterion

Every surviving finding has all required fields including `regression_risk`. P2/P3 counts respect calibration caps. Dropped counts from Phase 2.5 remain available for the summary.
