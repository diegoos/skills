# Phase 2 — Hunt

Dispatch domain hunters. Orchestrator reads this file to build prompts; each subagent receives only its domain + optional shape paths from the manifest.

## Dispatch

- Always: AuthZ, Injection, Secrets, Infra — **in parallel**
- Optional 5th: BusinessLLM when **any** signal is true:
  - shape tags include `llm` or `sensitive`
  - hotspots or `abuse_goals` name payment, wallet, billing, payout, refund, or checkout
  - threat model or hotspots name LLM tools, RAG, MCP, agents, or prompt pipelines
  - scoped surface includes admin/privileged agent tools or package-publish flows
- No shared findings until Phase 3
- Pass: scope, threat-model summary (compact), hotspots, bypasses, auth_model, exact reference paths

## How to hunt

Work the hotspots and bypasses first. Lead with these angles (dense list — apply, do not essay):

sad path · trust boundaries · broken assumptions · ordering · races · parser disagreement · round-trip · config overrides · privilege · leaked context · unverified claims

## Universal moves

Apply on every domain (SSOT here — domains do not restate):

- Incomplete-fix siblings — one path patched, a twin left open
- Asymmetric trust between roles — A trusts B’s word without re-check
- Shape validated without authority — schema passes, ownership never checked

## Soft silo

Hunt primarily in the assigned domain. An incidental **proven** finding may leave with the canonical `domain` enum; do not open extra references or start a second hunt. Phase 3 dedupes.

## Pass A — hunter self-check

Raise a vulnerability candidate only when all are true:

- `evidence_level` is `proven` or `likely` (use `needs-runtime` only when the code path is real but deploy/config proof is missing — Phase 3 routes it out of Findings P0–P3)
- `exploit_path` names a concrete attacker path with a pointable line **today**
- Middleware / shared guards / validators were read before flagging a route
- Data provenance is classified (user / llm / backend)
- Speculative "if in the future" risks are omitted or marked hardening — not vulnerability
- A control you would praise as working is not also flagged as missing on the same path

Drop the candidate yourself if Pass A fields are missing or the claim is speculative. Default `category_hint` to `vulnerability`; Phase 3 owns hardening downgrades.

## Subagent prompt template

```text
Hunt security findings in [scope] from the [DOMAIN] perspective primarily.

Threat model (from Phase 1):
[assets / actors / entry points / trust boundaries / abuse_goals]
auth_model: [one sentence]
hotspots: [1–15 paths/flows]
bypasses: [list or "none found"]

References (read ONLY these files, then hunt in code — max 2):
- [domain path]
- [shape path or "none"]

How to hunt: sad path, boundaries, assumptions, ordering, races, parser disagreement, round-trip, config, privilege, leaked context, unverified claims.
Universal moves: incomplete-fix siblings; asymmetric trust between roles; shape validated without authority.

Before flagging anything (Pass A):
- Read the entire cited file, not just a diff snippet.
- Read middleware / auth helpers / validators / shared config before flagging a route.
- Trace the full data path from entry to sink (or final output).
- Classify data provenance: direct user input, LLM content, or backend value.
- Raise vulnerability candidates only at evidence_level proven or likely with a pointable line today.
- Omit speculative "if in the future" paths; hardening gaps wait for Phase 3.
- If a control works on the path, leave it unflagged (self-consistency with strengths).
- Default category_hint to vulnerability; Phase 3 owns hardening downgrades.

Return CandidateFinding list (YAML or bullets):
- location: file:line
- domain: AuthZ | Injection | Secrets | Infra | BusinessLLM
- title: short title
- category_hint: vulnerability | hardening
- exploit_path: why exploitable TODAY (concrete attacker path)
- data_provenance: user | llm | backend
- impact: what the attacker gains
- evidence_level: proven | likely | needs-runtime
- suggested_fix: minimal, local when possible; fail-closed; do not weaken auth/validation

Do not open other files under references/.
Do not assign final P0/P1/P2/P3 severity.
```

## Domain scopes (one line each)

| Domain      | Hunt for                                                                                          |
| ----------- | ------------------------------------------------------------------------------------------------- |
| AuthZ       | Sessions/JWT/OAuth/API keys; object- and function-level access; tenant isolation; mass assignment |
| Injection   | SQL/NoSQL/command/path/XSS/CSRF; SSRF; XXE; deserialization; uploads; schema validation           |
| Secrets     | Hardcoded secrets; log/error/bundle leakage; PII; crypto; cookie/transport exposure               |
| Infra       | IAM; CI/CD; deps/supply chain; rate limits; containers; deployment defaults                       |
| BusinessLLM | Races; payment/wallet bypass; prompt injection; tool permissions; boundary-crossing               |

Full checklists live in `./references/domains/*.md`. Shape-specific probes live in `./references/shapes/*.md`.

## CandidateFinding schema

```yaml
location: path/file.ts:42
domain: AuthZ
title: Missing tenant scope on invoice fetch
category_hint: vulnerability
exploit_path: Authenticated user changes invoice id → loads another tenant row
data_provenance: user
impact: Cross-tenant billing data exposure
evidence_level: proven
suggested_fix: Query by id + tenantId; add cross-tenant 403/404 test
```

## Completion criterion

Every dispatched domain has returned. Each candidate includes `location`, `domain`, `exploit_path`, `data_provenance`, and `evidence_level`. Vulnerability candidates meet the Pass A bar (`proven`/`likely` with a pointable line today) or were self-dropped by the hunter.
