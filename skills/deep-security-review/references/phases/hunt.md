# Phase 2 — Hunt

Dispatch domain hunters. Orchestrator reads this file to build prompts; each subagent receives only its domain + optional shape paths from the manifest.

## Dispatch

- Always: AuthZ, Injection, Secrets, Infra — **in parallel**
- Optional 5th: Business & LLM when `llm` / `sensitive` tags or high-value flows
- No shared findings until Phase 3
- Pass: scope, threat-model summary (compact), exact reference paths

## Subagent prompt template

```text
Hunt security findings in [scope] from the [DOMAIN] perspective only.

Threat model (from Phase 1):
[assets / actors / entry points / trust boundaries / abuse goals]

References (read ONLY these files, then hunt in code — max 2):
- [domain path]
- [shape path or "none"]

Before flagging anything:
- Read the entire cited file, not just a diff snippet.
- Read middleware / auth helpers / validators / shared config before flagging a route.
- Trace the full data path from entry to sink (or final output).
- Classify data provenance: direct user input, LLM content, or backend value.
- Prefer proven exploit paths over speculative Medium findings.

Return CandidateFinding list (YAML or bullets):
- location: file:line
- domain: AuthZ | Injection | Secrets | Infra | BusinessLLM
- title: short title
- category_hint: vulnerability | hardening
- exploit_path: why exploitable TODAY (concrete attacker path)
- data_provenance: user | llm | backend
- impact: what the attacker gains
- evidence_level: proven | likely | needs-runtime
- suggested_fix: minimal, local when possible

Do not open other files under references/. Do not review outside your domain.
Do not assign final P0/P1/P2/P3 severity.
```

## Domain scopes (one line each)

| Domain         | Hunt for                                                                                          |
| -------------- | ------------------------------------------------------------------------------------------------- |
| AuthZ          | Sessions/JWT/OAuth/API keys; object- and function-level access; tenant isolation; mass assignment |
| Injection      | SQL/NoSQL/command/path/XSS/CSRF; SSRF; XXE; deserialization; uploads; schema validation           |
| Secrets        | Hardcoded secrets; log/error/bundle leakage; PII; cookies/CORS/CSP; cache leakage                 |
| Infra          | IAM; CI/CD; deps/supply chain; rate limits; containers; deployment defaults                       |
| Business & LLM | Races; payment/wallet bypass; prompt injection; tool permissions; sensitive context leakage       |

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

Every dispatched domain has returned. Each candidate includes `location`, `exploit_path`, `data_provenance`, and `evidence_level`.
