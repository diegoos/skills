# Skills

Personal collection of AI agent skills. Each skill is Markdown the agent reads to run a fixed process: code review, docs, commits, security, and similar engineering work.

> Notable changes live in [CHANGELOG.md](CHANGELOG.md).

---

## Agent rules

[global-rules.md](global-rules.md) is the global judgment layer. The operating stack is always: **this file → repository** `AGENTS.md` **→ workflow skills**. Use it layered (tool loads the file globally; the repo keeps its own operational `AGENTS.md`) or fused (fold the base into the project's `AGENTS.md` with Commands, Permissions, and done criteria — do not keep two competing policy files in the same scope).

The global rules can be defined in the `~/.codex/AGENTS.md` for Codex, `~/.claude/CLAUDE.md` for Claude, `~/.config/opencode/AGENTS.md` for OpenCode or `~/.cursor/rules/agent-rules.md` for Cursor.

---

## Available skills

| Skill                                                  | What it does                                                                                                                                                                                    |
| ------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `[write-great-agentsmd](skills/write-great-agentsmd/)` | Create, update, or lint an `AGENTS.md` (or tool mirrors). Branches: `bootstrap`, `update`, `lint`, `slim`.                                                                                      |
| `[commit-message](skills/commit-message/)`             | Draft [Conventional Commits](https://www.conventionalcommits.org/) from the real git status and diff. One atomic commit per concern by default; a single commit only when you ask.              |
| `[code-review-plus](skills/code-review-plus/)`         | Multi-pipeline PR/diff review (≤5 hunters), optional shapes (`llm`; single-tag on `normal`), optional P0 verifier, P0-P3 report. Branches: `review`, `fix`/`apply`/`implement`. Invoke by name. |
| `[deep-security-review](skills/deep-security-review/)` | Security-first review: threat model with hotspots, parallel domain hunts, disprove/verify, findings + hardening notes (P0-P3). Branches: review, `fix`/`apply`/`implement`. Invoke by name.     |
| `[make-docs](skills/make-docs/)`                       | Architecture docs and behavioral specs under `docs/`. Branches: `explore`, `update` (since the `Updated on` stamp), `adr`.                                                                      |
| `[markdown-editor](skills/markdown-editor/)`           | Create or edit `.md` / `.mdc` / `.mdx` with Google Markdown Style Guide rules and YAML frontmatter. No prose hard line breaks.                                                                  |
| `[sass-with-bem](skills/sass-with-bem/)`               | Write or review BEM with Sass/SCSS (flat compiled selectors, `is-` / `has-` states, 7-1 partials). Branches: `write`, `review`.                                                                 |

Each skill's `SKILL.md` is what the agent follows. Some skills also ship a human `README.md`, a `PATTERNS.md`, or templates under `references/`.

---

## Quickstart

Install with the [skills.sh](https://www.skills.sh/) CLI:

```bash
# all skills in this repo
npx skills add diegoos/skills

# one skill
npx skills add diegoos/skills --skill write-great-agentsmd
```

After install, invoke skills from your agent harness (slash commands or natural language, depending on the skill).

## How to use

Some skills load from intent (you do not have to name them):

```text
"Create an AGENTS.md for this project"           → write-great-agentsmd (bootstrap)
"Generate docs for this codebase"                → make-docs (explore)
"Update the docs after these changes"            → make-docs (update)
"Record the decision to use Postgres"            → make-docs (adr)
"Write a commit message for these changes"       → commit-message
"Add a BEM card component in SCSS"               → sass-with-bem (write)
"Review these styles for BEM compliance"         → sass-with-bem (review)
"Fix the formatting in this README"              → markdown-editor
```

User-invoked only (`disable-model-invocation`). Call by name:

```text
/code-review-plus              → multi-perspective PR/diff review
/code-review-plus fix          → apply findings from the last report (aliases: apply, implement)
/deep-security-review          → deep security review (domain + shape hunts)
/deep-security-review fix      → apply review findings (aliases: apply, implement)
```

Harnesses also accept forms like `/make-docs explore`.

---

## Structure

```text
.
├── AGENTS.md               # Policy for agents working in this repo
├── CHANGELOG.md            # Keep a Changelog
├── global-rules.md         # Global agent defaults (layered or fused with repo AGENTS.md)
├── README.md
├── skills/
│   ├── write-great-agentsmd/   # AGENTS.md: bootstrap / update / lint / slim
│   │   ├── SKILL.md
│   │   ├── PATTERNS.md
│   │   └── README.md
│   ├── commit-message/         # Conventional Commits
│   │   └── SKILL.md
│   ├── code-review-plus/       # Multi-perspective code review
│   │   ├── SKILL.md            # Router: review vs fix|apply|implement
│   │   └── references/
│   │       ├── phases/         # scope, dispatch, verify, synthesize, fix
│   │       ├── perspectives/   # correctness, security, architecture, quality, performance
│   │       ├── shapes/         # web, api, ts/js/node, python, go, rust, llm (optional, ≤1 per hunter)
│   │       ├── examples/       # kept-vs-dropped (on Pass B doubt)
│   │       ├── dependency-review.md
│   │       ├── remedies.md
│   │       └── templates/      # final report
│   ├── deep-security-review/   # Deep security review
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── phases/         # plan, hunt, verify-and-synthesize, fix
│   │       ├── templates/      # final report
│   │       ├── domains/        # authz, injection, secrets, infra, business-llm
│   │       ├── shapes/         # api, web, languages, cloud, llm, …
│   │       ├── examples/       # gates, FP table, kept-vs-dropped (Phase 3)
│   │       └── optional/       # OWASP map (on request)
│   ├── make-docs/              # Architecture + observable specs
│   │   ├── SKILL.md
│   │   ├── README.md
│   │   └── references/         # Templates (architecture, ADR, specs, …)
│   ├── markdown-editor/        # Markdown + frontmatter
│   │   └── SKILL.md
│   └── sass-with-bem/          # BEM + Sass/SCSS
│       ├── SKILL.md
│       └── references/
│           ├── conventions.md
│           └── examples.md
└── .opencode/                  # Optional OpenCode agents (not part of the skills contract)
    └── agents/
        ├── ask.md              # Read-only
        └── reviewer.md         # Single-pass review
```

---

## Custom OpenCode agents

Optional agents under `.opencode/agents/`. They are not part of the skills install contract.

| Agent      | Role                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------- |
| `ask`      | Read-only: conversation and code analysis. No edits, no bash, no subagents.                       |
| `reviewer` | Single-pass, high-signal review. Complements `code-review-plus` (parallel multi-pipeline review). |

---

### `code-review-plus` vs `deep-security-review`

Use `code-review-plus` for a balanced PR/diff review (correctness, security, architecture, quality, performance), with adaptive tiers and optional stack shapes including `llm` (`1` perspective + `0` or `1` shape per hunter; on `normal`, only when a single eligible tag is obvious).

Use `deep-security-review` when security is the main goal: threat model with hotspots/bypasses, domain hunts (`1` domain + `1` shape per subagent), disprove gates, and security-calibrated severity with separate hardening notes. Apply findings with `/deep-security-review fix` (aliases: `apply`, `implement`).

Do not run both Security perspectives on the same scope at once. `deep-security-review` replaces the shallow security pass. `code-review-plus` may tell you to run `/deep-security-review`; it will not start that skill by itself.
