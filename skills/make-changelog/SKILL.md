---
name: make-changelog
description: >-
  Maintains CHANGELOG.md in Keep a Changelog form. Use when the user asks to start a changelog, add or record an entry, update the changelog, bump a version, cut a release, or release a version. Skip when the task is only to commit, amend, tag, or publish, or when it is to format or lint Markdown, to write architecture or behavior docs, to edit agent instructions for a reason other than the changelog, or to write a skill.
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

**Invariants.** Notes sit under `[Unreleased]` until a bump. Sections are Added, Changed, Deprecated, Removed, Fixed, Security. Write a section only when it has a bullet. Newest release first. Dates are `YYYY-MM-DD`. A bump runs only when the user explicitly asks.

## Inputs

- `request` (text, required): the message that selects the branch. A version token in it (`1.2.3`, `2026.09.30`) is the version to write.
- `changes` (diff or stated list, required on update): what this task changed. Older commits count only when the request asks to catch up.
- `changelog` (file, optional): the file the repo already uses. None → root `CHANGELOG.md`.

When update has no diff and no stated changes, stop and ask what to record. Until that answer arrives, write no bullet.

A question uses the harness question tool, or chat when that tool is missing. Wait. The next message resumes the branch at that step.

## Output

- **init:** the changelog path and the file that holds the standing block. When a release tool keeps the file, the reply says the tool owns it and names no new changelog.
- **update:** each notable change as a new bullet or a skip. No version heading and no product field changed.
- **bump:** one line, `previous → new`, the changelog path, and the product-field path. A pointer field names the file it points at.

## Branch

Name the branch at the start.

| Invocation | Branch |
| --- | --- |
| `/make-changelog init` | **init** |
| `/make-changelog update`, or a request to record or add notes | **update** |
| `bump`, `bump version`, `/make-changelog bump`, `cut`, or a release request | **bump** |

With no bump, cut, or release request: **init** when the changelog file is missing; **update** when it exists and the task is to record changes. A missing file on update or bump runs init, then that branch continues.

**Done when:** the run has named **init**, **update**, or **bump**.

## Layout

A **monorepo** has an explicit signal: a workspace member list, or the root docs call it a monorepo and name the package directories. No signal → a normal project. Leave the tree unscanned.

A recorded choice in the standing block or the root changelog stays. Otherwise ask once, then wait. List packages as `name — path`.

- Each package. The root changelog only links to them. → `per package`
- Root only. One changelog at the repo root. → `root only`

**Done when:** the run is `normal`, or `monorepo` with the package list and the choice.

## Branch init

1. **Owners.** A release tool that already generates the changelog (changesets, release-please, semantic-release, standard-version) → ask whether this skill maintains it, then wait, unless the standing block already says. Record the choice as one sentence in that block. The tool keeps it → stop before a changelog file exists. **Done when:** this skill owns the file, or the run stopped with no changelog file created and the reply names the tool.
2. **File.** An existing changelog stays as it is. A missing file uses the intro below and an empty `[Unreleased]`. The intro names the scheme. `per package`: that intro in each package directory; the root file names each package and links to its changelog. **Done when:** every file this layout needs exists, and a file created this run has an empty `[Unreleased]`.
3. **Standing.** Read [references/standing.md](references/standing.md) when writing the standing block, and copy the block for this layout. **Done when:** that block is present once, in the one file the Where list selects, and the reply names every changelog path for this layout and the file that holds the block.

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
```

Any other scheme: keep the Keep a Changelog sentence. Replace the second sentence with `and this project versions with <scheme>.`

## Branch update

One concise bullet per notable change in `[Unreleased]`: what a user of the product would miss. One line. End with a period. Scope is `changes`. Skip format-only edits, comments, generated files, lockfiles, and tool config. A breaking change starts with `**Breaking:**`.

Never alter bullets outside the `[Unreleased]` section unless the user explicitly requests this. Edits must be strictly limited to adding new bullets under `[Unreleased]`, or the minimal structural changes needed to create or position an `[Unreleased]` heading. All other bullets or sections are left unchanged unless the user asks to edit or move content outside `[Unreleased]`.

`per package`: write the detail in that package's `[Unreleased]`. The root gets one link for that package (`name`: see `path/CHANGELOG.md`). `root only`: start the bullet with the package name.

A file with releases and no `[Unreleased]` gets that heading above them. A file that is not a changelog → ask before rewriting it, and leave it unchanged until the answer.

**Done when:** each notable change is a new bullet or a skip under `[Unreleased]`, no version heading or product field changed, no bullet outside `[Unreleased]` changed unless the user asked, and a file that is not a changelog is unchanged until the user agrees.

## Branch bump

Run this branch only when the request is an explicit bump, cut, or release. Any other request stops. `bump` and `bump version` name no version. A commit or a tag is part of this branch only when the request asked for it.

1. **Scope.** More than one changelog has notes → ask which to cut, then wait. **Done when:** one changelog is selected. The run asked first when more than one has notes.
2. **Empty.** An empty `[Unreleased]` on that file asks whether to cut anyway, then wait. **Done when:** the file has notes, or the user confirmed an empty cut.
3. **Version.** An ambiguous scheme or two product versions → ask, then wait, and leave the heading and the product field unchanged until the answer. A version token in `request` is the version. Strip a leading `v`. Otherwise the notes pick the next SemVer. Major `0`: Fixed or Security alone → patch; any other section → minor. Stay below `1.0.0` unless the user asks. No product version yet → `0.1.0`. Major `1` or higher: `Breaking:` or Removed → major; Added or Deprecated → minor; otherwise patch. A confirmed empty cut → patch. Another scheme → the increment the repo already uses. A prerelease (`-rc.1`), or a version shared by more than one package → ask before writing. **Done when:** the version is the request's token with no leading `v`, or, when the request has no token, the increment in this step. The run asked first when the scheme is ambiguous, two product versions exist, the version is a prerelease, or the version is shared by more than one package.
4. **Heading.** Move the `[Unreleased]` sections under `## [version] - YYYY-MM-DD`, using the date of the cut. Leave `[Unreleased]` empty. Match a heading shape the file already uses. A release the user says was pulled adds `[YANKED]`. **Done when:** the notes sit under the dated heading and `[Unreleased]` is empty.
5. **Product field.** Write that version into the product field that held the previous one. A pointer field (`version.workspace = true`, a dynamic version) stays; write the file it points at. A `version` key in tool config (`.vscode/launch.json`, `.vscode/tasks.json`, a Compose file `version:`) is that file's schema. Leave it, along with dependency ranges and lockfiles. A package cut leaves the root link under `[Unreleased]`. A root cut writes a root product field only when that field is the product being cut. **Done when:** the field that holds the product version matches the heading. A pointer field is unchanged and the file it points at matches. Tool-config `version` keys, dependency ranges, and lockfiles are unchanged. A package cut left the root link under `[Unreleased]`. A root cut wrote a root product field only when that field is the product being cut.
6. **Footer.** Point an existing link footer at the new version in its current style, including the repo's tag prefix. **Done when:** a footer that existed keeps its style, keeps its older links, and names the new version, and a file without a footer still has none.

**Done when:** steps 1–6 each met their criterion, and the reply is one line, `previous → new`, the changelog path, and the product-field path.
