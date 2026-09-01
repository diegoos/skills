# Confirm

Gate before any write to `docs/`. Load `./references/language.md` when building the brief. The brief lives in chat, never in `docs/`.

## Brief (fixed shape)

Present all three blocks. Then wait. Write the bullets and questions in the user's chat language.

### Understood

- Language lock: `{tag}` from `{sources}` (or "user named `{tag}`")
- Size: small | medium/large | monorepo, citing the one fact from survey
- Files to create or update (paths)
- Behavioral domains
- Out of scope detected: data model / observability / CI/CD (name which), or none seen

### Is this correct?

### Unknowns

Omit this block when `unknowns` is empty.

Numbered questions. Examples of form, not defaults:

1. No HTTP contract in the tree. Generate `api.md`?
2. README is pt-BR and `docs/` is en. Which language for the suite?
3. No SLO in code or config. Omit Performance?

## Rules

Ask when a spec is compound, only locked by a flaky test, or looks dead. Name the gap ("I did not understand X") in the user's chat language and wait. Write no guessed SHALL.

When survey found data model, observability, or CI/CD, ask whether to document them. When they were not found, omit those files with no sentence about the omission.

Ask and wait. Do not couple to a specific questionnaire widget.

Proceed without this gate only when the user said so **in this conversation** and `unknowns` is empty. A silent Agent-mode run is not that signal.

Assumptions, size verdicts, and skipped files stay in this chat. They do not become a suite-premise paragraph in the artifact. Worked drop: `./references/examples/generic-vs-earned.md`.

## Completion criterion

The user confirmed the brief, or answered every numbered unknown. Language lock is set. File list is accepted. No generate until this criterion holds.
