# Skills

Personal collection of AI agent skills in Markdown. Each skill is a fixed process the agent follows for a job such as code review, docs, commits, or security.

Notable changes live in [CHANGELOG.md](CHANGELOG.md).

---

## Available skills

| Skill                                                        | What it does                                                                                                                                        |
| ------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| [write-great-instructions](skills/write-great-instructions/) | Writes the files an agent reads, such as `AGENTS.md`, `CLAUDE.md`, Cursor rules, and Copilot instructions.                                          |
| [code-review-plus](skills/code-review-plus/)                 | Reviews a pull request or diff for bugs, security issues, and code quality, and can apply the fixes you pick.                                       |
| [deep-security-review](skills/deep-security-review/)         | Reviews a change for security issues, builds a threat model, and rates what it finds.                                                               |
| [make-changelog](skills/make-changelog/)                     | Keeps a changelog: creates it, records notable changes, and bumps the version only when you ask.                                                    |
| [make-code](skills/make-code/)                               | Writes and fixes application code, and can simplify it or speed up a slow spot you name.                                                            |
| [make-commits](skills/make-commits/)                         | Writes a commit from the git diff in the project's style, one per reason, or only the message when that is all you ask.                             |
| [make-docs](skills/make-docs/)                               | Writes architecture docs and behavior specs, updates them after code changes, or records a decision.                                                |
| [makefile-expert](skills/makefile-expert/)                   | Writes or reviews a GNU Make Makefile.                                                                                                              |
| [markdown-writer](skills/markdown-writer/)                   | Writes Markdown that is easy to scan and that an agent can parse.                                                                                   |
| [frontend-design-plus](skills/frontend-design-plus/)         | Builds or restyles a web page, screen, or component.                                                                                                |
| [sass-with-bem](skills/sass-with-bem/)                       | Writes or reviews Sass/SCSS that uses BEM class names.                                                                                              |

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

Some skills load from intent:

```text
"Write an AGENTS.md for this project"            → write-great-instructions
"Tighten this CLAUDE.md"                         → write-great-instructions
"Write Cursor rules for our TSX components"      → write-great-instructions
"Add an endpoint that lists orders"              → make-code (write)
"This function is too nested"                    → make-code (refactor)
"This loop is doing N+1 queries"                 → make-code (improve)
"Start a changelog for this project"             → make-changelog (init)
"Record these changes in the changelog"          → make-changelog (update)
"Bump the version"                               → make-changelog (bump)
"Generate docs for this codebase"                → make-docs (explore)
"Update the docs after these changes"            → make-docs (update)
"Refresh the docs against current code"          → make-docs (refresh)
"Record the decision to use Postgres"            → make-docs (adr)
"Write a commit message for these changes"       → make-commits (draft)
"Commit these changes"                           → make-commits (commit)
"Amend the commit you just made"                 → make-commits (amend)
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
/code-review-plus              → PR/diff review (Correctness, Security, Quality by default)
/code-review-plus quality      → Quality hunter only (also: correctness, security, architecture, performance)
/code-review-plus fix          → P0, P1, and vuln from the last report; leftover IDs printed (aliases: apply, implement)
/code-review-plus fix all      → every P0–P3 finding
/code-review-plus fix 2,3,6    → those Findings IDs
/code-review-plus prune        → drop old docs/code-review review files (count first, then choose)
/code-review-plus help         → explain how the skill works
/deep-security-review          → deep security review (domain + shape hunts)
/deep-security-review fix      → P0 and P1 from the last report; leftover IDs printed (aliases: apply, implement)
/deep-security-review fix all  → every P0–P3 finding (hardening included)
/deep-security-review fix 2,3,6 → those Findings IDs
```

Harnesses also accept forms like `/make-docs explore`.

---

## Agent rules

[global-rules.md](global-rules.md) is a slim always-on defaults file: direct replies, same model for subagents, no prose hard-breaks, prefer `rg` and `fd`, stop when blocked, git/secrets/production guardrails, conventional commits, and STE100/candid output.

The same rules can live in `~/.codex/AGENTS.md` for Codex, `~/.claude/CLAUDE.md` for Claude, `~/.config/opencode/AGENTS.md` for OpenCode, or `~/.cursor/rules/agent-rules.md` for Cursor.

---

## Custom OpenCode agents

Optional agents under `.opencode/agents/`. They are not part of the skills install contract.

| Agent      | Role                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------- |
| `ask`      | Read-only: conversation and code analysis. No edits, no bash, no subagents.                       |
| `reviewer` | Single-pass, high-signal review. Complements `code-review-plus` (parallel multi-pipeline review). |

---

### `code-review-plus` vs `deep-security-review`

`/code-review-plus` runs its own Security hunter. Use `/deep-security-review` when security is the main goal, or after a `code-review-plus` report that suggests it. See [code-review-plus](skills/code-review-plus/README.md) and [deep-security-review](skills/deep-security-review/README.md).
