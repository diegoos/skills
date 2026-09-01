# Formats

Schema for each instruction file this skill may write. Body writing follows the Principles in `SKILL.md`. Do not invent frontmatter on `AGENTS.md`.

Out of scope: `.github/agents/*.agent.md` and `SKILL.md` workflows (capability / persona, not repo policy).

## Three attach models

1. **Always-on:** every turn. Root `AGENTS.md` (most tools), `copilot-instructions.md`, `CLAUDE.md` at launch, Cursor `alwaysApply: true`, Devin root `AGENTS.md`.
2. **Glob / path:** when matching files are in context. Cursor `globs`, Copilot `applyTo`, Claude `paths:`, Windsurf/Devin `trigger: glob`.
3. **Nearest / merge / JIT:** directory tree. Semantics differ per harness — do not collapse them into one rule.

## Adapter (canonical + overlay)

Canonical source for a generic ask: root `AGENTS.md`. Overlay only what that harness cannot read.

| If the repo uses | Adapter |
| ---------------- | ------- |
| Claude Code | `@AGENTS.md` at the top of `CLAUDE.md`, plus Claude-only lines below. Symlink `ln -s AGENTS.md CLAUDE.md` when there is no Claude-only overlay. Skip the symlink when Devin CLI (or anything that loads **both** filenames always-on) is in play |
| Gemini CLI | `context.fileName` in `.gemini/settings.json` pointing at `AGENTS.md`. Emit `GEMINI.md` only when the user asked for that filename |
| Aider | `read: AGENTS.md` in `.aider.conf.yml` |
| OpenCode | Keep `AGENTS.md`. Extra files go in `opencode.json` `instructions` |
| Cursor | `.mdc` only for glob or agent-requested slices. Do not mirror the whole root as `alwaysApply: true` |
| Copilot | Pick **one** always-on: `.github/copilot-instructions.md` **or** root `AGENTS.md`. Path rules → `*.instructions.md` with `applyTo` |
| Codex | `AGENTS.md` as-is. `AGENTS.override.md` only when that directory must hide its `AGENTS.md` |
| Devin Desktop | `AGENTS.md` for directory scope; `.devin/rules` when the trigger is not "this folder" |

Copy mirrors are last resort. When a copy exists, keep it verbatim with the canonical section.

## Caps

| Harness | Budget |
| ------- | ------ |
| Codex `AGENTS.md` | 32 KiB **cumulative** along root→CWD |
| Root `AGENTS.md` (heuristic) | Warn above ~150 lines |
| Claude `CLAUDE.md` | Target ~200 lines; `@import` still counts at launch |
| Cursor `.mdc` | Target ≤500 lines per file |
| Copilot instruction file | Soft cap ~1000 lines |
| Devin/Windsurf rule | 12k chars workspace, 6k global |

## AGENTS.md

- **Path:** repo root; optional nested file per package. Also `AGENTS.override.md` (same directory: override wins, `AGENTS.md` ignored). `AGENTS.local.md` is personal; gitignore it.
- **Frontmatter:** none. Plain Markdown.
- **Body:** headings the repo earns (stack, commands, style with a snippet, constraints, boundaries, git). No required section names.
- **Nested:** Codex concatenates Git root → CWD (one file per directory). Child that must change a parent command **states the replacement**. Devin Desktop inherits parent; nested `AGENTS.md` = glob `dir/**`.
- **Danger:** treating `AGENTS.override.md` and `AGENTS.md` as a pair in one directory (Codex reads only the override). Committing `AGENTS.local.md`.

## CLAUDE.md

- **Path:** `CLAUDE.md` or `.claude/CLAUDE.md` at project root; nested `CLAUDE.md` in subdirs (JIT when Claude reads that tree). `CLAUDE.local.md` beside it (after `CLAUDE.md`; gitignore). User file: `~/.claude/CLAUDE.md`.
- **Frontmatter:** none on `CLAUDE.md`. `.claude/rules/*.md` may use YAML `paths:` (list of globs). Missing `paths:` = always-on.
- **Body:** same policy as `AGENTS.md`. Target ~200 lines. `@path` imports expand at launch (depth 4, relative to the importing file). `@` inside fences and code spans is not an import. HTML comments are stripped (human notes).
- **Danger:** assuming Claude reads `AGENTS.md` natively. Importing an encyclopedia (`@` still counts toward launch tokens). Tracking `CLAUDE.local.md`.

## GEMINI.md

- **Path:** `GEMINI.md` at project root and/or `~/.gemini/GEMINI.md`. Filename override: `.gemini/settings.json` → `context.fileName` (project `.gemini/` wins over user `~/.gemini/`).
- **Frontmatter:** none.
- **Body:** same policy. `@file.md` imports, default depth 5. Concatenated memory is sent every prompt; `/memory show` is the ground truth.
- **Danger:** emitting `GEMINI.md` while the CLI is configured to read only `AGENTS.md` (or the reverse) without updating `context.fileName`.

## Cursor rules

- **Path:** `.cursor/rules/*.mdc` only. A `.md` in that folder is ignored. Legacy `.cursorrules` at repo root: migrate, do not grow.
- **Frontmatter:** `description` (string), `globs` (comma-separated string per Cursor docs), `alwaysApply` (boolean).
- **Modes:** `alwaysApply: true` → always-on (globs and description ignored). `globs` set → path attach. `description` only → agent-requested (the description is the pointer). None of the three → **manual** (never fires alone).
- **Body:** one concept per file. Target ≤500 lines.
- **Danger:** defaulting to manual by omitting all three fields. Putting `alwaysApply: true` on a copy of the whole `AGENTS.md`.

## Copilot instructions

- **Path:** `.github/copilot-instructions.md` (always-on). `.github/instructions/**/*.instructions.md` (path-specific).
- **Frontmatter:** none required on `copilot-instructions.md`. Path files: `applyTo` (glob, comma-separated, repo-relative). Optional `name`, `description`, `excludeAgent` (`code-review` or `cloud-agent`). Missing `applyTo` on VS Code → file does not auto-apply.
- **Body:** same policy. Soft cap ~1000 lines per file.
- **Danger:** shipping both `copilot-instructions.md` and root `AGENTS.md` as always-on. Putting `@imports` in `*.instructions.md` or `GEMINI.md` (Copilot does not expand those).

## Aider

- **Path:** any Markdown listed under `read:` in `.aider.conf.yml` (often `AGENTS.md` or `CONVENTIONS.md`).
- **Frontmatter:** none. No glob, no nested discovery.
- **Body:** the file `read:` points at.
- **Danger:** writing `AGENTS.md` and expecting Aider to find it without `read:`.

## OpenCode

- **Path:** `AGENTS.md` (wins over `CLAUDE.md` in the same category) plus optional `instructions` globs/URLs in `opencode.json`. User: `~/.config/opencode/AGENTS.md`.
- **Frontmatter:** none. `@` in the Markdown is not expanded; list extra files in `instructions` or teach a Read.
- **Danger:** relying on `@AGENTS.md` the way Claude does.

## Devin / Windsurf rules

- **Path:** prefer `.devin/rules/*.md`. Legacy `.windsurf/rules/*.md`. Root `AGENTS.md` is also read (always-on at root; nested = glob `dir/**`; child inherits parent).
- **Frontmatter:** `trigger`: `always_on` / `glob` / `model_decision` / `manual`. `globs` when trigger is `glob`. `description` when `model_decision`.
- **Body:** cap 12k characters per workspace rule; 6k global.
- **Danger:** using nested `AGENTS.md` for a cross-cutting glob (`*.test.ts`) instead of a rule with `trigger: glob`.
