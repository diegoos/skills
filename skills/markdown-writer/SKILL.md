---
name: markdown-writer
description: >-
  Creates or updates Markdown (`.md` / `.mdc` / `.mdx`). Use when writing or editing Markdown, fixing Markdown formatting, or editing YAML frontmatter in a Markdown file.
metadata:
  version: 0.1.0
  author: "Diego Oliveira"
  tags:
    - markdown
    - markdown-writer
---

# Markdown writer

Write Markdown that reads as intended and parses as written. Dest file conventions and dest lint config win.

## Workflow

1. **Match dest.** Path, document type, existing layout, lint config if any, and _prose wrap_ (one-line or wrap). Dest requires wrap when MD013 is on, `.editorconfig` sets `max_line_length` for Markdown, or the file already wraps. **Done when:** those five are named.
2. **Write.** Apply [Write](#write). Load [frontmatter.md](references/frontmatter.md) when YAML is at the top or dest requires it. **Done when:** every applicable Write rule is visible in the file.
3. **Prove.** Run `markdownlint` on changed `.md` / `.mdc` / `.mdx` paths when dest has the tool or a `.markdownlint.yaml`. **Done when:** that command exits 0, or dest has no linter. One-line dest: keep prose on one line if MD013 fires.

## Write

**Prose.** One sentence, list item, or table cell per line. Break only on a heading, new list item, blank line, or fence. Wrap to a column only when Match dest named wrap.

**Headings.** ATX (`# Heading`). One H1; with frontmatter, it is the first heading after the closing `---`. Each heading is one level deeper than its parent. Unique heading text. H1 mirrors the filename. Blank line around headings. Blank line above `---` so the previous line stays a paragraph.

**Lists.** Marker `-`. Ordered lists use `1.` (lazy `1.` on long or mutable lists). Nested items, continuations, and fences inside an item indent 4 spaces. Blank line before and after the list.

**Code.** Fenced block with a language tag (`txt` when there is none). Blank line around the fence. Inline backticks for filenames, fields, commands, variables, and example paths.

**Links.** `[descriptive text](url)` or `<url>`. Images: `![alt](url)` with alt that describes the image. Long URLs: reference links, defined just before the next heading or at file end if shared.

**Emphasis.** `*italic*` and `**bold**`.

**Blocks.** Blank line around quotes and tables. Multi-paragraph quotes keep `>` on the blank lines between them. Markdown over raw HTML.

**Tables.** Header, hyphen delimiter, data rows. `|` on both ends of every row. Same cell count on every row. Tabular data only.

**Tasks.** `- [ ]` / `- [x]` at the start of the item.

**Whitespace.** Spaces for indent. File ends with one newline. A line break inside a paragraph is a trailing `\`.

**Shape.** Brief intro under the H1. `[TOC]` only on Gitiles/MkDocs. See also at the end when dest already uses that pattern.
