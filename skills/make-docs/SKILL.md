---
name: make-docs
description: >-
  Writes architecture docs and observable behavior specs under `docs/`. Use when the user asks to document a codebase, write architecture docs or behavior specs, explore a repo for documentation, sync or update docs after changes, refresh or regenerate stale docs against current code, or record an ADR or architecture decision. Skip when the task is an agent instruction file, a changelog, a skill, application code, or Markdown outside that suite.
metadata:
  version: 0.4.0
  author: "Diego Oliveira"
  tags:
    - docs
    - architecture
    - specs
    - adr
---

# Make docs

Write architecture (how the system is structured) and specs (what it does) under `docs/`. Specs name observable outcomes an agent can implement or verify. Paths in this file and in `references/` resolve from this skill folder.

## Inputs

- `codebase` (workspace, required): the tree to document. It comes from the workspace.
- `request` (text, optional): a branch name or an unnamed docs ask. It comes from the user message.
- `docs/` (directory, optional): an existing suite, when the workspace has one.

When the workspace has no project files, stop and report the missing codebase as the next thing to provide.

## Steps

1. **Branch.** Pick one path. **explore:** `docs/` is missing, or the user asked to generate a suite or explore the codebase for documentation. **update:** `docs/` exists and the user asked to sync docs after changes or commits. **refresh:** `docs/` exists and the user asked to regenerate docs, or said the docs are stale, against the current tree. **adr:** the user asked to record one architecture decision. When `docs/` exists and the message names no branch signal, ask once which branch to run. When one message carries both a sync signal and a stale signal, ask once which branch to run. **Done when:** the run names one of those four branches and the signal that selected it. When `docs/` is missing, that signal may be the missing suite. When `docs/` exists and the message names no signal, or names both a sync signal and a stale signal, the branch is named only after the user answers.
2. **Run** that branch. Open its first phase file. Open the next phase file only when the current file's completion criterion holds. A hunter reads only its own file under `references/hunters/`. **Done when:** every phase listed for that branch meets the completion criterion in its phase file.

## Branches

| Branch | Open first | Then |
| --- | --- | --- |
| explore | `references/phases/survey.md` | `references/phases/confirm.md`, then `references/phases/generate.md`, then `references/phases/verify.md` |
| update | `references/phases/update.md` | `references/phases/verify.md` |
| refresh | `references/phases/refresh.md` | survey, confirm, generate, verify, in the order that file states |
| adr | `references/phases/adr.md` | `references/phases/verify.md` |

## Invariants

Every claim cites a path, an observable command, or a config. A section with no evidence is omitted, and the reason stays in chat. One language per suite. Identifiers and BCP 14 keywords stay as in source. Load `references/language.md` on confirm, generate, and verify. Hunters collect evidence and the orchestrator writes the files. The index is `docs/README.md`, with a line `> Updated on` and today's ISO date. Scan rules (one topic per heading, commands in backticks, heading depth at h3) live in `references/anti-slop.md`, loaded on generate and verify.

## Output

```text
docs/
  README.md
  architecture/
    architecture.md
    domains/
      glossary.md
      api.md
      constraints.md
    decisions/
    patterns.md
  specs/
    <domain>.md
```

`api.md` exists only when the project exposes an API. One spec file per confirmed behavioral domain. The survey file names which files a small repo, a larger repo, or a monorepo earns. Replace every template example from evidence, or cut the row.

## Templates

Load the matching template before writing the file.

| Template | Writes |
| --- | --- |
| `references/template-readme.md` | `docs/README.md` |
| `references/template-architecture.md` | `docs/architecture/architecture.md` |
| `references/template-glossary.md` | `docs/architecture/domains/glossary.md` |
| `references/template-api.md` | `docs/architecture/domains/api.md` |
| `references/template-constraints.md` | `docs/architecture/domains/constraints.md` |
| `references/template-adr.md` | `docs/architecture/decisions/ADR-*.md` |
| `references/template-patterns.md` | `docs/architecture/patterns.md` |
| `references/template-spec.md` | `docs/specs/<domain>.md` |

## Boundaries

Data model, observability, and CI/CD stay out of the suite unless the survey lists them and confirm accepts them.

An existing canonical always-on file (`AGENTS.md`, or the one always-on file already in the repo) may gain one when-to-read line for `docs/README.md`. The procedure is in `references/phases/generate.md`. The run leaves every other instruction-file line as it found it, and it does not create `AGENTS.md`.
