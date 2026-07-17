---
name: sass-with-bem
description: >-
  BEM + Sass/SCSS with flat compiled selectors. Use when writing or reviewing .scss/.sass or BEM classes in markup. Branches: write, review.
metadata:
  version: 0.1.0
  author: "Diego Oliveira"
  tags:
    - sass
    - scss
    - bem
    - sass-with-bem
---

# BEM + Sass (SCSS)

Sass organizes the source; compiled CSS stays **flat** — one class selector per component rule.

**Precedence:** human override or local repo doc > this skill > personal habit > generic framework examples.

Pick a **branch** and state it at the start of the run:

- author / change styles or BEM classes → **write**
- audit styles for BEM → **review**

Load [`conventions.md`](references/conventions.md) when naming, 7-1 layout, or tokens need more than Essentials. Load [`examples.md`](references/examples.md) on **write** when a concrete shape helps.

## Branch A — write

1. **Discover the style tree.** Entrypoint, layout (7-1 / flat / legacy), import style (`@use` preferred; `@import` only if already legacy). No structure → create the 7-1 map in `conventions.md`. **Done when:** entrypoint path, layout shape, and import style are recorded.
2. **Name the surface.** Apply the **axiom** and prefer **composition**. Design variant → `--modifier`. Runtime / JS → `is-` / `has-*`. **Done when:** every new class matches Pattern (plus optional existing namespace / `is-` / `has-*` / `js-`); no `block__a__b`.
3. **Author SCSS.** Nest with `&` only to build BEM names; output stays **flat**. Cap at block → element → element-modifier. Tokens from `abstracts/`; one partial per block; wire new partials into the entrypoint.
   **Done when:** markup has base + modifier together; selectors are single-class (plus intentional `.block.is-active`); tokens used; `prefers-reduced-motion` if motion was added.
4. **Verify.** Run Branch B against the change. **Done when:** every applicable checklist item is true.

## Branch B — review

Report each failure with selector/path. Stay on the repo’s methodology.

- [ ] Classes only for components (no `id`, no tag-as-component)
- [ ] No `block__a__b`; deep subtrees are new blocks
- [ ] Modifiers in HTML include the base class
- [ ] Compiled CSS is **flat** (no `.block .block__el` cascade)
- [ ] Variants use `--*`; transient states use `is-` / `has-*`
- [ ] Values from central tokens (or one-line local exception)
- [ ] One partial per block (or clearly named layout)
- [ ] Tree is 7-1 or the repo’s documented legacy layout
- [ ] Motion respects `prefers-reduced-motion` when applicable

**Done when:** every applicable item is checked; each failure cites a selector or file.

## Essentials (every branch)

### Pattern

```txt
block
block__element
block--modifier
block__element--modifier
```

Lowercase, digits, hyphens. Classes only. Modifier always with its base class.

### Axiom

1. One context only → **element**.
2. Many contexts → independent **block**.
3. Blocks nest blocks; never `block__a__b` — extract a block (**composition**).

### Nesting → flat

`&__el` / `&--mod` append suffixes; compiled selectors stay single-class. See [`examples.md`](references/examples.md).

### States vs modifiers

| Kind           | Form            | Use                    |
| -------------- | --------------- | ---------------------- |
| Design variant | `--*`           | theme, size, layout    |
| Transient / JS | `is-*`, `has-*` | active, open, loading  |
| JS hook only   | `js-*`          | no presentational SCSS |

### Scope

- **WRITE:** style-tree SCSS; BEM classes in markup for the same feature.
- **READ:** entrypoint, tokens/abstracts, existing class patterns.
- **NEVER:** change methodology unprompted; emit CSS from `abstracts/`; ship a modifier without its base class.

New writing uses `&` nesting; output stays **flat**. Refactor legacy only inside the requested scope.
