---
name: markdown-editor
description: >-
  Creates or updates Markdown (`.md`|`.mdc`|`.mdx`) files. Use when writing or editing any `.md` file; creating or updating documentation, README, changelog, or ADR; reviewing or fixing Markdown formatting and lint; editing YAML frontmatter in Markdown. Applies the Google Markdown Style Guide. Do not use for non-Markdown files.
compatibility: Works with any agent capable of reading and writing files.
---

# Markdown editor

## Workflow

1. **Identify the document type** (README, ADR, changelog, guide, reference) and match tone and structure to it.
2. **Write or edit** applying every formatting rule below — including frontmatter when present or required.
3. **Pass the quality checklist** before delivering.

Done when the file is lint-clean, follows every rule here, and matches the document type.

## Document structure

Prefer this layout (Google Style Guide):

```markdown
# Document Title

Brief introduction (1–3 sentences on purpose).

[TOC]

## Topic

Content.

## See also

- <https://link-to-more-info>
```

- H1 matches or closely mirrors the filename. Only one H1; further headings start at `##`.
- Introduction comes **before** `[TOC]`. Omit `[TOC]` on plain GitHub/GitLab (Gitiles/MkDocs only).
- Reference links under "See also" at the end.
- With frontmatter, H1 is the first heading **after** the closing `---` — not the first line of the file.

## Formatting rules

### Prose: no hard line breaks

Never soft-wrap or hard-break prose to fit a column. Keep instructional sentences, list items, and table cells on one line. Break only on semantic boundaries: heading, new list item, blank line, or fence.

### Lists

Blank line before and after lists. Unordered: `-` only — never mix `*`, `+`, `-`. Ordered: `.` delimiter, never `)`. Long or mutable ordered lists: lazy numbering (`1.` on every item). Nested lists: 4-space indent; blank line between top-level items that have children.

### Code

Fenced blocks only (never 4-space indent), with a language tag (`txt` for plain text). Blank line before and after. Inline backticks for filenames, fields, commands, and variables; also for example paths/URLs that must not autolink.

### Headings

ATX (`#`) only — never setext (`===` / `---`). Space after `#`. Blank line before and after. One H1. Do not skip levels. Prefer unique, descriptive heading text (avoid repeated "Overview" / "Example").

### Links

No bare URLs — use `[text](url)` or `<url>`. Descriptive link text (never "here" / "click here" / "link"). Long URLs (especially in tables): reference links; define them just before the next section heading, or at file end if shared.

### Emphasis

`**bold**` and `*italic*` — not `__` / `_` (asterisks work mid-word across parsers).

### Whitespace

Spaces for indent, never tabs. No trailing whitespace. Prefer a new paragraph over forced line breaks; if you must break inside a paragraph, use a trailing `\` (not two spaces). File ends with exactly one trailing newline.

### Blockquotes

Blank line before and after. Multi-paragraph quotes: `>` on blank lines between paragraphs.

### Images, tables, HTML

Images: descriptive alt text; use sparingly (prefer prose). Tables: only for genuinely tabular data; otherwise use a list. Prefer native Markdown over HTML; HTML only as last resort.

## Frontmatter

Frontmatter is optional YAML metadata at the **very top** of the file, between `---` fences. It must be the first thing in the file. Parsers treat the block as YAML — indentation and types matter.

```markdown
---
title: Configuration guide
description: How to set up the local environment
tags:
  - setup
  - docker
published: true
---

# Configuration guide

Body starts here.
```

### Edit rules

- **Preserve schema** unless asked to change it — keep existing keys, casing, and list style.
- **Key-value pairs** only. Meaningful keys (`description`, not `desc`; `author`, not `auth`). Consistent naming (camelCase, snake_case, or kebab-case — match the file/repo).
- **Arrays** for multi-values — never a comma-separated string:

  ```yaml
  authors:
    - Ada Lovelace
    - Grace Hopper
  ```

- **Explicit types**: numbers as numbers (`year: 2026`), booleans as `true`/`false` (not `"yes"`). Quote strings that would otherwise parse as another type.
- **Spaces only** for YAML indent — never tabs. Indent consistently (2 spaces is conventional).
- **Multiline** with `|` (keep newlines) or `>` (fold). Comments with `#` are fine.
- **No HTML** inside frontmatter values.
- After the closing `---`, continue with normal Markdown (H1, then body). A later `---` in the body is a thematic break or setext hazard — blank line above horizontal rules.

### When to add or change frontmatter

Add or update frontmatter when the user asks, the project convention requires it (SSG, CMS, skill metadata), or you are editing fields that already exist. Do not invent a frontmatter block for plain docs that never used one.

## Gotchas

- Blank line before lists is required — without it, some parsers treat the list as a paragraph.
- `---` immediately under text becomes a setext H2; put a blank line above thematic breaks.
- Missing final newline fails MD047 and many CI checks.

## Quality checklist

Before finishing:

- [ ] Every formatting rule above applied (prose unbroken; lists, code, headings, links, emphasis, whitespace).
- [ ] Frontmatter (if any): first in file, valid YAML, meaningful keys, explicit types, no HTML, schema preserved.
- [ ] Single H1 (after frontmatter when present); ATX headings; no skipped levels.
- [ ] No bare URLs; descriptive link text.
- [ ] File ends with exactly one trailing newline.
