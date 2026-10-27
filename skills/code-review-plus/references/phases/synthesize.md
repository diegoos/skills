# Phase 3 — Synthesize

Assign categories, severity, and required finding fields after Pass B verification.

If Phase 1 marked lockfile in source, read `./references/dependency-review.md` and fold dependency findings that survive the same evidence bar.

## Steps

1. Take `kept` and `downgraded` candidates from Phase 2.5, plus dependency-review items that pass the same evidence bar when that file was opened
2. Deduplicate: same `file:line` + same cause = one finding
3. Categorize: assign exactly one category
4. Prioritize: map category + impact to P0/P1/P2/P3
5. Origin: a finding that matches a `Prior findings` entry (same file and cause) is `prior <old ID>`; every other finding is `new`
6. Re-check each `open` prior finding that no finding matched and whose Perspective is in `Pipelines`: re-read its `file:line` and callers. Break holds → carry it with its prior severity, category, and details (derive missing ones from the re-read), Origin `prior <old ID>`, and a `verification_note`. Break gone → count it as closed since the prior review. Carry every other unmatched `open` prior finding unchanged, with Origin `prior <old ID>, not re-checked`. `closed` and `known` prior findings are not carried
7. In a `Closed paths` file, keep a `new` finding only at P0/P1; count the rest as dropped
8. Attach **regression_risk** on every kept finding's suggested fix
9. Strengths: 1–2 specific wins that do not contradict findings, or omit the section
10. Tests in source **and** Quality in `Pipelines`: answer the three Test quality questions (useful / efficient / removable)
11. Verified unused code (all consumers checked) goes to Dead Code, not P0–P3, unless it also breaks behavior today
12. Copy `quality_source` from the Quality hunter when Quality ran
13. When `Prior findings` is not `none`, count carried, closed since, and new findings for the Review Summary

## Categories

| Category                         | Definition                                                                      | Typical severity |
| -------------------------------- | ------------------------------------------------------------------------------- | ---------------- |
| **Vulnerability**                | Exploitable security issue today, with a pointable line                         | P0/P1            |
| **Bug**                          | Reproducible breakage today, with a pointable line                              | P0/P1            |
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
- Structural default P2; P1 when this change worsens structure today. Name a remedy from `./references/remedies.md` or mark follow-up with high `regression_risk`.
- Quality with today's cost is P2/P3 maintainability. Complexity scores: `./references/complexity.md`.
- Hardening (CSP, HSTS, pagination, `.catch()` on a floating promise) is follow-up, not a merge block.
- An authorization bypass with a concrete data or privilege gain is P1 or higher.

## Required fields per finding

1. Exact **file:line**
2. **Category** (vulnerability, bug, hardening, maintainability)
3. **Why it is exploitable/breaks/costs today** — concrete path with a pointable line
4. **Data provenance** when it is a security issue
5. **Severity** per tables above
6. **Proposed fix** — minimal and local when possible; consistent with existing logic and intentional design. If not verified to compile/pass, say so.
7. **regression_risk** — callers, contracts, tests, or Phase 1 "what must NOT change" the fix could alter. If a safe fix is not local, mark structural risk and prefer follow-up over a must-fix structural change.
8. **verification_note** — why it survived Pass B
9. **Origin** — `new` or `prior <old ID>`

## Regression gate (on suggested fixes)

- Prefer a **minimal local fix** over a broad refactor
- Name what must stay true after the fix
- Structural or cross-cutting fixes → follow-up unless the finding is P0 and no local fix exists

## Approval standard

Request changes when a verified P0 exists. With a verified P1 and no P0, choose Request changes or Approve with follow-ups by the P1's impact on this merge, and state the reason in the Verdict. Otherwise Approve, or Approve with follow-ups when P2/P3 remain. Carried prior findings count like new ones. Findings with Origin `prior <old ID>, not re-checked` stay in the table and out of the verdict. Preference without today's cost stays off the report.

## Completion criterion

Every surviving finding has all required fields including `regression_risk` and Origin, and appears in the report. Every `open` prior finding is matched, carried, or counted as closed. Dropped counts from Phase 2.5 remain available for the summary. `quality_source` is ready for the report when Quality ran.
