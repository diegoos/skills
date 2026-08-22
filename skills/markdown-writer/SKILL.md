---
name: markdown-writer
description: >-
  Write Markdown (`.md` / `.mdc` / `.mdx`). Use when creating or editing a Markdown file, or YAML frontmatter in one.
metadata:
  version: 0.1.0
  author: "Diego Oliveira"
  tags:
    - markdown
    - markdown-writer
---

# Markdown writer

Write Markdown that _scans_ and _parses_. Dest file conventions and dest lint config win.

## Workflow

1. **Match dest.** Path, document type (including `.mdc` / `.mdx` extras dest owns: JSX, rule schema), existing layout, lint config if any, and _prose wrap_ (one-line or wrap). Dest requires wrap when MD013 is on, `.editorconfig` sets `max_line_length` for Markdown, or the file already wraps. **Done when:** those five are named.
2. **Write.** Apply [Write](#write). Load [frontmatter.md](references/frontmatter.md) when YAML is at the top or dest requires it. **Done when:** every applicable Write rule is visible in the file.
3. **Prove.** Read the headings only. Check each list, table, and fence against Parse. Run `markdownlint` on changed `.md` / `.mdc` / `.mdx` paths when dest has the tool or a `.markdownlint.yaml`. **Done when:** the headings are the outline, each list/table/fence matches Parse, and that command exits 0 or dest has no linter. One-line dest: keep prose on one line if MD013 fires.

## Write

**Scan.** First sentence under the H1 names the file's job. Headings are the outline: ATX (`# Heading`), one H1 (first heading after frontmatter `---` if any), each heading one level deeper than its parent, unique text that names the section. H1 mirrors the filename. Blank line around headings.

**Parse.** Parallel facts → list. Records with the same fields → table. Copy-paste or syntax → fenced block. A link's text names the target.

**Prose.** One sentence, list item, or table cell per line. Break only on a heading, new list item, blank line, or fence. Wrap to a column only when Match dest named wrap.

**Lists.** Marker `-`. Ordered lists use `1.` (lazy `1.` on long or mutable lists). Nested items, continuations, and fences inside an item indent 4 spaces. Nest at most one extra level. Blank line before and after the list.

**Tables.** Header, hyphen delimiter, data rows. `|` on both ends of every row. Same cell count on every row.

**Code.** Fenced block with a language tag (`txt` when there is none). Blank line around the fence. Inline backticks for filenames, fields, commands, variables, and example paths.

**Links.** `[label](url)` or `<url>`. Images: `![alt](url)` with alt that describes the image. Long URLs: reference links, defined just before the next heading or at file end if shared.

**Emphasis.** `*italic*` and `**bold**`. Bold only words that change a decision.

**Blocks.** Blank line around quotes and tables. Multi-paragraph quotes keep `>` on the blank lines between them. Markdown over raw HTML. A `---` thematic break only when dest already uses that pattern; blank line above `---` so the previous line stays a paragraph.

**Tasks.** `- [ ]` / `- [x]` at the start of the item.

**Whitespace.** Spaces for indent. File ends with one newline. A line break inside a paragraph is a trailing `\`.

**Shape.** `[TOC]` only on Gitiles/MkDocs. See also at the end when dest already uses that pattern.
