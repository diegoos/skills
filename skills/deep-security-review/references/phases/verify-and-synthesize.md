# Phase 3 — Verify & Synthesize

Reject false positives after all hunters return. Single source of truth for severity, confirmation gates, and required finding fields. Only candidates that survive disprove (and optional re-verify) enter the report as Findings.

When keep/drop is unclear, read `../examples/kept-vs-dropped.md` (do not preload).

## Leading words

- **disprove** — active attempt to falsify a candidate before keep
- **needs-runtime** — unsettled without deployed config, logs, or live traffic (never P0)

## Pass A — hunter fields (orchestrator intake)

Before disprove, drop immediately if a candidate is missing `location`, `exploit_path`, `data_provenance`, or `evidence_level`, or if a vulnerability claim is speculative (no pointable line today). `needs-runtime` never enters Findings as P0–P3 — route to Verification Gaps.

## Verify checklist (every remaining candidate)

```text
- [ ] Entire cited file read (not just a snippet)?
- [ ] Shared authz/validation middleware checked before flagging a route?
- [ ] Data provenance stated (user / LLM / backend)?
- [ ] Entry → sink / final output traced?
- [ ] Exact line that makes this exploitable TODAY pointable?
- [ ] Framework / library defaults verified before asserting failure modes?
- [ ] Intentional design comments respected (not contradicted)?
- [ ] Reproducible by reading code without "if in the future"?
- [ ] Self-consistent with other candidates and likely "What Looks Good" strengths?
- [ ] Proposed fix local, fail-closed, and does not weaken auth/validation/error paths?
- [ ] Evidence level stated (proven / likely / needs-runtime)?
```

Drop or downgrade any item that fails. Future-only risks become hardening, not Findings blockers.

## Disprove

Before keep, falsify each candidate on: (1) exploitation at lowest practical privilege, (2) material impact, (3) existing mitigation at a cited line, (4) parser/runtime defaults changing the outcome. Survivors stay `kept`. Failures become `dropped` or `downgraded` with evidence in `verification_note` and required `drop_reason`.

## P0 bar

A candidate may become P0 only if disprove is complete and the exploit path is reconfirmed today with a pointable `file:line`. `needs-runtime` without code proof is never P0.

## Confirmation gates (SSOT)

| Gate                                | Keep only when                                                                |
| ----------------------------------- | ----------------------------------------------------------------------------- |
| Parser / framing disagreement       | Two components + divergent parse with concrete cross-boundary effect          |
| Token / JWT claim                   | Verify line present **and** a required claim missing or unchecked             |
| Host / cache                        | Cross-user or cross-tenant impact demonstrated                                |
| Mitigating layer already blocks     | Downgrade to hardening (not keep as vuln)                                     |
| Unknown library / framework default | `needs-runtime` or unverifiable — do not invent P0/P1                         |
| AuthZ fail-open on error path       | Reachable error path **and** concrete privilege or data consequence           |
| Second-order / chained injection    | Both store and later sink proven; otherwise one finding or drop the weak half |

## Recurring false positives

| Pattern                                                                           | Why it is usually wrong                                                              |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Route "missing auth" when global middleware covers it                             | Check middleware / shared guards / matcher first                                     |
| "Missing CSRF" without framework defaults + cookie `SameSite`                     | Verify the actual CSRF strategy                                                      |
| ORM use treated as always-safe                                                    | Flag only when raw/dynamic queries are unsafe                                        |
| Schema/allowlist already strips privileged fields                                 | Mass-assignment FP — confirm the field reaches persistence                           |
| TypeScript types as runtime validation                                            | Types are not a control                                                              |
| LLM system prompt as access control                                               | Server must enforce tool/data permissions                                            |
| Helper named `auth()` treated as authorization                                    | AuthN ≠ AuthZ; require ownership/tenant proof                                        |
| XSS while final output escapes and unescapes only fixed literals                  | Not exploitable today — hardening at most                                            |
| Self-XSS only (attacker must paste into own session)                              | Drop unless it becomes stored/reflected for another user                             |
| `credentials: "include"` as cross-origin cookie leak                              | Browser sends cookies only for the destination origin                                |
| CORS `*` without credentials                                                      | Often intentional for public reads — keep only with credentialed or sensitive impact |
| Incomplete security headers / missing CSP with no exploit path                    | Hardening note, not vulnerability                                                    |
| Open redirect when redirect URI/host is allowlisted                               | Confirm allowlist is enforced server-side                                            |
| SSRF when URL is constant or allowlisted after DNS+redirects                      | Confirm rebind/TOCTOU actually bypasses the check                                    |
| GraphQL introspection "enabled" without checking production config                | Verify the deployed/prod path                                                        |
| Dependency CVE / advisory without reachability                                    | Triage via call graph / prod vs devDependency — else process/gap                     |
| IDOR when query already scopes by owner/tenant                                    | Re-read the data access line before keep                                             |
| Missing rate limit without an abuse-prone flow                                    | Hardening unless stuffing/spray path is concrete                                     |
| Missing cookie flags on a non-session / non-sensitive cookie                      | Drop or hardening                                                                    |
| JWT claim nit (`nbf` only) without forge/escalation path                          | Downgrade unless verify is missing or alg/key confused                               |
| Scanner finding (SAST/DAST) without a code-backed exploit path                    | Cite `file:line` or drop                                                             |
| P0 from "if in the future" / "any evolution could"                                | Future risk is hardening                                                             |
| Praise a global control in "What Looks Good" and flag the same control as missing | Self-consistency — drop one of them                                                  |
| suggested_fix that relaxes auth, validation, or error handling                    | Over-simplify — rewrite the fix fail-closed                                          |

## Synthesize steps

1. Verify — Pass A intake + checklist + disprove; drop or downgrade failures
2. Deduplicate — merge overlapping findings across domains
3. Categorize — assign exactly one category
4. Prioritize — map kept vulns to P0–P3 and CRITICAL–LOW
5. Self-consistency — no contradictions with "What Looks Good"
6. Gaps — skipped domains / needs-runtime / fail-open AuthZ called out
7. Strengths — note 1–2 specific controls done well
8. Re-verify (conditional) — see below

## Status routing

| Status       | Meaning                                                  | Report section                       |
| ------------ | -------------------------------------------------------- | ------------------------------------ |
| `kept`       | Current vulnerability with an exploitable path today     | Findings (P0–P3)                     |
| `downgraded` | Defense-in-depth or residual risk, not exploitable today | Hardening notes or Verification Gaps |
| `dropped`    | False positive / disproved                               | Count only — omit narrative          |

One item appears in exactly one report section. Record counts `{kept, downgraded, dropped}`.

## Categories

| Category                         | Definition                                       | Typical severity  |
| -------------------------------- | ------------------------------------------------ | ----------------- |
| **Current vulnerability**        | Exploitable **today**, with a pointable line     | P0–P3 (kept)      |
| **Hardening / defense-in-depth** | Not exploitable today; protects future evolution | Hardening notes   |
| **Process / residual risk**      | Missing tests, tooling, or runtime evidence      | Verification Gaps |

## Severity (kept vulnerabilities only)

Likelihood × impact in prose feeds these tables — not a third scale.

| Prefix | Meaning                                                                       | Author action                    |
| ------ | ----------------------------------------------------------------------------- | -------------------------------- |
| P0     | Verified critical — account/tenant/secret/payment compromise or RCE **today** | Must fix before ship             |
| P1     | Real vuln with lower blast radius, or clear authz/injection gap               | Should fix; defer only with plan |
| P2     | Real vuln with limited impact                                                 | Optional follow-up               |
| P3     | Current low-risk issue (not speculative hardening)                            | Can ignore                       |

| Level    | Meaning                                                 | Typical P |
| -------- | ------------------------------------------------------- | --------- |
| CRITICAL | Exploitable in production with high impact **today**    | P0        |
| HIGH     | Significant risk with a concrete path; needs prompt fix | P1        |
| MEDIUM   | Limited-impact vuln                                     | P2        |
| LOW      | Low-risk current issue                                  | P3        |

**Calibration:** P0 blocks ship — demonstrated only after the P0 bar. Prefer one well-supported High over many speculative Mediums. Explicit AuthZ boundary defeat with concrete consequence → minimum HIGH / P1+. `needs-runtime` never receives P0–P3 — route to Verification Gaps.

## VerifiedFinding fields

1. Exact **file:line**
2. **Category** (vulnerability / hardening / process)
3. **Why it is exploitable** — concrete attacker path
4. **Data provenance**
5. **Severity** (P0–P3) and **security level** (CRITICAL–LOW) — kept vulns only
6. **Evidence level** (proven / likely / needs-runtime)
7. **Proposed fix** — local when possible; say if unverified to compile/pass
8. **verification_note** — confidence reason in prose (e.g. "middleware verified at file:line") or why it failed
9. **drop_reason** — required when `dropped` or `downgraded`

**Required for kept P0/P1 vulnerabilities:** `trace` (multi-step entry → gain), `intended_behavior`, `trigger_sketch`.

```yaml
status: kept | dropped | downgraded
drop_reason: # required when dropped or downgraded
verification_note: # why it survived or failed
trace: optional # required for kept P0/P1 vulns
intended_behavior: optional # required for kept P0/P1 vulns
trigger_sketch: optional # required for kept P0/P1 vulns
# plus all VerifiedFinding fields when kept/downgraded
```

## Re-verify (inside Phase 3 — not a new phase)

After disprove, if **≥1** remaining candidate could still be P0 (P0 bar met), the orchestrator **may** dispatch **one** independent verifier when either trigger is true:

1. Residual ambiguity (middleware vs route, framework/parser default, `needs-runtime` borderline), or
2. **≥2** candidates still look like P0 after disprove

**Skip when:** zero P0-capable candidates remain, or disprove settled every P0-capable candidate without residual ambiguity and there is at most one such candidate. Also dispatch when a kept P1 depends on an unknown framework/parser default. Record `reverify: skipped` (reason) when neither path fires.

Verifier re-reads cited files and applies the same gates; returns only `status` + `verification_note` (+ `drop_reason`); may only drop or downgrade; does not invent findings or assign final severity.

## Verification probes (shared)

- Auth: unauthenticated → `401`
- AuthZ: wrong tenant/user → `403`/`404`
- AuthZ fail-open: auth dependency error on a protected request → deny (not allow)
- Validation: malformed input → `400`, no mutation
- Injection: payload treated as data
- Rate limit: abuse-prone flows → `429`
- Secrets: none in logs/errors/client bundles
- LLM tools: prompt cannot call unauthorized tools or cross-tenant data

## Completion criterion

Every candidate has `status` and `verification_note` (`drop_reason` when dropped/downgraded). Surviving Findings have all required fields (including P0/P1 `trace` / `intended_behavior` / `trigger_sketch` when kept). `{kept, downgraded, dropped}` counts recorded. Re-verify ran or `skipped` documented. P0 candidates that fail the P0 bar are downgraded or marked unverified.
