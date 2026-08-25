# Product register

Load when [load-map.md](load-map.md) attaches this file to the current slot. Unanswered blanks belong to the Packet. Direction picks `recipe=`. Implement reads the matching heading and does not pick a new recipe.

When design serves the product: app UI, dashboards, admin, settings, data tables, tools, authenticated surfaces.

Stance: transact. The interface disappears into the task. No three visual occupancy cards. No catalog Pick.

## Job before recipe

Before Lock `recipe=`, write from the Briefing card:

1. *job* — “The user is here to ______.” No hero, card, sidebar.
2. *objects* — domain nouns + verb (know / do / compare / monitor / decide). At most 7. Success stays.
3. P0 — one perception, one action. Everything-is-P0 fails.

Done when Packet `job=` and `P0=` exist and Primary is an *object*, not “the dashboard.” Then pick one recipe when the view is a CMS/admin/CRM home, list, editor, or accounts. Settings and other tools stay on the [app shell](#app-shell).

## Surface map

One recipe per view. No fifth id.

| Surface | Recipe |
| --- | --- |
| CMS / admin / editorial home | `queue-home` (`main` = what needs me now) |
| CRM home (deals, tickets, pipeline that asks for action) | `queue-home` |
| Record catalog, inbox, ops list, CRM list | `list-filter` |
| Deal / post / record / deep settings that edit | `editor` |
| People and roles | `accounts` |
| Settings and tools outside those four | app shell only |
| *Job* is BI, not a queue | Shared analytics-type: KPI Label→Value→Delta→Time; chart only with a question; table or queue below |

A CMS/CRM/list/editor/accounts view with `recipe=` missing fails Direction.

## Product slop test

Would a user fluent in the category's best tools trust this? Linear, Figma, Notion, and Stripe Dashboard set that bar.

Failure mode: strangeness without purpose (over-decorated buttons, display fonts on labels, motion with no state meaning, reinvented affordances).

## Pareto screens

The Lock names the 1–2 screens that carry the product's value. Only those may receive extra craft (macro whitespace, cinematic motion, nested enclosure). Settings, repeated empty states, and CRUD stay in this register.

## Typography

One sans family for headings, body, labels, and data. Fixed rem scale (fluid clamp headings stay on brand). System stacks (Inter, SF Pro, system-ui) when they match the project. Type pairing waits for Implement when [typography.md](typography.md) is attached.

## Color

Default: **Restrained** (near-neutral surfaces + accent ≤10%). Semantic states carry status. Accent for primary actions and selection. Mode from briefing Theme. Hue from briefing Palette when it applied. Strategy, states, dark canvas: [color.md](color.md) when attached.

## Layout

Responsive means structure (collapse sidebar, responsive tables). Dense when users need it. Spacing and alignment group first; a border or card is last. A card is a self-contained clickable unit (feed item, catalog preview). Not for KPI rows, settings rows, table rows, or form groups. Nested cards fail here.

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
- Controls stay inside the rail (Implement [surfaces.md](surfaces.md#chrome-containment) when attached).
- Lock `theme=system`: labeled theme control in the top bar; not the filled primary ([color.md](color.md#system-theme)).

### Density

Match row height and padding to frequency of use: compact scales for data-dense, daily-use tools; comfortable scales for occasional or first-run surfaces. Offer a density toggle only when both audiences share one view.

### Data tables

- Left-align text, **right-align numbers**; align decimals on the same column.
- Sticky header; sticky first column when rows are wide.
- Truncate with tooltip rather than wrapping cells unpredictably.
- Built-in empty, loading (skeleton rows), and error states.
- Responsive: collapse to stacked key/value cards on mobile, or prioritize columns and hide the rest behind expand. Keep a primary table inside the viewport.
- Large datasets: paginate or virtualize (≥50 visible rows).

## Components

Full state cycle: `default → hover → focus → active → disabled → loading → error`.

- Skeleton loaders for content loading
- Empty states that teach the interface
- Same button shape, form vocabulary, icon style across screens

## Motion

150–250ms transitions. Motion shows state. Skip orchestrated page-load sequences. Reduced motion: instant or crossfade. Product micro (press `0.96`, interruptible, row restraint) at Implement when [motion.md](motion.md) is attached.

## Forms

Field contract: Implement [production-engineering.md](production-engineering.md#forms) when attached. Prefer native controls. Prefer inline and progressive patterns over a modal.

Do not open [ux-principles.md](ux-principles.md) in this slot. Implement attaches it for app UI.

## Product permissions

- System fonts and familiar navigation (top bar + side nav, tabs, command palette)
- Consistency over surprise screen-to-screen
- Delight saved for moments (success, empty state, onboarding)

Labels, buttons, and table data stay on the product family. Motion tells wait for QA.

## Onboard

Open when the prompt names onboarding, first-run, empty, or activation. Marketing stays closed.

First-run is one next step that completes the Job. It is not a KPI gallery, a feature tour, or a welcome `h1` in `main`. Empty names what is missing and the action that fills it. Activation copy leaves after day one; the queue recipe remains. Delight only on success, empty, or this first-run — not on every chrome control.

Done when `main` still matches Packet `recipe=` (or settings when `recipe=none`) and greeting nodes in `main` = 0.

## Dashboards

CMS, admin, editorial tools, and operator homes are **functional product-homes**. Chart families wait for Implement (ux-principles Dashboards). Do not open [ux-principles.md](ux-principles.md) or [anti-slop.md](anti-slop.md) from this file. Familiar chrome is the bar (Linear, Figma, Notion) — not a unique poster.

Pick **one recipe per view** from Job when the surface is a CMS/admin/CRM home, list, editor, or accounts. Settings and other tools stay on the [app shell](#app-shell). Write the *job* phrase, *objects*, and P0 first ([Job before recipe](#job-before-recipe)), then the three operator questions. Lock `recipe=` to that id when a recipe applies. Extra craft only on the 1–2 Pareto screens.

**Scan 10s.** Headlines are the three operator questions this view answers in `main`. Primary is an *object*, not “the dashboard.”

**Read.** Ranked rows. Tabular numbers. Every KPI that exists has Label → Value → Delta → Time. Filters on the same plane as the list (≥8 rows → ≥1 visible filter).

**Edit.** One filled primary = the persist verb (Save / Book / Assign), visible. Back restores scroll and filters. Empty, loading, and error on the list or the canvas.

**Chrome.** Top bar + side nav, or master-detail. One work area. Controls inside the rail. Command palette may pair. Island nav, display face on labels, and landing motion fail here.

### queue-home

CMS / admin / editorial **home**. `main` answers "what needs me now?"

- `h1` names the queue (Drafts, Scheduled, Failing, Assigned) — not a greeting
- Filters visible in `main` (not overflow-only)
- One filled primary in the view header
- KPI optional: one strip, 1 hero number + at most 2 ranked siblings. Never 4 equal cards
- Workflow objects exist as rows in `main`, not only as nav

Done when greeting nodes in `main` = 0, filled primary count = 1, ≥1 list or table in `main`, and each KPI (if any) has Label → Value → Delta → Time.

### list-filter

Ops list, inbox, catalog of records. The table or dense list is the spine.

- Search plus 2–4 filters on the same plane as the list
- Empty, loading (skeleton rows), and error on the list
- Same chrome as editor and accounts

Done when a view with ≥8 rows has ≥1 visible filter, and the three list states exist in markup.

### editor

Create and edit. Same nav, tokens, and control vocabulary as the list.

- Content canvas + meta panel
- Save is the filled primary and stays visible
- Do not invent a second nav

Done when filled primary count = 1 and that control is Save (or the Job's persist verb).

### accounts

People and roles. Not a second analytics wall.

- Rows are people or seats; filters are role / status
- Same chrome as list and editor

Done when `main` is a people list or table, not a KPI gallery.

### Shared

- **KPI anatomy** (when a KPI exists): Label → Value → Delta → Time window. Missing a part: cut or fix.
- **Analytics-type views** (when Job is BI, not CMS home): KPIs top if any → charts middle only with a question → tables/queue bottom.
- **Color:** legend and status; the same meaning across pages. Restrained. "Professional" is density and predictability, not catalog `id=professional`.
- Lock `style=none`. Leave [design-styles.md](design-styles.md) closed unless the user named a catalog `id`.
- Chrome stays inside the rail (Implement when [surfaces.md](surfaces.md) is attached).

Apply brand register only to marketing/about surfaces within the same product.
