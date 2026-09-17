# Phase 1 — Plan

Orchestrator-only. Build the threat model and `DispatchManifest` before any hunt.

## Leading words

- **hotspot** — concrete path or flow an attacker would hit first (up to 15 in the manifest; hunters still cover the assigned domain in scope)
- **bypass** — dev/debug/setup surface that can skip AuthZ or expose privileged actions
- **proven** — exploit path demonstrated by reading code at `file:line` today
- **needs-runtime** — claim that requires deployed config, logs, or live traffic to settle

## Threat model (minimum)

```text
- Assets: secrets, tokens, PII, payment data, tenant data, admin actions
- Actors: anonymous, authenticated, tenant admin, platform admin, third-party, malicious prompt
- Entry points: routes, APIs, webhooks, uploads, jobs, queues, WebSockets, CLIs
- Trust boundaries: browser/server, public/private, app/DB, app/LLM, LLM/tools, CI/runtime
- abuse_goals: 1–3 concrete attacker outcomes tied to hotspots (not a parallel abuse_cases list)
- auth_model: one sentence — how identity, session, and authority are established
- hotspots: up to 15 first-hit paths (small reviews: the scoped files themselves; hunters still cover the assigned domain)
- bypasses: dev/debug/setup surfaces, or `none found`
```

## Scope sources

| Source              | Action                                            |
| ------------------- | ------------------------------------------------- |
| Whole codebase      | Map entry points first; prioritize auth and money |
| Specific files      | Review those files in full trust-boundary context |
| Uncommitted changes | `git diff`                                        |
| Feature branch      | `git diff <base>...HEAD` (repo default base)      |
| Pasted code         | Review directly                                   |

## Detect shape tags (cheap signals — Phase 1 stays on this file)

| Signal                                                     | Tag          |
| ---------------------------------------------------------- | ------------ |
| `openapi`, `app/api`, `routes/`, GraphQL, webhooks, REST   | `api`        |
| `*.tsx`/`*.jsx`, `pages/`, `public/`, templates, SSR       | `web`        |
| `package.json`, `*.ts`/`*.js`, Node, Next, Nest            | `ts-js-node` |
| `pyproject.toml`, `requirements.txt`, Django, FastAPI      | `python`     |
| `composer.json`, `*.php`, Laravel, Symfony, WordPress      | `php`        |
| Dockerfile, Terraform, K8s, `.github/workflows`, cloud IaC | `cloud`      |
| LLM SDK, agents, RAG, MCP, tool-calling, prompt pipelines  | `llm`        |
| Stripe/billing/wallet/payments, package publish            | `sensitive`  |
| User asks to run scanners / audit CI / deps tooling        | `tooling`    |

Pick **at most one** language tag (`ts-js-node` | `python` | `php`). If polyglot, choose the language of the attack surface under review.

## Catalog (paths only)

| Tag / role             | File                                                |
| ---------------------- | --------------------------------------------------- |
| Domain AuthZ           | `./references/domains/authz.md`                     |
| Domain Injection       | `./references/domains/injection.md`                 |
| Domain Secrets         | `./references/domains/secrets.md`                   |
| Domain Infra           | `./references/domains/infrastructure.md`            |
| Domain Business & LLM  | `./references/domains/business-llm.md`              |
| Shape `api`            | `./references/shapes/api.md`                        |
| Shape `web`            | `./references/shapes/web.md`                        |
| Shape `ts-js-node`     | `./references/shapes/typescript-javascript-node.md` |
| Shape `python`         | `./references/shapes/python.md`                     |
| Shape `php`            | `./references/shapes/php.md`                        |
| Shape `cloud`          | `./references/shapes/cloud.md`                      |
| Shape `llm`            | `./references/shapes/llm.md`                        |
| Shape `sensitive`      | `./references/shapes/sensitive-flows.md`            |
| Shape `tooling`        | `./references/shapes/tooling.md`                    |
| Optional OWASP         | `./references/optional/owasp-map.md`                |
| Gates / FPs / examples | `./references/examples/kept-vs-dropped.md`          |
| Report sample          | `./references/examples/report-sample.md`            |

## Reference Plan algorithm

Each dispatched domain gets **slot 1 = its domain file** and **slot 2 = one shape** (or `"none"`).

| Domain         | Slot 2 candidates (walk until first match)   |
| -------------- | -------------------------------------------- |
| AuthZ          | dominant surface (`api` \| `web`) → language |
| Injection      | dominant surface → language                  |
| Secrets        | `web` (if set) → language                    |
| Infra          | `cloud` → `sensitive` → `tooling`            |
| Business & LLM | `llm` → `sensitive`                          |

**Dominant surface:** count entry points (API routes/webhooks vs browser pages). Prefer that tag. If tied: AuthZ/Injection prefer `api`; Secrets prefers `web`.

**OWASP:** only if the user asks for an OWASP map, or the stack is unknown and the surface is public HTTP. If used, it **replaces** slot 2 for AuthZ or Injection (still ≤2 files).

**Load:**

1. Phase 1 stays on this file. Domain and shape files wait for hunt.
2. Each hunter's **load** is the two paths listed for its domain (1 domain + 0 or 1 shape). Those files **complement** the hunt. After them, hunt in code; the model's security knowledge stays in play.
3. No matching tag for slot 2 → `"none"`.
4. Keep domains separate (one hunter each).
5. `examples/` is orchestrator-only (Phase 3 gates/FPs/worked cases, Phase 4 sample) — not a hunter path.

## Codebase sweeps (only `scope.type: codebase`)

Run two orchestrator sweeps that feed hotspots and bypasses — not an architecture document. Hunters still cover the assigned domain in scope:

1. Entry-point sweep — routes, APIs, webhooks, jobs, CLIs that touch auth or high-value data
2. Trust-boundary / bypass sweep — browser↔server, public↔private, app↔LLM/tools, CI↔runtime, plus dev/debug/setup surfaces

Other scope types derive hotspots and bypasses directly from the requested material.

## DispatchManifest schema

```yaml
scope:
  type: diff | branch | files | codebase | pasted
  ref: string
threat_model:
  assets: [string]
  actors: [string]
  entry_points: [string]
  trust_boundaries: [string]
  abuse_goals: [string] # 1–3 concrete outcomes tied to hotspots
  auth_model: string # one sentence: identity + session + authority
  hotspots: [string] # up to 15 first-hit paths; hunters still cover the assigned domain in scope
  bypasses: [string] # or ["none found"]
shape_tags: [api, web, ts-js-node] # example; ≤1 language
domains:
  AuthZ:
    - ./references/domains/authz.md
    - ./references/shapes/api.md
  Injection:
    - ./references/domains/injection.md
    - ./references/shapes/api.md
  Secrets:
    - ./references/domains/secrets.md
    - ./references/shapes/web.md
  Infra:
    - ./references/domains/infrastructure.md
    - ./references/shapes/cloud.md
  # BusinessLLM: omit if not dispatched
```

## Worked example

Tags: `api`, `web`, `ts-js-node`, `cloud`

```text
AuthZ:     domains/authz.md + shapes/api.md
Injection: domains/injection.md + shapes/api.md
Secrets:   domains/secrets.md + shapes/web.md
Infra:     domains/infrastructure.md + shapes/cloud.md
Business:  (not dispatched)
hotspots:  /api/invoices/:id, /api/admin/*, password-reset, webhook/stripe
bypasses:  /api/debug/*, SETUP_MODE
auth_model: Session cookie + JWT bearer; tenant from session, never body
```

## Completion criterion

Threat model written (assets, actors, entry points, trust boundaries, 1–3 abuse_goals, auth_model, up to 15 first-hit hotspots, bypasses or `none found`); shape tags listed; every dispatched domain has ≤2 concrete paths (or `"none"` for slot 2). Open `hunt.md` when this criterion is met.
