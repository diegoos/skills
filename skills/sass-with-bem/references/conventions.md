# BEM + Sass — conventions

Rules past the pattern in [`SKILL.md`](../SKILL.md). Shapes are in [`examples.md`](examples.md).

## Namespace

Add a prefix only when the project already uses one (`c-`, `l-`, and the same form). A new project uses a bare block name.

## Parent modifier

A block modifier may style a child as `.block--mod .block__el`. Prefer an element modifier, or a new block, so the selector stays one class. Use the descendant only when that variant cascades inside one instance of the block.

## Layout

```txt
sass/
├── abstracts/    # variables, functions, mixins only
├── vendors/
├── base/
├── layout/
├── components/   # one partial per block
├── pages/
└── main.scss
```

The root folder name follows the project. This internal map stays.

Flat partials are the layout under 12 partials. Use this map when the tree is already 7-1, or when this change reaches 12 partials. A layout the repo documents stays.

Entrypoint order: `abstracts` → `vendors` → `base` → `layout` → `components` → `pages`. A new tree uses `@use` and `@forward`. An existing `@import` tree stays on `@import`.

## Tokens

Color, space, typography, radius, and motion live in `abstracts/`. A component partial uses those tokens. A one-off value gets a one-line comment. A mixin repeats a pattern such as reduced motion or truncation. The mixin keeps the BEM class name in the partial.
