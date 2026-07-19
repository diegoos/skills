# Phase 1 — Plan

Orchestrator-only. Build the threat model and `DispatchManifest` before any hunt.

## Threat model (minimum)

```text
- Assets: secrets, tokens, PII, payment data, tenant data, admin actions
- Actors: anonymous, authenticated, tenant admin, platform admin, third-party, malicious prompt
- Entry points: routes, APIs, webhooks, uploads, jobs, queues, WebSockets, CLIs
- Trust boundaries: browser/server, public/private, app/DB, app/LLM, LLM/tools, CI/runtime
- Abuse goals: read others' data, mutate protected state, escalate, RCE, exfiltrate, bypass billing
```

## Scope sources

| Source              | Action                                            |
| ------------------- | ------------------------------------------------- |
| Whole codebase      | Map entry points first; prioritize auth and money |
| Specific files      | Review those files in full trust-boundary context |
| Uncommitted changes | `git diff`                                        |
| Feature branch      | `git diff <base>...HEAD` (repo default base)      |
| Pasted code         | Review directly                                   |

## Detect shape tags (cheap signals — do not open domain/shape files yet)

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

| Tag / role            | File                                                |
| --------------------- | --------------------------------------------------- |
| Domain AuthZ          | `./references/domains/authz.md`                     |
| Domain Injection      | `./references/domains/injection.md`                 |
| Domain Secrets        | `./references/domains/secrets.md`                   |
| Domain Infra          | `./references/domains/infrastructure.md`            |
| Domain Business & LLM | `./references/domains/business-llm.md`              |
| Shape `api`           | `./references/shapes/api.md`                        |
| Shape `web`           | `./references/shapes/web.md`                        |
| Shape `ts-js-node`    | `./references/shapes/typescript-javascript-node.md` |
| Shape `python`        | `./references/shapes/python.md`                     |
| Shape `php`           | `./references/shapes/php.md`                        |
| Shape `cloud`         | `./references/shapes/cloud.md`                      |
| Shape `llm`           | `./references/shapes/llm.md`                        |
| Shape `sensitive`     | `./references/shapes/sensitive-flows.md`            |
| Shape `tooling`       | `./references/shapes/tooling.md`                    |
| Optional OWASP        | `./references/optional/owasp-map.md`                |

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

**Hard caps:**

1. Orchestrator does not open `domains/` or `shapes/` in Phase 1.
2. Each hunter reads at most the two paths listed for its domain.
3. No matching tag for slot 2 → `"none"`.
4. Do not merge domains to save reads.

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
  abuse_goals: [string]
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
```

## Completion criterion

Threat model written; shape tags listed; every dispatched domain has ≤2 concrete paths (or `"none"` for slot 2). Do not start Phase 2 until this is done.
