# Surfaces

Load when [load-map.md](load-map.md) attaches this file to the current slot. Unanswered blanks belong to the Packet.

In-flow product chrome: dashboard, admin, CMS, settings. Marketing enclosure waits for material-craft when that path is attached. Layout and queues are Packet `recipe=`. Motion technique is Product micro in this slot when [motion.md](motion.md) is attached.

Done when every check below holds at 1024px and 1440px, or failed and fixed.

## Chrome containment

Nav and toolbar controls sit fully inside the chrome padding box. Labels truncate or wrap. The control does not grow past the rail. Lock `theme=system`: the theme control sits in the header padding box ([color.md](color.md#system-theme)).

Hard guardrail: no negative margin, drop shadow, or hit-area pseudo that crosses a chrome edge. Do instead: inset, `min-width: 0` on the flex child, truncate with a keyboard-reachable full string (tables wrap or ellipsize inside the rail).

Hover and press use color, opacity, or compositor `transform` that still clips to the parent. Press feedback does not change padding, border, or width ([production-engineering.md](production-engineering.md)).

## Padding inside the rail

Rail padding is at least the control's own padding. A filled primary in the sidebar cannot kiss or cross the rail edge. One filled primary per view; a second copy in the header fails.

## Concentric radius

Nested surfaces that sit close: `outerRadius = innerRadius + padding`. Padding larger than `24px`: choose each radius independently.

Nested cards stay a fail. This formula is for chrome (rail, header, inset well, selected row), not a second card stack.

## Optical alignment

Icon plus label: icon-side padding = text-side padding minus `2px`. Optical nudge stays inside padding; it does not pull the control over the edge.

## Elevation vs structure

Same-plane chrome (sidebar, table, filters): hairline or token border. Overlays (dropdown, modal, popover): elevation token, one light source ([design-systems.md](design-systems.md) when attached).

Hard guardrail: do not use drop shadow to fake a sidebar or toolbar button as an overlay. Do instead: fill plus hairline on the product plane.

## Hit areas

Touch and below `lg`: targets ≥44px with ≥8px gap ([production-engineering.md](production-engineering.md)). Dense desktop may draw a 40px control; the hit box still reaches 44px **inside** the parent. Adjacent hit boxes do not overlap; shrink the extension first. Containment beats inflated padding: shrink type or icon, do not clip.

## Numeric rendering

KPI Value and Delta, live counters, and numeric table columns use `font-variant-numeric: tabular-nums`. Skip IDs, phones, zips, versions, and static decorative numerals.

Apply `-webkit-font-smoothing: antialiased` (and `-moz-osx-font-smoothing: grayscale`) once on `html`, not per component.

`text-wrap: balance` on the view `h1`–`h3` only. `text-wrap: pretty` on short helper and empty-state copy. Neither on tables, code, or prose of 10+ lines.

## Icon chrome

One family and one stroke weight in sidebar, header, and row actions. Label 14–16px / 400 → `1.5px` stroke; 500–600 → `2px`. Chrome glyphs at `16` / `20` / `24` only.

SVGs use `currentColor`. No hardcoded `fill` / `stroke` hex on chrome icons. Outline at rest; fill for the active destination.

Recipe depth: [assets.md](assets.md). This file stays the check; do not open assets.md unless the user asked a visual restyle.

## CSS budget

Name the properties that change. Zero `transition: all` / `transition-all`. `will-change` only on `transform`, `opacity`, or `filter`, and only while the element is animating.

Product press: `scale(0.96)` with an interruptible transition ([motion.md](motion.md#product-micro)). High-frequency rows: background or opacity ≤150ms, no entrance replay.
