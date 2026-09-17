# AGENTS.md

Collection of Markdown skills (`skills/<name>/SKILL.md`). Ship Markdown only: no package manager, build, or test suite. `.opencode/agents/` is optional OpenCode; it is not the skills install contract.

## Commands

- Lint one changed Markdown file: `markdownlint -c .markdownlint.yaml <path>` (exit 0)

## Conventions

MD013 is off (`.markdownlint.yaml`, `.editorconfig` `[*.md]`). One-line prose, list items, and table cells. Break on a heading, new list item, blank line, or fence. If MD013 fires, fix the config.

## Boundaries

| Mode             | Paths                                                                                                                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| WRITE            | `skills/**`, `docs/**`, `README.md`, `AGENTS.md`, `CHANGELOG.md`, `global-rules.md`, `.editorconfig`, `.markdownlint.yaml`, `.opencode/**`                 |
| NEVER            | force-push or rewrite git history (both rewrite shared history)                                                                                            |
| HUMAN_CHECKPOINT | publishing or removing a skill from the public registry; deleting a skill directory                                                                        |

## Precedence

1. Explicit user instruction for this turn
2. This `AGENTS.md`
3. The `SKILL.md` / `references/` of the skill being edited
4. Generic Markdown style guides: keep MD013 off

## Changelog

`CHANGELOG.md` is for consumers of a skill, an OpenCode agent, or `global-rules.md`. Keep a Changelog sections as needed. Leave `[Unreleased]` until the user asks to cut a version. A new skill may set an initial `metadata.version`. Do not invent a changelog version to match a skill bump.

| Change                                                              | `[Unreleased]` | `metadata.version` |
| ------------------------------------------------------------------- | -------------- | ------------------ |
| Skill, OpenCode agent, or `global-rules.md`                         | bullet         | leave              |
| `AGENTS.md` or other contributor-only policy                        | skip           | leave              |
| User asked to cut; skill still at last dated `CHANGELOG.md` heading | dated heading  | bump once          |
| User asked to cut; skill already newer                              | dated heading  | leave              |

CORRECT (skill edit): `[Unreleased]` gains a bullet; `metadata.version` in `SKILL.md` stays put.

WRONG: Unreleased bullet with `0.1.0 → 0.2.0`; frontmatter bumped in the same skill edit.

WRONG: Unreleased bullet for an `AGENTS.md` rewrite.

CORRECT (cut): skill still at last-cut `0.1.0` → bump once. Skill already at `0.2.0` (user bump) → leave `0.2.0`.

## Structure

New skill: `skills/<name>/SKILL.md` (frontmatter `name` and `description`) plus `agents/openai.yaml`. Keep `SKILL.md` thin; depth goes in `references/` or `reference/`. Copy `skills/write-great-instructions/SKILL.md` and `skills/write-great-instructions/agents/openai.yaml`. User-invoked only: copy `skills/code-review-plus/SKILL.md` (`disable-model-invocation: true`) and `skills/code-review-plus/agents/openai.yaml` (`allow_implicit_invocation: false`). `interface.short_description` is 25–64 characters. ChatGPT picker fields: [optional metadata](https://learn.chatgpt.com/docs/build-skills#optional-metadata) when writing `agents/openai.yaml`. MCP `dependencies` only when the skill names a server.

Add or remove a skill: `README.md` table and `docs/structure.md` tree in the same change, plus `[Unreleased]`.

Ambiguous skill behaviour or scope: stop and ask. Do not invent a second skill or a build toolchain.

## Done when

1. Each changed `.md` path: `markdownlint -c .markdownlint.yaml <path>` exits 0
2. Diff has no reflow-only edits; long instructional lines stay on one line
3. Skill add/remove: `README.md` table and `docs/structure.md` tree updated in the same change
4. Consumer-facing change (skill, OpenCode agent, `global-rules.md`): `[Unreleased]` records it; `metadata.version` unchanged unless this change is a version cut, and then only skills still at the last-cut value. `AGENTS.md`-only: no changelog bullet
