# Product register

When design serves the product: app UI, dashboards, admin, settings, data tables, tools, authenticated surfaces.

Stance: transact. The interface disappears into the task.

## Product slop test

Would a user fluent in the category's best tools trust this? Linear, Figma, Notion, and Stripe Dashboard set that bar.

Failure mode: strangeness without purpose (over-decorated buttons, display fonts on labels, motion with no state meaning, reinvented affordances).

## Pareto screens

The Lock names the 1–2 screens that carry the product's value. Only those may receive extra craft (macro whitespace, cinematic motion, nested enclosure). Settings, repeated empty states, and CRUD stay in this register.

## Typography

One sans family for headings, body, labels, and data. Fixed rem scale (fluid clamp headings stay on brand). System stacks (Inter, SF Pro, system-ui) when they match the project. Detail: [typography.md](typography.md).

## Color

Default: **Restrained** (tinted neutrals + accent ≤10%). Semantic states carry status. Accent for primary actions and selection. Strategy, states, dark mode: [color.md](color.md).

## Layout

Responsive means structure (collapse sidebar, responsive tables). Dense when users need it. Cards only for independent clickable units. Nested cards fail here. Details: [layout-patterns.md](layout-patterns.md#cards).

### App shell

| Pattern | When |
| --- | --- |
| **Top bar + side nav** | Broad navigation, many sections. Default app shell. |
| **Top bar only** | Few destinations; nav fits one row |
| **Split / master-detail** | List drives a detail pane (mail, inbox, settings) |
| **Command palette** | Power users; pairs with any shell as a fast path |

- Persistent nav in a predictable place; collapse the side nav to icons or a drawer below `lg`, with an affordance. Bottom nav ≤5, icon+label, top-level only. Mark where the user is. Back restores scroll and filters.
- One primary work area per view; secondary panels (filters, inspectors) dock.
- One filled primary per view.

### Density

Match row height and padding to frequency of use: compact scales for data-dense, daily-use tools; comfortable scales for occasional or first-run surfaces. Offer a density toggle only when both audiences share one view.

### Data tables

- Left-align text, **right-align numbers**; align decimals on the same column.
- Sticky header; sticky first column when rows are wide.
- Truncate with tooltip rather than wrapping cells unpredictably.
- Built-in empty, loading (skeleton rows), and error states.
- Responsive: collapse to stacked key/value cards on mobile, or prioritize columns and hide the rest behind expand. Keep a primary table inside the viewport.
- Large datasets: paginate or virtualize; see [ux-principles.md](ux-principles.md#dashboards-and-data-ui).

## Components

Full state cycle: `default → hover → focus → active → disabled → loading → error`.

- Skeleton loaders for content loading
- Empty states that teach the interface
- Same button shape, form vocabulary, icon style across screens

## Motion

150–250ms transitions. Motion shows state. Skip orchestrated page-load sequences. Reduced motion: instant or crossfade.

## Forms

Field contract: [production-engineering.md](production-engineering.md#forms). Prefer native controls. Prefer inline and progressive patterns over a modal.

More UX patterns: [ux-principles.md](ux-principles.md).

## Product permissions

- System fonts and familiar navigation (top bar + side nav, tabs, command palette)
- Consistency over surprise screen-to-screen
- Delight saved for moments (success, empty state, onboarding)

Labels, buttons, and table data stay on the product family. Motion tells: [anti-slop.md](anti-slop.md#motion-tells).

## Dashboards

Audience types and chart rules: [ux-principles.md](ux-principles.md#dashboards-and-data-ui).

Apply brand register only to marketing/about surfaces within the same product.
