# Skills

Personal collection of AI agent skills in Markdown. Each skill is the procedure an agent follows for one job, such as code review, docs, commits, or security.

Notable changes live in [CHANGELOG.md](CHANGELOG.md).

## Available skills

| Skill                                                        | What it does                                                                                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| [write-great-instructions](skills/write-great-instructions/) | Writes the files an agent reads, such as `AGENTS.md`, `CLAUDE.md`, Cursor rules, and Copilot instructions.                     |
| [code-review-plus](skills/code-review-plus/)                 | Reviews a pull request or diff for bugs, security issues, and code quality, and can apply the fixes you pick.                  |
| [make-changelog](skills/make-changelog/)                     | Keeps a changelog: creates it, records notable changes, and bumps the version only when you ask.                               |
| [make-code](skills/make-code/)                               | Writes and fixes application code, and can simplify it or speed up a slow spot you name.                                       |
| [make-commits](skills/make-commits/)                         | Writes a commit from the git diff in the project's style, one commit per reason, or only the message when that is all you ask. |
| [make-docs](skills/make-docs/)                               | Writes architecture docs and behavior specs, updates them after code changes, or records a decision.                           |
| [make-skill](skills/make-skill/)                             | Writes or edits an AI agent skill so the agent follows the same process on every run.                                          |
| [makefile-expert](skills/makefile-expert/)                   | Writes or reviews a GNU Make Makefile.                                                                                         |
| [markdown-writer](skills/markdown-writer/)                   | Writes Markdown that people can scan and an agent can parse.                                                                   |
| [sass-with-bem](skills/sass-with-bem/)                       | Writes Sass/SCSS so each component rule compiles to one BEM class.                                                             |

The agent follows each skill's `SKILL.md`. Some skills also include a `README.md` for people, a `PATTERNS.md`, or templates under `references/`.

<details>
<summary>Deprecated</summary>

Archived under `deprecated/`. A normal `npx skills add` does not install these.

| Skill                                                    | What it does                                                                                               |
| -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| [deep-security-review](deprecated/deep-security-review/) | Archived. It used to review a change for security issues, build a threat model, and rate what it finds.    |
| [frontend-design-plus](deprecated/frontend-design-plus/) | Archived. It used to build or restyle a web page, screen, or component.                                    |

</details>

## Quickstart

Install with the [skills.sh](https://www.skills.sh/) CLI:

```bash
# all skills under skills/
npx skills add diegoos/skills

# one skill
npx skills add diegoos/skills --skill make-code
```

After install, call them from the harness with a slash command or with natural language, depending on the skill.

## How to use

Some skills start from what you ask:

```text
"Write an AGENTS.md for this project"            → write-great-instructions
"Tighten this CLAUDE.md"                         → write-great-instructions
"Write Cursor rules for our TSX components"      → write-great-instructions
"Add an endpoint that lists orders"              → make-code (write)
"This function is too nested"                    → make-code (refactor)
"This loop is doing N+1 queries"                 → make-code (refactor, named hotspot)
"Start a changelog for this project"             → make-changelog (init)
"Record these changes in the changelog"          → make-changelog (update)
"Bump the version"                               → make-changelog (bump)
"Generate docs for this codebase"                → make-docs (explore)
"Update the docs after these changes"            → make-docs (update)
"Refresh the docs against current code"          → make-docs (refresh)
"Record the decision to use Postgres"            → make-docs (adr)
"Create a skill for reviewing SQL migrations"    → make-skill
"Tighten the description and steps in this skill" → make-skill
"Write a commit message for these changes"       → make-commits (draft)
"Commit these changes"                           → make-commits (commit)
"Amend the commit you just made"                 → make-commits (amend)
"Add a BEM card component in SCSS"               → sass-with-bem
"Fix the formatting in this README"              → markdown-writer
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
```

Harnesses also accept forms like `/make-docs explore`.

## Agent rules

[global-rules.md](global-rules.md) is a short defaults file the agent always loads: direct replies, the same model for subagents, prose kept on one line, a preference for `rg` and `fd`, a stop when blocked, limits on git, secrets, and production, conventional commits, and candid output in STE100 style.

The same rules can live in `~/.codex/AGENTS.md` for Codex, `~/.claude/CLAUDE.md` for Claude, `~/.config/opencode/AGENTS.md` for OpenCode, or `~/.cursor/rules/agent-rules.md` for Cursor.

## Custom OpenCode agents

Optional agents under `.opencode/agents/`, separate from the skills install.

| Agent      | Role                                                                                                             |
| ---------- | ---------------------------------------------------------------------------------------------------------------- |
| `ask`      | Read-only conversation and code analysis, without file edits, bash, or subagents.                                |
| `reviewer` | Single-pass review of findings worth acting on. Complements `code-review-plus` (parallel multi-pipeline review). |
