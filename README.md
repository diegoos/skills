# Skills

Personal collection of AI agent skills in Markdown. Each one gives the agent a fixed process for code review, docs, commits, security, and similar work.

Notable changes live in [CHANGELOG.md](CHANGELOG.md).

---

## Agent rules

[global-rules.md](global-rules.md) is the global judgment layer. The operating stack is always: this file → repository `AGENTS.md` → workflow skills. Use it layered (the tool loads the file globally; the repo keeps its own operational `AGENTS.md`) or fused (fold the base into the project's `AGENTS.md` with Commands, Permissions, and done criteria). Do not keep two competing policy files in the same scope.

The same rules can live in `~/.codex/AGENTS.md` for Codex, `~/.claude/CLAUDE.md` for Claude, `~/.config/opencode/AGENTS.md` for OpenCode, or `~/.cursor/rules/agent-rules.md` for Cursor.

---

## Available skills

| Skill                                                          | What it does                                                                                                                                                                                  |
| -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `[write-great-instructions](skills/write-great-instructions/)` | Helps you write `AGENTS.md`, `CLAUDE.md`, Cursor rules, and Copilot instructions. Loads when you create or edit one.                                                                          |
| `[commit-message](skills/commit-message/)`                     | Draft [Conventional Commits](https://www.conventionalcommits.org/) from the real git status and diff. One atomic commit per concern by default; a single commit only when you ask.            |
| `[code-review-plus](skills/code-review-plus/)`                 | Multi-pipeline PR/diff review (≤5 hunters or one on demand), optional shapes, test-quality, `docs/code-review/` memory, P0-P3 report. Branches: `review`, `fix`/`apply`/`implement`, `prune`. |
| `[deep-security-review](skills/deep-security-review/)`         | Security-first review: threat model with hotspots, parallel domain hunts, disprove/verify, findings + hardening notes (P0-P3). Branches: review, `fix`/`apply`/`implement`. Invoke by name.   |
| `[make-code](skills/make-code/)`                               | XP Simple Design for app code: make it work, right, then fast. YAGNI, cyclomatic cap. Branches: `write`, `refactor`, `improve`.                                                               |
| `[make-docs](skills/make-docs/)`                               | Architecture docs and behavioral specs under `docs/`. Branches: `explore`, `update` (stamp), `refresh` (re-survey), `adr`. Confirm gate; ≤3 hunters.                                          |
| `[makefile-expert](skills/makefile-expert/)`                   | Author or review GNU Make Makefiles (last-mile glue vs compile graph). Branches: `write`, `review`.                                                                                           |
| `[markdown-writer](skills/markdown-writer/)`                   | Create or edit `.md` / `.mdc` / `.mdx` that scans for humans and parses for agents. One-line prose unless dest requires wrap. YAML frontmatter when dest uses it.                             |
| `[frontend-design-plus](skills/frontend-design-plus/)`         | Build or restyle visual frontend (component, app UI, marketing). Origin `greenfield` or `redesign`; Design Read + Lock before markup; routed refs; anti-slop pre-flight (A / A+B / A+C).      |
| `[sass-with-bem](skills/sass-with-bem/)`                       | Write or review BEM with Sass/SCSS (flat compiled selectors, `is-` / `has-` states, 7-1 partials). Branches: `write`, `review`.                                                               |

The agent follows each skill's `SKILL.md`. Some skills also ship a human `README.md`, a `PATTERNS.md`, or templates under `references/`.

---

## Quickstart

Install with the [skills.sh](https://www.skills.sh/) CLI:

```bash
# all skills in this repo
npx skills add diegoos/skills

# one skill
npx skills add diegoos/skills --skill write-great-instructions
```

After install, call them from the harness with a slash command or with natural language, depending on the skill.

## How to use

Some skills load from intent (you do not have to name them):

```text
"Write an AGENTS.md for this project"            → write-great-instructions
"Tighten this CLAUDE.md"                         → write-great-instructions
"Write Cursor rules for our TSX components"      → write-great-instructions
"Add an endpoint that lists orders"              → make-code (write)
"This function is too nested"                    → make-code (refactor)
"This loop is doing N+1 queries"                 → make-code (improve)
"Generate docs for this codebase"                → make-docs (explore)
"Update the docs after these changes"            → make-docs (update)
"Refresh the docs against current code"          → make-docs (refresh)
"Record the decision to use Postgres"            → make-docs (adr)
"Write a commit message for these changes"       → commit-message
"Add a BEM card component in SCSS"               → sass-with-bem (write)
"Review these styles for BEM compliance"         → sass-with-bem (review)
"Fix the formatting in this README"              → markdown-writer
"Build a landing page for this product"          → frontend-design-plus (marketing, greenfield)
"Restyle this dashboard without changing flows"  → frontend-design-plus (app UI, redesign)
"Add a modal with loading and error states"      → frontend-design-plus (component)
"Add a Makefile for docker and lint"             → makefile-expert (write, glue)
"Review this Makefile for make -j"               → makefile-expert (review, compile)
```

User-invoked only (`disable-model-invocation`). Call by name:

```text
/code-review-plus              → multi-perspective PR/diff review
/code-review-plus quality      → Quality hunter only (also: correctness, security, architecture, performance)
/code-review-plus fix          → apply findings from the last report (aliases: apply, implement)
/code-review-plus prune        → drop old docs/code-review review files (count first, then choose)
/deep-security-review          → deep security review (domain + shape hunts)
/deep-security-review fix      → apply review findings (aliases: apply, implement)
```

Harnesses also accept forms like `/make-docs explore`.

---

## Structure

Repo layout (every skill has `SKILL.md` and `agents/openai.yaml`) is in [docs/structure.md](docs/structure.md)

---

## Custom OpenCode agents

Optional agents under `.opencode/agents/`. They are not part of the skills install contract.

| Agent      | Role                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------- |
| `ask`      | Read-only: conversation and code analysis. No edits, no bash, no subagents.                       |
| `reviewer` | Single-pass, high-signal review. Complements `code-review-plus` (parallel multi-pipeline review). |

---

### `code-review-plus` vs `deep-security-review`

Use `code-review-plus` for a PR or diff review covering correctness, security, architecture, quality, and performance, with adaptive tiers and optional stack shapes including `llm` (`1` perspective + `0` or `1` shape per hunter; Quality may add `test-quality.md` when tests are in scope). Name one hunter (`/code-review-plus security`) to run that pass only. Shape pick is a priority list on `normal` and `large/sensitive`. Reviews persist under `docs/code-review/` in the reviewed repo.

Use `deep-security-review` when security is the main goal: threat model with hotspots/bypasses, domain hunts (`1` domain + `1` shape per subagent), disprove gates, and severity calibrated for security, with hardening notes kept separate. Apply findings with `/deep-security-review fix` (aliases: `apply`, `implement`).

`deep-security-review` replaces the shallow security pass. Do not run both Security perspectives on the same scope at once. `code-review-plus` may tell you to run `/deep-security-review`. It will not start that skill by itself.
