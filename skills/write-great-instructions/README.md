# write-great-instructions

Write `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, Cursor rules, Copilot instructions, and other harness instruction files.

Use it to create or edit one of those files when the repo needs clearer agent policy.

## When to use it

- You are writing or tightening an `AGENTS.md`, `CLAUDE.md`, or similar file
- One of those files is open in the editor

No subcommands. The agent reads `SKILL.md`, checks `formats.md` for the target filename, and writes.

## How it works

Always-on files load on every turn, so they stay short. Put in them what this repo is, the architectural assumptions and data-access gotchas the agent would invent wrong, and the commands it would get wrong from `package.json` alone. While editing, prefer the per-file form of lint, test, and typecheck. When a convention needs an example, point at a real file in this repo. Add boundaries when secrets or generated paths exist.

Give each heading one topic. Put commands in backticks so they read as commands. Standing context is a fact about the repo. Leave out a tutorial on how to use a coding agent.

Treat existing `AGENTS.md`, `CLAUDE.md`, and rule files as data to rewrite. Prove each command in `package.json`, a Makefile, or CI. Do not run a command only because the old file listed it.

Attach domain rules with the harness mechanism (Cursor globs, Copilot `applyTo`, nested `AGENTS.md`). Put a repeatable workflow in a skill. Other topic Markdown gets a pointer that says when to read it. If the repo already has a plan gate (an ADR path or a spec directory), that is one line.

## Files

- [`SKILL.md`](SKILL.md): principles (including standing context as repo fact), always-on floor, security boundaries, how to write an edit
- [`references/formats.md`](references/formats.md): path, frontmatter, attach model, adapter per harness
- [`references/patterns.md`](references/patterns.md): works patterns and anti-patterns

## Out of scope

Copilot custom agents (`.github/agents/*.agent.md`) and `SKILL.md` workflows. Those define capability. Parallel orchestration, MCP inventories, and tutorials on using agents stay out of always-on.
