# AGENTS.md

Collection of Markdown skills (`skills/<name>/SKILL.md`). Ship Markdown only — no package manager, build, or test suite. `.opencode/agents/` is optional OpenCode; it is not the skills install contract.

## Commands

- Lint changed Markdown: `markdownlint -c .markdownlint.yaml <path>` (exit 0). Config: `.markdownlint.yaml`.
- MD013 is off (`.markdownlint.yaml`, `.editorconfig` `[*.md]`). One-line prose, list items, and table cells. Break on a heading, new list item, blank line, or fence. If MD013 fires, fix the config.

## Permission boundaries

| Mode             | Paths                                                                                                                   |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------- |
| WRITE            | `skills/**`, `docs/**`, `README.md`, `AGENTS.md`, `CHANGELOG.md`, `.editorconfig`, `.markdownlint.yaml`, `.opencode/**` |
| NEVER            | force-push, rewriting git history                                                                                       |
| HUMAN_CHECKPOINT | publishing or removing a skill from the public registry; deleting a skill directory                                     |

## Precedence

1. Explicit user instruction for this turn
2. This `AGENTS.md`
3. The `SKILL.md` / `references/` of the skill being edited
4. Generic Markdown style guides — keep MD013 off

## Changelog

`CHANGELOG.md` is for consumers of a skill, an OpenCode agent, or `global-rules.md`. Record those changes under `[Unreleased]` (Keep a Changelog sections as needed). Skip `AGENTS.md` and other contributor-only repo policy.

Leave `[Unreleased]` in place until the user asks to cut a version. Leave `skills/<name>/SKILL.md` `metadata.version` unchanged while work sits in `[Unreleased]`. A new skill may set an initial `metadata.version`; bump it only on the next cut. The user may bump `metadata.version` before a changelog cut. When the user asks to cut a version, for each skill with entries in that release: compare the current `metadata.version` to that skill's frontmatter at the last dated `CHANGELOG.md` heading. If it is already newer, leave it. If it still matches the last-cut value, bump it once in the same change (one bump per skill per cut). Do not invent a changelog version to match a skill bump. No version arrow on Unreleased bullets.

CORRECT (skill edit): `[Unreleased]` gains a bullet; `metadata.version` in `SKILL.md` stays put.

WRONG: Unreleased bullet with `0.1.0 → 0.2.0`; frontmatter bumped in the same skill edit.

WRONG: Unreleased bullet for an `AGENTS.md` rewrite.

CORRECT (cut): skill still at last-cut `0.1.0` → bump once. Skill already at `0.2.0` (user bump) → leave `0.2.0`.

## Skills

Each skill lives in `skills/<name>/` with `SKILL.md` (frontmatter `name` and `description`; `disable-model-invocation: true` only for user-invoked-only). Keep `SKILL.md` thin; depth goes in `references/` or `reference/`. Ship `agents/openai.yaml` for ChatGPT/Codex ([optional metadata](https://learn.chatgpt.com/docs/build-skills#optional-metadata)): `interface.display_name`, `interface.short_description` (25–64 characters), `policy.allow_implicit_invocation: false` when `disable-model-invocation: true`, otherwise `true`. Add MCP `dependencies` only when the skill needs a named server.

Add or remove a skill: update the table in `README.md` and the tree in `docs/structure.md` in the same change, plus `[Unreleased]`.

Ambiguous skill behaviour or scope: stop and ask. Do not invent a second skill or a build toolchain.

## Done when

1. Each changed `.md` path: the Commands lint exits 0
2. Diff has no reflow-only edits; long instructional lines stay on one line
3. Skill add/remove: `README.md` table and `docs/structure.md` tree updated in the same change
4. Consumer-facing change (skill, OpenCode agent, `global-rules.md`): `[Unreleased]` records it; `metadata.version` unchanged unless this change is a version cut, and then only skills still at the last-cut value. `AGENTS.md`-only: no changelog bullet
