# Skills

Personal collection of AI agent skills in Markdown. Each skill is a fixed process the agent follows for a job such as code review, docs, commits, or security.

Notable changes live in [CHANGELOG.md](CHANGELOG.md).

---

## Agent rules

[global-rules.md](global-rules.md) is a slim always-on defaults file: direct replies, same model for subagents, no prose hard-breaks, prefer `rg` and `fd`, stop when blocked, git/secrets/production guardrails, conventional commits, and STE100/candid output.

> That slim is the trade for [`make-code`](skills/make-code/): code judgment (*tight* ladder, YAGNI, surgical fix, *red* proof) loads only when writing or changing application code, not on every turn. Layered load: the tool loads the file globally, and the repo keeps its own operational `AGENTS.md`. Fused load: fold the base into the project's `AGENTS.md` with Commands, Permissions, and done criteria. Keep a single policy file in each scope.

The same rules can live in `~/.codex/AGENTS.md` for Codex, `~/.claude/CLAUDE.md` for Claude, `~/.config/opencode/AGENTS.md` for OpenCode, or `~/.cursor/rules/agent-rules.md` for Cursor.

---

## Available skills

| Skill                                                          | What it does                                                                                                                                                                                  |
| -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `[write-great-instructions](skills/write-great-instructions/)` | Helps you write `AGENTS.md`, `CLAUDE.md`, Cursor rules, and Copilot instructions. Loads when you create or edit one.                                                                          |
| `[commit-message](skills/commit-message/)`                     | Draft [Conventional Commits](https://www.conventionalcommits.org/) from the real git status and diff. One atomic commit per concern by default; a single commit only when you ask.            |
| `[code-review-plus](skills/code-review-plus/)`                 | PR/diff review: Correctness, Security, Quality by default; Architecture on large diffs. Memory under `docs/code-review/`. P0-P3. Branches: `review`, `fix`/`all`/`ids`, `prune`, `help`.      |
| `[deep-security-review](skills/deep-security-review/)`         | Security-first review: threat model, domain hunts, P0–P3 findings. Same report skeleton as `code-review-plus`. Branches: `review`, `fix`/`all`/`ids`. Invoke by name.                         |
| `[make-code](skills/make-code/)`                               | KISS, DRY, YAGNI, CC for app code: make it work, right, then fast. Branches: `write`, `refactor`, `improve`.                                                                                  |
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

Some skills load from intent:

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

## Structure

Repo layout (every skill has `SKILL.md` and `agents/openai.yaml`) is in [docs/structure.md](docs/structure.md).

---

## Custom OpenCode agents

Optional agents under `.opencode/agents/`. They are not part of the skills install contract.

| Agent      | Role                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------- |
| `ask`      | Read-only: conversation and code analysis. No edits, no bash, no subagents.                       |
| `reviewer` | Single-pass, high-signal review. Complements `code-review-plus` (parallel multi-pipeline review). |

---

### `code-review-plus` vs `deep-security-review`

Use `code-review-plus` for a PR or diff review. The default hunters are correctness, security, and quality. Architecture joins on `large/sensitive`. Performance runs only when you isolate it. Tiers follow the size of the change. Optional stack shapes include `llm`. Each hunter gets one perspective and at most one shape. Quality may add `test-quality.md` when tests are in scope.

Hunt lists are a **floor**: cover them, then report other issues in that pipeline. Pass B drops false positives. The Quality hunter reads `make-code` when that skill is available. Otherwise it uses a built-in Floor and the report says so. Name one hunter (`/code-review-plus security`) to run that pass only.

`code-review-plus` always runs its own Security hunter. The report may end with a `/deep-security-review` suggestion. On `normal` and `large/sensitive`, shape pick follows a priority list. Reviews persist under `docs/code-review/` in the reviewed repo. A later run on the same branch is **delta** when a prior HEAD exists.

Use `deep-security-review` when security is the main goal. It builds a threat model with hotspots and bypasses, then runs domain hunts. Each hunter loads one domain file and at most one shape, then hunts in the code. Pass B confirms candidates. Severity is calibrated for security. Hunt lists are a **floor**. Without a subagent, domains run in series. The report uses the same skeleton as `code-review-plus` (Review Summary, six-column Overview, Verdict). Threat Model and Verification Gaps stay. Hardening is P2 in the table. Apply with `/deep-security-review fix` (P0, P1), `fix all`, or `fix 2,3,6`. Fix reads `make-code` when that skill is in the environment.

Start `deep-security-review` yourself after the `code-review-plus` report if you want that pass. A `code-review-plus` run still uses CRP's Security hunter.
