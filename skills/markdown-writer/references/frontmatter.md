# YAML frontmatter

A YAML block at the top of a Markdown file.

## Shape

The block is the first bytes of the file, between `---` fences. After the closing `---`, the first heading is the H1.

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

Add or update a block when the user asks, dest convention requires it (SSG, CMS, skill metadata), or you are editing keys that already exist.

## Edit rules

- **Preserve schema** unless asked to change it: existing keys, casing, and list style.
- **Key-value pairs** only. Meaningful keys (`description`, not `desc`). Match dest naming (camelCase, snake_case, or kebab-case).
- **Arrays** for multi-values:

    ```yaml
    authors:
      - Ada Lovelace
      - Grace Hopper
    ```

- **Explicit types**: `year: 2026`, `published: true`. Quote a string that would parse as another type (`"on"`, `"null"`, `"2026-08-16"`).
- **Spaces** for YAML indent (2 spaces is conventional). Fold with `>` or keep newlines with `|`. `#` comments are fine.
