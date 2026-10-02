---
name: make-changelog
description: >-
  Maintain CHANGELOG.md in Keep a Changelog form. Use when starting a changelog, when the user asks to record a changelog entry, or when the user asks to bump or release.
metadata:
  version: 0.1.0
  author: "Diego Oliveira"
  tags:
    - changelog
    - keep a changelog
    - semver
    - release
---

# Make changelog

[Keep a Changelog](https://keepachangelog.com/en/1.1.0/) 1.1.0. The **scheme** is the project's version convention. None → [SemVer](https://semver.org/spec/v2.0.0.html).

**Invariants:** Notes sit under `[Unreleased]` until a bump. Sections are Added, Changed, Deprecated, Removed, Fixed, Security. Write a section only when it has a bullet. Newest release first. Dates are `YYYY-MM-DD`. A bump runs only when the user explicitly asks. A `version` key in tool config (`.vscode/launch.json`, `.vscode/tasks.json`, a Compose file `version:`) is that file's schema, not the product version. Use the changelog file the repo already has. None → root `CHANGELOG.md`.

## Commands

| Invocation | Branch |
| --- | --- |
| `/make-changelog init` | **init** |
| `/make-changelog update`, or a request to record changelog entries | **update** |
| `bump`, `bump version`, `/make-changelog bump`, or a release request | **bump** |

Name the branch at the start. With no bump or release request: **init** when the changelog file is missing; **update** when it exists and the task is to record changes. A missing file on update or bump runs init, then that branch continues.

A question uses the harness question tool, or chat when that tool is missing. Wait. The next message resumes the branch at that step.

## Layout

A **monorepo** has an explicit signal: a workspace member list, or the root docs call it a monorepo and name the package directories. No signal → a normal project. Do not scan the tree.

A recorded choice in the standing block or the root changelog stays. Otherwise ask once, then wait. List packages as `name — path`.

- Each package. The root changelog only links to them. → `per package`
- Root only. One changelog at the repo root. → `root only`

**Done when:** the run is `normal`, or `monorepo` with the package list and the choice.

## Branch init

1. **Owners.** A release tool that already generates the changelog (changesets, release-please, semantic-release, standard-version) → ask whether this skill maintains it, then wait, unless the standing block already says. Record the choice as one sentence in that block. The tool keeps it → stop. Create no changelog file. **Done when:** this skill owns the file, or the run stopped.
2. **File.** An existing changelog stays as it is. A missing file uses the intro below and an empty `[Unreleased]`. The intro names the scheme. `per package`: that intro in each package directory; the root file names each package and links to its changelog. **Done when:** every file this layout needs exists, and a file created this run has an empty `[Unreleased]`.
3. **Standing.** Add the block in [standing.md](references/standing.md). **Done when:** the block is present once. A `normal` block does not mention monorepo. A `CLAUDE.md` that only imports `@AGENTS.md` was left unchanged.

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
```

Any other scheme: keep the Keep a Changelog sentence. Replace the second sentence with `and this project versions with <scheme>.`

## Branch update

One concise bullet per notable change in `[Unreleased]`: what a user of the product would miss. One line. End with a period. Scope is this task's diff. Older commits only when the user asks to catch up. Skip format-only edits, comments, generated files, lockfiles, and tool config. A breaking change starts with `Breaking:`.

`per package`: write the detail in that package's `[Unreleased]`. The root gets one link for that package (`name`: see `path/CHANGELOG.md`). `root only`: start the bullet with the package name.

A file with releases and no `[Unreleased]` gets that heading above them. A file that is not a changelog → ask before rewriting it.

**Done when:** each notable change is a new bullet or a skip, and no version heading or product field changed.

## Branch bump

An explicit bump or release request is required. Otherwise stop. `bump` and `bump version` name no version. A version token in the request (`1.2.3`, `2026.09.30`) is the version to write. Strip a leading `v`.

An ambiguous scheme or two product versions → ask, then wait. That turn writes no version heading and no product field. An empty `[Unreleased]` asks whether to cut anyway.

1. Move the `[Unreleased]` sections under `## [version] - YYYY-MM-DD`. Leave `[Unreleased]` empty. Match a heading shape the file already uses. A release the user says was pulled adds `[YANKED]`.
2. The notes pick the next SemVer. Major `0`: Fixed or Security alone → patch; any other section → minor. Stay below `1.0.0` unless the user asks. No product version yet → `0.1.0`. Major `1` or higher: `Breaking:` or Removed → major; Added or Deprecated → minor; otherwise patch. A confirmed empty cut → patch. Another scheme → the increment the repo already uses. A prerelease (`-rc.1`), or a version shared by more than one package → ask before writing.
3. Write that version into the product field that held the previous one. A pointer field (`version.workspace = true`, a dynamic version) stays; write the file it points at. Leave dependency ranges, lockfiles, and tool-config `version` keys.
4. Keep an existing link footer in its current style, including the repo's tag prefix.

More than one changelog has notes → ask which to cut. A package cut leaves the root link under `[Unreleased]`. A root cut writes a root product field only when that field is the product being cut.

A commit or a tag happens only when this request asked. Reply with `previous → new`, the changelog path, and the product-field path.

**Done when:** the new heading is dated, `[Unreleased]` is empty, and the product field matches it.
