# Skills

My collection of AI agent skills — to work with safety and quality as a real software engineer.

---

## Available skills

| Skill                                                      | What it does                                                                                                                                                                                                           |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **[`write-great-agentsmd`](skills/write-great-agentsmd/)** | Creates, updates, and audits `AGENTS.md` — the policy that orchestrates the agent in the repo. Branches: **bootstrap** (from scratch), **update** (sync after changes), **lint** (health audit).                       |
| **[`commit-message`](skills/commit-message/)**             | Generates [Conventional Commits](https://www.conventionalcommits.org/) messages from the real diff. Fires only when asked; never force-pushes, skips hooks, or commits secrets.                                        |
| **[`code-review-plus`](skills/code-review-plus/)**         | Code review across 5 dimensions (correctness, security, architecture, quality, performance) with parallel subagents and anti-false-positive checks. Prioritized report (P0–P3), calibrated to avoid inflated severity. |
| **[`deep-security-review`](skills/deep-security-review/)** | Deep security review: phased router (plan → hunt → verify → report), parallel domain subagents, each with at most one domain + one shape checklist. Findings table (P0–P3 + CRITICAL–LOW).                             |
| **[`make-docs`](skills/make-docs/)**                       | Generates and maintains architecture docs and behavioral specs in `docs/`. Branches: **explore** (survey → propose → generate), **update** (commits since the `Updated on` stamp), **adr** (decision record).          |
| **[`sass-with-bem`](skills/sass-with-bem/)**               | Writes and reviews BEM CSS with Sass/SCSS — flat selectors via `&` nesting, block/element/modifier, `is-`/`has-` states, 7-1 partials. Branches: **write**, **review**.                                                |

> Each skill has a `SKILL.md` (source of truth for the agent).
>
> Some include a human-facing `README.md`, catalogues (`PATTERNS.md`), or templates under `references/`.

---

## Quickstart

1. Install via the [skills.sh](https://www.skills.sh/) script:
   - All skills:

   ```bash
   npx skills add diegoos/skills
   ```

   - A specific skill:

   ```bash
   # e.g. install the write-great-agentsmd skill
   npx skills add diegoos/skills --skill write-great-agentsmd
   ```

2. Done — you can use the installed skill(s).

---

## Structure

```text
skills/
├── write-great-agentsmd/   # AGENTS.md — bootstrap / update / lint
│   ├── SKILL.md
│   ├── PATTERNS.md
│   └── README.md
├── commit-message/         # Conventional Commits
│   └── SKILL.md
├── code-review-plus/       # Multi-perspective code review
│   └── SKILL.md
├── deep-security-review/   # Deep security review (subagents + findings table)
│   ├── SKILL.md            # Thin router — phases load on demand
│   └── references/
│       ├── phases/         # plan, hunt, verify-and-synthesize
│       ├── templates/      # final report
│       ├── domains/        # authz, injection, secrets, infra, business-llm
│       ├── shapes/         # api, web, languages, cloud, llm, …
│       └── optional/       # OWASP map (on request)
├── make-docs/              # Architecture + observable specs
│   ├── SKILL.md
│   ├── README.md
│   └── references/         # Templates (architecture, ADR, specs, …)
└── sass-with-bem/          # BEM + Sass/SCSS
    ├── SKILL.md
    └── references/
        ├── conventions.md  # Naming, 7-1, tokens
        └── examples.md     # Canonical HTML/SCSS samples

.opencode/                  # Optional — Custom OpenCode agents
└── agents/
    ├── ask.md              # Read-only agent
    └── reviewer.md         # Single-pass review
```

---

## Custom OpenCode agents

Custom agents for OpenCode can live under `.opencode/agents/`.

> They are not part of the skills contract.

| Agent          | Role                                                                                                           |
| -------------- | -------------------------------------------------------------------------------------------------------------- |
| **`ask`**      | Read-only persona: conversation and code analysis. No edits, no bash, no subagents.                            |
| **`reviewer`** | Single-pass, high-signal review persona. Complements `code-review-plus` (which does the deep parallel review). |

---

## How to use

In some cases the agent loads the skill from intent — you don't need to name it:

```text
"Create an AGENTS.md for this project"           → write-great-agentsmd (bootstrap)
"Generate docs for this codebase"                → make-docs (explore)
"Update the docs after these changes"            → make-docs (update)
"Record the decision to use Postgres"            → make-docs (adr)
"Add a BEM card component in SCSS"               → sass-with-bem (write)
"Review these styles for BEM compliance"         → sass-with-bem (review)
```

**User-invoked only** (`disable-model-invocation`) — call by name:

```text
/code-review-plus          → multi-perspective PR/diff review
/deep-security-review      → deep security review (domain + shape hunts)
```

Or invoke by skill name/command (e.g. `/make-docs explore`), depending on the harness.

**`code-review-plus` vs `deep-security-review`:** use the first for multi-perspective PR/diff review (correctness + security + quality…). Use the second when security is the primary goal — threat model, domain hunts (`1 domain + 1 shape` per subagent), and a security-calibrated findings table. Do not run both Security perspectives on the same scope in parallel; `deep-security-review` **replaces** the shallow security pass. `code-review-plus` may suggest you run `/deep-security-review`, but will not start it automatically.
