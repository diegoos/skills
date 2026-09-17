# AGENTS.md

This repository is a collection of AI agent skills (`skills/<name>/SKILL.md`) plus optional OpenCode agents under `.opencode/`.

No package manager, build, or test suite — ship Markdown skills only.

## Commands

- Lint Markdown: `markdownlint -c .markdownlint.yaml 'skills/*/SKILL.md' README.md AGENTS.md CHANGELOG.md 'docs/*.md'` (exit 0)
- MD013 is **off** in `.markdownlint.yaml` and `.editorconfig` (`[*.md] max_line_length = off`)

## Permission boundaries

| Mode             | Paths                                                                                                                   |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------- |
| READ             | `**`                                                                                                                    |
| WRITE            | `skills/**`, `docs/**`, `README.md`, `AGENTS.md`, `CHANGELOG.md`, `.editorconfig`, `.markdownlint.yaml`, `.opencode/**` |
| NEVER            | `.env*`, credentials, force-push, rewriting git history                                                                 |
| HUMAN_CHECKPOINT | publishing/removing a skill from the public registry, deleting a skill directory                                        |

## Precedence

1. Explicit user instruction for this turn
2. This `AGENTS.md`
3. The `SKILL.md` / references of the skill being edited
4. Generic Markdown style guides — **never** re-enable line wrapping to satisfy MD013

## Changelog

- Record every notable change in `CHANGELOG.md` under `[Unreleased]`, using Keep a Changelog sections (`Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`, `Security`) as needed.
- Do **not** create a dated version heading (e.g. `## [0.4.0] - YYYY-MM-DD`) or move `[Unreleased]` into a release section unless the user explicitly asks to set or cut a version.
- Leave `skills/<name>/SKILL.md` `metadata.version` unchanged while the work sits in `[Unreleased]`. Do not write a version arrow on Unreleased bullets. A new skill may set an initial `metadata.version`; do not bump it again until the next changelog cut.
- When the user asks to cut a changelog version, bump `metadata.version` of each skill that has entries in that release **in the same change** (one bump per skill per cut). Do not invent a changelog version to match a skill bump, and do not bump a skill while `[Unreleased]` is uncut.

CORRECT (skill edit): `[Unreleased]` gains a bullet; `metadata.version` in `SKILL.md` stays put.

## When writing or editing skills

- Put each skill in `skills/<name>/` with required `SKILL.md`; optional `references/`, `README.md`, `PATTERNS.md`.
- Each skill ships `agents/openai.yaml` for ChatGPT/Codex ([optional metadata](https://learn.chatgpt.com/docs/build-skills#optional-metadata)): `interface.display_name`, `interface.short_description` (25–64 characters). Set `policy.allow_implicit_invocation: false` when `disable-model-invocation: true`; otherwise `true`. Do not add MCP `dependencies` unless the skill needs a named server.
- Frontmatter must include `name` and `description`. Set `disable-model-invocation: true` only for user-invoked-only skills.
- Keep `SKILL.md` thin; push depth to `references/` (progressive disclosure).
- **Do not soft-wrap Markdown** (MD013). Do not break prose, list items, or table cells to fit 80/120 columns. Break only on semantic boundaries (heading, new list item, blank line, fence).
- After edits, run `markdownlint -c .markdownlint.yaml` on every changed `.md` path — exit 0. If MD013 fires, fix the config — never insert wraps to silence it.
- Adding or removing a skill: update the skills table in `README.md` and the tree in `docs/structure.md` in the same change.
- Update `CHANGELOG.md` in the same change (see Changelog above).
- Proof artifact: diff has no reflow-only edits; long instructional lines stay on one line.

## When committing

- **Never** `git push`, commit secrets, or skip hooks unless the user explicitly asks.
- Use the `commit-message` skill to write a commit message **when available**.
- If the `commit-message` skill is **not available**, write a commit message using `conventional commits` format. The message should be concise and descriptive.

## When blocked

- Ambiguous skill behaviour or scope: stop and ask — do not invent a second skill or a build toolchain.
- Never soft-wrap Markdown to clear lint.
- Never treat `.opencode/agents/` as part of the skills contract (see `README.md`).
