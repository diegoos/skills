# Phase 2 — Hunt

Dispatch domain hunters. Orchestrator reads this file to build prompts; each hunter receives its domain + optional shape paths from the manifest.

## Hunt bar

Cover the domain (and shape) as a **floor**, then emit any other in-domain issue when **today**'s exploit path is **proven** at `file:line`. Floor items may be `likely`; Phase 3 confirms. Extra-floor extras are `proven` only. P0/P1 require **proven**. An empty list is valid when this domain found nothing.

## Dispatch

- Always: AuthZ, Injection, Secrets, Infra — **in parallel** when the harness has a subagent
- Optional 5th: BusinessLLM when **any** signal is true:
  - shape tags include `llm` or `sensitive`
  - hotspots or `abuse_goals` name payment, wallet, billing, payout, refund, or checkout
  - threat model or hotspots name LLM tools, RAG, MCP, agents, or prompt pipelines
  - scoped surface includes admin/privileged agent tools or package-publish flows
- No shared findings until Phase 3
- Pass: scope, threat-model summary (compact), hotspots, bypasses, auth_model, exact reference paths

## Serial fallback (no subagent)

If the harness has no subagent, run the dispatched domains **in series** (one domain at a time). Record `serial: yes` in the report only when **two or more** domains ran in series. One domain: omit `serial:`.

**Carry list.** After each domain returns, append each candidate's `location`, `title`, and `domain`. A domain with no candidates still records `domain: … (none)`. Restate that compact list before starting the next domain. Auto-compact drops earlier hunts: restore from that restated list first, then continue. Mid-series with no restated block for a finished domain is a failed dispatch; rebuild from the last restated block before the next hunt.

Carry is orchestrator storage. The next hunter still receives only its own domain (prompt template below). Deduplicate in Phase 3.

## How to hunt

Work the hotspots and bypasses first. Lead with these angles (dense list — apply, do not essay):

sad path · trust boundaries · broken assumptions · ordering · races · parser disagreement · round-trip · config overrides · privilege · leaked context · unverified claims · **chained layers**

**chained layers** — untrusted prompt/RAG → tool/MCP → sink, including a utility with no HTTP route. The sequence is the finding when each layer works as designed and the caller still gains what the normal API denies.

## Universal moves

Apply on every domain (SSOT here — domains do not restate):

- Incomplete-fix siblings — one path patched, a twin left open
- Asymmetric trust between roles — A trusts B’s word without re-check
- Shape validated without authority — schema passes, ownership never checked
- Exceptional conditions — empty/swallow catch; missing param that still writes; catch without resource release; fail-open on the error path

## Soft silo

Hunt primarily in the assigned domain. An incidental **proven** finding may leave with the canonical `domain` enum. Phase 3 dedupes.

## Pass A — hunter self-check

Raise a vulnerability candidate when all are true:

- Floor items: `evidence_level` is `proven` or `likely`. Extra-floor items: `proven` only (`needs-runtime` when the code path is real but deploy/config proof is missing — Phase 3 routes it out of Findings P0–P3)
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

Skill files (load these, then hunt in code):
- [domain path]
- [shape path or omit this line]

Cover the **floor** (`likely` allowed). Extra-floor in-domain issues: **proven** only. An empty list is valid when this domain found nothing.
suggested_fix is local; regression_risk is one line.

How to hunt: sad path, boundaries, assumptions, ordering, races, parser disagreement, round-trip, config, privilege, leaked context, unverified claims, chained layers.
Universal moves: incomplete-fix siblings; asymmetric trust between roles; shape validated without authority; exceptional conditions (empty catch, missing param that still writes, catch without resource release, fail-open).

Before flagging anything (Pass A):
- Read the entire cited file, not just a diff snippet.
- Read middleware / auth helpers / validators / shared config before flagging a route.
- Trace the full data path from entry to sink (or final output). For chained layers, include prompt/RAG → tool/MCP → sink even when no HTTP route reaches the sink.
- Classify data provenance: direct user input, LLM content, or backend value.
- Raise floor candidates at evidence_level proven or likely with a pointable line today. Extra-floor extras: proven only.
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
- suggested_fix: minimal, local when possible; fail-closed
- regression_risk: callers / contracts / tests / intended_behavior the fix could touch

Stay in this domain. Leave P0–P3 to synthesize.
Review is read-only. Same model as the orchestrator.
```

## Domain scopes (one line each)

| Domain      | Hunt for                                                                                          |
| ----------- | ------------------------------------------------------------------------------------------------- |
| AuthZ       | Sessions/JWT/OAuth/API keys; object- and function-level access; tenant isolation; mass assignment |
| Injection   | SQL/NoSQL/command/path/XSS/CSRF; SSRF; XXE; deserialization; uploads; schema validation           |
| Secrets     | Hardcoded secrets; log/error/bundle leakage; PII; crypto; cookie/transport exposure               |
| Infra       | IAM; CI/CD; deps/supply chain; rate limits; containers; deployment defaults                       |
| BusinessLLM | Races; payment/wallet bypass; prompt injection; tool permissions; chained layers                  |

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
regression_risk: 403/404 shape for this route; existing happy-path tenant tests
```

## Completion criterion

Every dispatched domain has returned (an empty CandidateFinding list is valid when that domain found nothing). Each candidate includes `location`, `domain`, `exploit_path`, `data_provenance`, `evidence_level`, and `regression_risk`. Floor vulnerability candidates meet the Pass A bar (`proven`/`likely` with a pointable line today) or were self-dropped; extra-floor extras are `proven`. Serial fallback with two or more domains: the compact carry list holds every finished domain before the next hunt starts.
