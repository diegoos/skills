# BEM + Sass — conventions

Load when naming, 7-1 layout, or tokens need more than [`SKILL.md`](../SKILL.md)
Essentials.

## Naming detail

| Entity   | Form                              | Rule                                         |
| -------- | --------------------------------- | -------------------------------------------- |
| Block    | `.block`                          | Standalone; no `__` / `--` in the block name |
| Element  | `.block__element`                 | Part of one block; no standalone meaning     |
| Modifier | `.block--mod` / `.block__el--mod` | Extra class on the same node as the base     |

Optional namespace only if the project already uses one (`c-`, `l-`, …). Do not
invent prefixes.

Block-level modifiers may style children (`.block--mod .block__el`) per official
BEM. Prefer an element modifier or a new block when that keeps selectors
**flat**; use the parent-modifier form only when the variant truly cascades
inside one block instance.

## HTML + composition

```html
<div class="card card--highlight">...</div>
<span class="card__title card__title--large">...</span>

<header class="header">
  <a class="logo" href="/">...</a>
  <nav class="nav">...</nav>
</header>
```

Style `.card__title` directly (not `.card .card__title` or `.card h2`). Keep
parts as elements only when they are never reused outside that block.

## Directory structure (7-1)

```txt
sass/
├── abstracts/    # variables, functions, mixins (emit no CSS)
├── vendors/      # third-party
├── base/         # reset, global typography, html/body
├── layout/       # grid, header, footer, shells
├── components/   # one partial per reusable BEM block
├── pages/        # page- or route-specific
└── main.scss     # entrypoint
```

Root folder name follows the project; the internal map stays the same. Flat
partials are fine under ~12 files; then migrate to 7-1.

Entrypoint order: `abstracts` → `vendors` → `base` → `layout` → `components` →
`pages`. Prefer `@use` / `@forward`; keep `@import` only on legacy trees.

## Tokens and mixins

Centralize color, space, typography, radius, and motion in `abstracts/`.
Component partials reference tokens; magic values get a one-line comment. Mixins
for repeated patterns (reduced-motion, truncate) — they do not hide BEM names.
