---
name: sass-with-bem
description: >-
  Writes BEM Sass (.scss, .sass) whenever the work touches a stylesheet that uses BEM. Use when the work writes, edits, or fixes .scss, .sass, scss, or sass whose classes are BEM (block, block__element, block--modifier), or the user mentions BEM, bem, a block, an element, a modifier, nesting, a partial, or styles in that Sass. Skip when the Sass does not use BEM, the task is only a review or audit, application logic with no stylesheet and no BEM class, a visual redesign with no stylesheet, plain CSS with no BEM class, Tailwind or utility classes, CSS modules, styled-components, or a pull-request review for bugs or security.
metadata:
  version: 0.2.0
  author: "Diego Oliveira"
  tags:
    - sass
    - scss
    - bem
    - sass-with-bem
---

# Sass with BEM

Write Sass so each compiled component rule is one class. `&` may build that class name.

When a repo style doc covers the same rule, follow the doc and name the file.

Load [`references/conventions.md`](references/conventions.md) when you judge layout, tokens, a namespace, or a parent-modifier descendant.
Load [`references/examples.md`](references/examples.md) when the change adds a block, an element, or a modifier.

## Inputs

- `request` (text, required): the work that touches the Sass. It comes from the user message.
- `styles` (files, optional): the `.scss`, `.sass`, and markup already in scope. They come from the workspace or the message. An empty tree is valid.

## Steps

1. **Discover.** Find the entrypoint, the layout (7-1, flat partials, or the repo's documented layout), and the import style (`@use` or `@import`). **Done when:** those three facts are named, or the run states `tree: none` and the assumption that new files use `@use` and flat partials. When the request names no Sass or BEM change and no BEM Sass is in scope, stop and ask what to write. When workspace search is unavailable, name the open files, state that the rest of the tree was not searched, and leave every other file unchanged.
2. **Write** the Sass and the markup for this request. Match the tree from Discover. `tree: none` adds the partials this request needs and wires them at one entrypoint with `@use`. A new partial in an existing tree uses that tree's import style. Follow Pattern, Composition, Flat nesting, and States. **Done when:** those files are saved; every class this request adds or edits satisfies Pattern, Composition, Flat nesting, and States; a parent-modifier descendant is only the exception in [`references/conventions.md`](references/conventions.md); each value uses a token or a one-line comment; each new partial is wired from the entrypoint; the tree matches the layout rule in [`references/conventions.md`](references/conventions.md); motion added in this change includes `prefers-reduced-motion`.

## Pattern

```txt
block
block__element
block--modifier
block__element--modifier
```

Lowercase, digits, and hyphens. A component selector is a class. An `id` that only pairs a label stays. A modifier is a second class on the same node as its base (`class="block block--modifier"`).

## Composition

1. One context only → element.
2. Many contexts → its own block.
3. A block contains blocks. The chain stops at one element.

The rule selector is `.block__element`.

## Flat nesting

`&__element` and `&--modifier` append to the parent name.

```scss
.card {
  &__title {
    color: $color-text;
  }

  &--highlight {
    border-color: $color-accent;
  }
}
```

This compiles to `.card__title` and `.card--highlight`. A block `&--modifier` sits as a sibling of `&__element`. An element `&--modifier` stays inside that `&__element`.

## States

| Kind | Form | Use |
| --- | --- | --- |
| Design variant | `--*` | theme, size, layout |
| Transient | `is-*`, `has-*` | active, open, loading |
| JS hook | `js-*` | presentational rules stay on the BEM class |
