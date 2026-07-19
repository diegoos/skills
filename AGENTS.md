# AGENTS.md

This repository is a collection of AI agent skills (`skills/<name>/SKILL.md`) plus optional OpenCode agents under `.opencode/`.

No package manager, build, or test suite — ship Markdown skills only.

## Commands

- Lint Markdown: `markdownlint -c .markdownlint.yaml 'skills/*/SKILL.md' README.md AGENTS.md` (exit 0)
- MD013 is **off** in `.markdownlint.yaml` and `.editorconfig` (`[*.md] max_line_length = off`)

## Permission boundaries

| Mode | Paths |
| --- | --- |
| READ | `**` |
| WRITE | `skills/**`, `README.md`, `AGENTS.md`, `.editorconfig`, `.markdownlint.yaml`, `.opencode/**` |
| NEVER | `.env*`, credentials, force-push, rewriting git history |
| HUMAN_CHECKPOINT | publishing/removing a skill from the public registry, deleting a skill directory |

## Precedence

1. Explicit user instruction for this turn
2. This `AGENTS.md`
3. The `SKILL.md` / references of the skill being edited
4. Generic Markdown style guides — **never** re-enable line wrapping to satisfy MD013

## When writing or editing skills

- Put each skill in `skills/<name>/` with required `SKILL.md`; optional `references/`, `README.md`, `PATTERNS.md`.
- Frontmatter must include `name` and `description`. Set `disable-model-invocation: true` only for user-invoked-only skills.
- Keep `SKILL.md` thin; push depth to `references/` (progressive disclosure).
- **Do not soft-wrap Markdown** (MD013). Do not break prose, list items, or table cells to fit 80/120 columns. Break only on semantic boundaries (heading, new list item, blank line, fence).
- After edits, run `markdownlint -c .markdownlint.yaml` on every changed `.md` path — exit 0. If MD013 fires, fix the config — never insert wraps to silence it.
- Adding or removing a skill: update the skills table in `README.md` in the same change.
- Proof artifact: diff has no reflow-only edits; long instructional lines stay on one line.

## When blocked

- Ambiguous skill behaviour or scope: stop and ask — do not invent a second skill or a build toolchain.
- Never soft-wrap Markdown to clear lint.
- Never `git push`, commit secrets, or skip hooks unless the user explicitly asks.
- Never treat `.opencode/agents/` as part of the skills contract (see `README.md`).
