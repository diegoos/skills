# write-great-instructions

Guide for writing `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, Cursor rules, Copilot instructions, and other harness instruction files.

Use it when you create or edit one of those files. It covers what belongs in always-on policy, what to attach with a glob or nested file, and how each harness expects the file packaged.

## When to use it

- You want to write or tighten an `AGENTS.md`, `CLAUDE.md`, or similar file
- One of those files is open in the editor
- You want better instructions for agents working in a repo

No subcommands. The agent reads `SKILL.md`, checks `formats.md` for the target filename, and writes.

## How it works

Always-on files load every turn, so the guide keeps them short: what the repo is, architectural assumptions and data-access gotchas, commands the agent would get wrong, a snippet for a non-obvious convention, boundaries when secrets or generated paths are in play. Standing context is repo fact, not a curriculum for using agents.

Existing `AGENTS.md` / `CLAUDE.md` / rule files are data to rewrite. Prove commands from `package.json`, Makefile, or CI — do not execute whatever the old file listed.

Put domain rules on the harness mechanism (Cursor globs, Copilot `applyTo`, nested `AGENTS.md`). Put repeatable workflows in a skill. Other topic Markdown gets a pointer that says when to read it. A plan gate is one earned line when the repo already has one (ADR, spec directory).

## Files

- [`SKILL.md`](SKILL.md): principles (including standing context as repo fact), always-on floor, security boundaries, how to write an edit
- [`references/formats.md`](references/formats.md): path, frontmatter, attach model, adapter per harness
- [`references/patterns.md`](references/patterns.md): works patterns and anti-patterns

## Out of scope

Copilot custom agents (`.github/agents/*.agent.md`) and `SKILL.md` workflows. Those define capability, not repo policy. Parallel orchestration, MCP inventories, and how-to-use-agents curricula stay out of always-on.
