# Standing block

Copy one block. `normal` uses the normal block. `per package` and `root only` use their blocks. A changelog path other than root `CHANGELOG.md` replaces that phrase in the block.

An existing `## Changelog` heading gets only the missing sentences. A release-tool choice is one extra sentence in that section.

## Normal

```markdown
## Changelog

Record notable changes in the root `CHANGELOG.md` under `[Unreleased]`: one concise bullet in the matching Keep a Changelog section (Added, Changed, Deprecated, Removed, Fixed, Security). Omit empty sections. Bump a version only when the user explicitly asks. Never bump on your own.
```

## Monorepo, per package

```markdown
## Changelog

This repo is a monorepo. Each package has its own `CHANGELOG.md`. The root `CHANGELOG.md` only names the package that changed and links to that file. Record the notable detail in the package file, under `[Unreleased]`. Bump a version only when the user explicitly asks. Never bump on your own.
```

## Monorepo, root only

```markdown
## Changelog

This repo is a monorepo. One root `CHANGELOG.md` covers every package. Name the package in the bullet. Bump a version only when the user explicitly asks. Never bump on your own.
```

## Where

One file.

1. `CLAUDE.md` is import-only when every non-blank line is `@AGENTS.md` or `@./AGENTS.md`. Edit `AGENTS.md` only. Create `AGENTS.md` when it is missing. Leave that `CLAUDE.md` unchanged.
2. Else `AGENTS.md` exists → edit `AGENTS.md` only.
3. Else `CLAUDE.md` exists → edit `CLAUDE.md` only.
4. Else create `AGENTS.md` with the block.

Place the section after the existing policy sections.
