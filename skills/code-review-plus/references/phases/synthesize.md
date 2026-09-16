# Phase 3 — Synthesize

Assign categories, severity, and required finding fields after Pass B verification.

If Phase 1 marked lockfile in source, read `../dependency-review.md` and fold dependency findings that survive the same evidence bar.

## Steps

1. Take `kept` and `downgraded` candidates from Phase 2.5, plus dependency-review items that pass the same evidence bar when that file was opened
2. Deduplicate: same `file:line` + same cause = one finding
3. Categorize: assign exactly one category
4. Prioritize: map category + impact to P0/P1/P2/P3
5. Attach **regression_risk** on every kept finding's suggested fix
6. Self-consistency: "What Looks Good" agrees with findings
7. Strengths: 1–2 specific wins that do not contradict findings, or omit the section
8. Tests in source **and** Quality in `Pipelines`: answer the three Test quality questions (useful / efficient / removable)
9. Verified unused code (all consumers checked) goes to Dead Code, not P0–P3, unless it also breaks behavior today
10. Copy `quality_source` from the Quality hunter when Quality ran

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
| P3     | Nit: small maintainability cost (naming/layout with a concrete but minor win)          | Can ignore                             |

**Calibration:**

- P0/P1 require **proven** (P0 bar in verify.md). Surviving `likely` is P2 hardening or lower.
- Every `kept` / `downgraded` finding goes in the report. Order by impact.
- Structural default P2; P1 when this change worsens structure today. Name a remedy from `../remedies.md` or mark follow-up with high `regression_risk`.
- Quality with today's cost is P2/P3 maintainability. Complexity scores: `../complexity.md`.
- Hardening (CSP, HSTS, pagination, `.catch()` on a floating promise) is follow-up, not a merge block.

## Security classification

For each security finding, also classify:

| Level    | Meaning                                                 |
| -------- | ------------------------------------------------------- |
| CRITICAL | Exploitable in production with high impact today        |
| HIGH     | Significant risk with a concrete path; needs prompt fix |
| MEDIUM   | Defense-in-depth gap, lower immediate risk              |

Include: scenario, impact, data provenance, recommended mitigation.

## Required fields per finding

1. Exact **file:line**
2. **Category** (vulnerability/bug, hardening, maintainability)
3. **Why it is exploitable/breaks/costs today** — concrete path with a pointable line
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

Approve (or Approve with follow-ups) when there is no verified P0, even if P2/P3 remain. Preference without today's cost stays off the report.

## Completion criterion

Every surviving finding has all required fields including `regression_risk` and appears in the report. Dropped counts from Phase 2.5 remain available for the summary. `quality_source` is ready for the report when Quality ran.
