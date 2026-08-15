# Design systems

Reuse project tokens and components before inventing new patterns.

## Tokens over magic values

```css
/* Good */
color: var(--text-primary);
background: var(--surface-elevated);
padding: var(--space-4);

/* Bad */
color: #374151;
padding: 13px;
```

Semantic naming: `text-primary`, `bg-surface`, `border-default` — not raw hex in components.

## Spacing scale

Use a consistent scale (4px / 8px increments). Never invent one-off values like `13px` or `2.3rem`.

## Density bands

The Lock `density` value selects the spacing range. Use the project's token names; these rem values are the contract.

| Band | Section / stack rhythm | Typical use |
| --- | --- | --- |
| **airy** | 1.5rem–6rem component; 6rem–10rem between brand sections | Marketing manifesto, portfolios |
| **regular** | 1rem–4rem | Default product and most landings |
| **dense** | 0.5rem–2rem | Daily-use dashboards, data tools |

`wild` layout + `airy` density is the usual brand combination. Product defaults to `regular` or `dense`. Macro brand padding does not apply to the hero top (cap `6rem`).

## Z-index scale

Define semantic layers — never arbitrary `z-9999`:

```
dropdown → sticky → modal-backdrop → modal → toast → tooltip
```

## Corner radius discipline

Pick ONE radius system per page: all sharp, all soft (12–16px), or all pill on interactive elements. Mixed radii only with a documented rule.

## Elevation scale

Define elevation as a token scale. Each level pairs a purpose with one shadow value.

| Token | Plane | Shadow | Use |
| --- | --- | --- | --- |
| `--elevation-0` | flat | none | base surface, page background |
| `--elevation-1` | raised | subtle, tight | cards, inputs at rest |
| `--elevation-2` | overlay | medium, softer | dropdowns, popovers, sticky bars |
| `--elevation-3` | modal | large, diffuse | dialogs, command palette |

- **Border vs shadow:** low-contrast borders separate same-plane regions; shadows imply a higher plane. Pick one job per edge.
- One light source — keep shadow offset/direction consistent across the scale.
- Avoid stacking multiple arbitrary shadows for "depth"; layered shadows are one considered value, not three pasted together.
- **Dark mode**: shadows barely read on dark surfaces. Convey elevation with lighter surface tokens instead ([color.md](color.md#dark-mode-construct-dont-invert)).

## One system per project

Pick one official system that matches the brief and customize within it.

| Brief reads as…        | Reach for                                    |
| ---------------------- | -------------------------------------------- |
| Enterprise / Microsoft | Fluent UI                                    |
| Material-flavored      | Material Web (M3)                            |
| IBM B2B / analytics    | Carbon                                       |
| Shopify admin          | Polaris                                      |
| US government          | USWDS                                        |
| Modern accessible UI   | Radix Themes, accessible component libraries |
| Fast MVP               | Tailwind CSS                                 |

## When no design system exists

1. Read existing project CSS/tokens/theme before inventing new patterns
2. Extract recurring colors, spacing, and type into variables
3. Build components that match neighboring screens

## Register token strategies

| Register | Color strategy | Typography |
| --- | --- | --- |
| Brand | Committed or Drenched often appropriate | Display + body pairing common |
| Product | Restrained default | Often one sans family |

Strategy definitions and palette construction: [color.md](color.md#color-strategies).

## Library customization

Component libraries must be **customized** to the project aesthetic. Shipping default theme state reads as uncrafted.
