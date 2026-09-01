---
name: write-great-instructions
description: >-
  Write or edit agent instruction files (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, Cursor `.mdc` rules, Copilot instructions, and other harness instruction files). Use when creating, drafting, or editing those files, or when the user wants better agent instructions for a repo.
metadata:
  version: 0.3.0
  author: "Diego Oliveira"
  tags:
    - instructions
    - agentsmd
    - claude-md
    - cursor-rules
    - copilot-instructions
    - opencode-rules
    - codex-agentsmd
---

# Write great instructions

Operational policy for a coding agent — not a README. Filename and harness vary; the writing does not.

## Principles

- **Always-on budget.** The expensive file loads on every turn in *this* harness. Root `AGENTS.md`: warn above ~150 lines. Codex shares 32 KiB cumulative along root→CWD; nested does not add a second budget. See caps in [`formats.md`](references/formats.md).
- **Observable or attachable.** Always-on: a command, an observable condition, or a CORRECT/WRONG snippet. Glob: a convention for that slice. Cut no-ops (`write clean code`, `follow best practices`, `handle errors gracefully`).
- **Environment is source of truth.** Point at `package.json`, CI, `--help`. Cache the gotcha, the decision, the tempting anti-pattern. Put a command in always-on when the runner is the recurring mistake (`pnpm` not `npm`, `uv` not `pip`).
- **Native disclosure.** Domain convention → glob / `.mdc` / `paths:` / `applyTo` / nested file. Repeatable workflow → skill. Topic Markdown only with a pointer that names when to read it.
- **One meaning, one place.** Adapter, not copy. A nested child that must replace a parent rule *names the replacement*. Omission does not delete the parent (Codex concatenates; Devin inherits).
- **Positive prompt.** Write the target. Pair a ban with the substitute. `NEVER` only for destructive moves.
- **Closure.** Two to four commands whose exit 0 proves done. Review/PR checklists belong in a skill or a pointed doc, not always-on.
- **Earned.** Emit the minimum the repo proves. Add a rule after the agent repeats a mistake — not after one incident. Skip directory overviews the `ls` already shows.

## Always-on floor

Include a line only when the repo earns it:

1. One sentence naming what this repo is (and nothing more of the README).
2. Package manager when it is not npm (or when `corepack` is required).
3. Build / test / typecheck commands the agent would get wrong by reading `package.json` alone.
4. Boundaries (READ / WRITE / NEVER / HUMAN_CHECKPOINT) when `.env*`, `generated/`, `legacy/`, `vendor/`, or infra paths exist.
5. Escalation and numbered precedence when the repo has a real tradeoff or a known destructive workaround.

Everything else → glob, nested file, skill, or omit.

## How to write this edit

1. **Name the file.** The open buffer or the filename the user named. One canonical always-on per scope; other harness files are adapters, not a second body. User-level files (`~/.claude/CLAUDE.md`, `~/.config/opencode/AGENTS.md`) are handwritten preferences — do not copy them into the repo.
2. **Recon only what a line needs.** One command from `package.json`, one gotcha, one boundary glob. No folder inventory.
3. **Earn each new line.** Observable or attachable; provable in the repo; no no-op. Run every command you emit.
4. **Close the edit.** The line does not duplicate the environment or the README. Smell → one heading in [`patterns.md`](references/patterns.md). Packaging → [`formats.md`](references/formats.md).

## Definition of Done

The edited file obeys the principles and floor above. Every emitted command was run (exit code recorded). No second always-on file created. No topic doc without an inbound pointer.

## Out of scope

Copilot custom agents (`.github/agents/*.agent.md`) and `SKILL.md` workflows. Those are capability, not repo policy.
