# Phase 3 — Verify & Synthesize

Reject false positives after all hunters return. Single source of truth for severity, status routing, and required finding fields. Only candidates that survive **Pass B** (and re-verify when required) enter the report as Findings.

**Gates and FP patterns:** when keep/drop is unclear, or before keep when a confirmation gate or recurring FP pattern applies, read `../examples/kept-vs-dropped.md`. That file is SSOT for gates, the FP table, and worked keep/drop cases.

## Leading words

- **Pass B** — three questions on every candidate; `verification_note` cites what was re-read
- **needs-runtime** — unsettled without deployed config, logs, or live traffic (never P0)

## Pass A — hunter fields (orchestrator intake)

Before Pass B, drop immediately if a candidate is missing `location`, `exploit_path`, `data_provenance`, or `evidence_level`, or if a vulnerability claim is speculative (no pointable line today). Extra-floor extras still `likely` → drop (or downgrade to hardening). `needs-runtime` never enters Findings as P0–P3 — route to Verification Gaps.

## Pass B — validator

Re-open `file:line` plus callers, middleware, shared helpers, and consumers as needed. Three questions on **every** remaining candidate:

1. Does the exploit path hold today at lowest practical privilege, with a pointable `file:line`? Falsify: existing mitigation at a cited line, parser/runtime defaults, missing material impact.
2. Does this contradict another candidate or a likely "What Looks Good" strength?
3. Would the suggested fix pass the **regression gate** (minimal, local, fail-closed)?

Drop or downgrade any item that fails. Future-only risks become P2 hardening, not Findings blockers. Apply confirmation gates and the recurring FP table from `kept-vs-dropped.md` when a pattern matches.

`likely` with a pointable line: re-read. Confirm → **proven**. Line holds but the path is still incomplete → keep as P2 hardening (not P0/P1). No line today → drop.

Pass B is complete only when `verification_note` cites what was re-read (`file` plus callers / middleware / helpers as needed). A note with no citation is not Pass B.

## P0 bar

A candidate may become P0 only if Pass B is complete and the exploit path is reconfirmed today with a pointable `file:line`. P0 and P1 require `evidence_level: proven`. `needs-runtime` without code proof is never P0.

## Synthesize steps

1. Verify — Pass A intake + Pass B + gates/FP file when applicable; drop or downgrade failures
2. Deduplicate — merge overlapping findings across domains
3. Categorize — assign exactly one category
4. Prioritize — map kept vulns to P0–P3 (security level follows 1:1); downgraded hardening is P2 in Overview
5. Self-consistency — no contradictions with "What Looks Good"
6. Gaps — skipped domains / needs-runtime / fail-open AuthZ / missing security audit-or-alert on high-risk paths called out
7. Strengths — note 1–2 specific controls done well
8. Re-verify (conditional) — see below

## Status routing

| Status       | Meaning                                                  | Report section                       |
| ------------ | -------------------------------------------------------- | ------------------------------------ |
| `kept`       | Current vulnerability with an exploitable path today     | Findings Overview (P0–P3)            |
| `downgraded` | Defense-in-depth, not exploitable today                  | Findings Overview as P2 `hardening`  |
| `dropped`    | False positive / disproved                               | Count only — omit narrative          |

Process / `needs-runtime` items go to Verification Gaps (evidence routing, not a fourth status). One item appears in exactly one report section. Record counts `{kept, downgraded, dropped}`.

## Categories

| Category                         | Definition                                       | Typical severity  |
| -------------------------------- | ------------------------------------------------ | ----------------- |
| **Current vulnerability**        | Exploitable **today**, with a pointable line     | P0–P3 (kept)      |
| **Hardening / defense-in-depth** | Not exploitable today; protects future evolution | P2 in Overview    |
| **Process / residual risk**      | Missing tests, tooling, or runtime evidence      | Verification Gaps |

## Severity (kept vulnerabilities only)

Assign **P0–P3** from likelihood × impact in prose. Security level is derived 1:1 — never invent a mismatch:

| P   | Security level | Meaning                                                                       | Author action                    |
| --- | -------------- | ----------------------------------------------------------------------------- | -------------------------------- |
| P0  | CRITICAL       | Verified critical — account/tenant/secret/payment compromise or RCE **today** | Must fix before merge            |
| P1  | HIGH           | Real vuln with lower blast radius, or clear authz/injection gap               | Should fix; defer only with plan |
| P2  | MEDIUM         | Real vuln with limited impact                                                 | Optional follow-up               |
| P3  | LOW            | Current low-risk issue (not speculative hardening)                            | Can ignore                       |

**Calibration:** P0 blocks merge — demonstrated only after the P0 bar. Prefer one well-supported High over many speculative Mediums. Explicit AuthZ boundary defeat with concrete consequence → minimum HIGH / P1+. `likely` that does not confirm on re-read is P2 hardening or drop. `needs-runtime` never receives P0–P3 — route to Verification Gaps. Hardening that is not exploitable today is P2 in Overview, labeled `hardening`.

## VerifiedFinding fields

1. Exact **file:line**
2. **Category** (vulnerability / hardening / process)
3. **Why it is exploitable** — concrete attacker path
4. **Data provenance**
5. **Severity** (P0–P3) — kept vulns and P2 hardening; Overview has no separate Security column
6. **Evidence level** (proven / likely / needs-runtime)
7. **Proposed fix** — local when possible; say if unverified to compile/pass
8. **regression_risk** — one line: callers / contracts / tests / `intended_behavior` the fix could touch
9. **verification_note** — files and callers/middleware re-read, then why it survived or failed
10. **drop_reason** — required when `dropped` or `downgraded`

**Required for kept P0/P1 vulnerabilities:** `trace` (multi-step entry → gain), `intended_behavior`, `trigger_sketch`, `regression_risk`.

```yaml
status: kept | dropped | downgraded
drop_reason: # required when dropped or downgraded
verification_note: # files and callers/middleware re-read, then why it survived or failed
trace: optional # required for kept P0/P1 vulns
intended_behavior: optional # required for kept P0/P1 vulns
trigger_sketch: optional # required for kept P0/P1 vulns
regression_risk: optional # required for kept P0/P1 vulns
# plus all VerifiedFinding fields when kept/downgraded
```

## Re-verify (inside Phase 3 — not a new phase)

After Pass B, if **≥1** remaining candidate could still be P0 (P0 bar met), the orchestrator **dispatches** **one** independent verifier when either trigger is true:

1. Residual ambiguity (middleware vs route, framework/parser default, `needs-runtime` borderline), or
2. **≥2** candidates still look like P0 after Pass B

**Also dispatch** when a kept P1 depends on an unknown framework/parser default.

**Skip when:** zero P0-capable candidates remain, or Pass B settled every P0-capable candidate without residual ambiguity and there is at most one such candidate, and no kept P1 depends on an unknown framework/parser default. Record `reverify: skipped` (reason) when no dispatch trigger fires.

Verifier re-reads cited files and applies the same Pass B questions; returns only `status` + `verification_note` (+ `drop_reason`); may only drop or downgrade; does not invent findings or assign final severity.

## Verification probes (shared)

- Auth: unauthenticated → `401`
- AuthZ: wrong tenant/user → `403`/`404`
- AuthZ fail-open: auth dependency error on a protected request → deny (not allow)
- Validation: malformed input → `400`, no mutation
- Injection: payload treated as data
- Rate limit: abuse-prone flows → `429`
- Secrets: none in logs/errors/client bundles
- Audit/alert: auth failures and high-risk actions leave an auditable trail (gap → Verification Gaps, not Findings, without an exploit path)
- LLM tools: prompt cannot call unauthorized tools or cross-tenant data; a tool cannot reach a sink the caller cannot reach via the normal API

## Completion criterion

Every candidate has `status` and a `verification_note` that cites the files/callers re-read (`drop_reason` when dropped/downgraded). Surviving Findings have all required fields (including P0/P1 `trace` / `intended_behavior` / `trigger_sketch` / `regression_risk` when kept). `{kept, downgraded, dropped}` counts recorded. Re-verify ran or `skipped` documented. P0 candidates that fail the P0 bar are downgraded or marked unverified. P0/P1 kept findings are `proven`.
