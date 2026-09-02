# write-great-instructions

Guide for writing `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, Cursor rules, Copilot instructions, and other harness instruction files.

Use it when you create or edit one of those files. It covers what belongs in always-on policy, what to attach with a glob or nested file, and how each harness expects the file packaged.

## When to use it

- You want to write or tighten an `AGENTS.md`, `CLAUDE.md`, or similar file
- One of those files is open in the editor
- You want better instructions for agents working in a repo

No subcommands. The agent reads `SKILL.md`, checks `formats.md` for the target filename, and writes.

## How it works

Always-on files load every turn, so the guide keeps them short: stack, commands the agent would get wrong, a snippet for a non-obvious convention, boundaries when secrets or generated paths are in play.

Put domain rules on the harness mechanism (Cursor globs, Copilot `applyTo`, nested `AGENTS.md`). Put repeatable workflows in a skill. Other topic Markdown gets a pointer that says when to read it.

## Files

- [`SKILL.md`](SKILL.md): principles, always-on floor, how to write an edit
- [`references/formats.md`](references/formats.md): path, frontmatter, attach model, adapter per harness
- [`references/patterns.md`](references/patterns.md): works patterns and anti-patterns

## Out of scope

Copilot custom agents (`.github/agents/*.agent.md`) and `SKILL.md` workflows. Those define capability, not repo policy.
