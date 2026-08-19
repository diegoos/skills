# Pre-Flight Checklist

Run after *crit*. Unanswered blanks: [briefing.md](briefing.md). Run the tier that matches [task routing](../SKILL.md#task-routing). Fix failures before shipping. Skip tiers that do not apply.

Tier B and C are **mechanical**: count in the DOM. A failed count means the page is not done.

## Tier A — Always (every UI deliverable)

### Direction

- [ ] Task type identified (component / app UI / marketing)
- [ ] Origin named: `greenfield` (new UI), `redesign` (existing page from the briefing), or `polish` (improve existing UI). Existing surface: [redesign.md](redesign.md) read; audit listed; Lock `style=none`; Catalog closed
- [ ] Briefing: every blank asked and answered this run via `AskQuestion` (one field per turn), or *invent-all*. A chat dump of questions fails. Skipping Theme, Palette, Behave, or Stack while still blank (when those apply) fails. App UI: Look skipped as `none`; a Catalog table in chat fails. Marketing Look blank required the Catalog table in chat plus four fitting ids and a specify option ([briefing.md](briefing.md#look)). Greenfield marketing `you-decide` / invent-all: Pick written; median cluster refused ([design-styles.md](design-styles.md#pick)). Redesign, polish, and app UI: Catalog closed; app UI Look is `none` unless the user named an `id`. Inferred wordmark, audience, CTA, style-from-job, theme-from-job, or palette-from-job fails — [briefing.md](briefing.md)
- [ ] `DESIGN.md` followed or created; CSS tokens match — [design-md.md](design-md.md)
- [ ] Files match [file-architecture.md](file-architecture.md) (default: `index.html` + `main.css` + `main.js`; no stylesheet dumped into HTML)
- [ ] Design Read declared (required for app UI and marketing)
- [ ] Lock line present: origin, name, scene, theme (`light` / `dark` / `system`), color strategy, layout/motion/density bands, stack
- [ ] *Crit* written (frame + triad + scan including logo-swap); P0 fixed; common-layout = no; first viewport fails a logo-swap; alternative is a layout family in the DOM or rejected with a user-goal reason — [crit.md](crit.md)
- [ ] Register correct when not an isolated component (brand vs product)

### Viewport and type

- [ ] Viewport is `width=device-width, initial-scale=1` with no `maximum-scale=1` or `user-scalable=no`
- [ ] Body and form controls ≥16px on mobile (inputs included — iOS zoom)

### Document structure

- [ ] Skip link is the first focusable control and targets `#main`; `<main id="main">` exists (page/app shell; skip for an isolated component)
- [ ] One `h1` per view; heading levels sequential (no `h1` → `h3` skip)

### Anti-slop

- [ ] Does not read as generic AI output (purple gradient hero, 3 equal cards, charcoal + orange spec sheet, default kit chrome, portable slogans) — slop test including common-layout, interchangeability, deletion, and code-floor checks ([anti-slop.md](anti-slop.md#the-slop-test))
- [ ] No em dashes (`—`) in visible copy

### Color

- [ ] One color strategy chosen; single accent locked page-wide (not a new accent per section)
- [ ] Lock `theme=light` or `theme=dark`: that one palette on `html`; theme-control count = 0
- [ ] Lock `theme=system`: light tokens and dark tokens both in CSS; labeled theme control count ≥ 1 in chrome; activating it sets `data-theme` or a class on `html` and surface tokens change. Media-query-only (control count = 0) fails. Dark-only or light-only CSS fails — [color.md](color.md#system-theme)
- [ ] Dark `--surface` / `--surface-raised` are near-neutral charcoal unless Palette named a tinted field or Lock `color=drenched` — [color.md](color.md#dark-mode-construct-dont-invert)

### Typography and contrast

- [ ] Clear hierarchy (not everything bold)
- [ ] Body contrast ≥4.5:1; buttons readable on their background
- [ ] Meaningful icons/controls ≥3:1 against adjacent color
- [ ] Headings do not overflow at mobile/tablet breakpoints

### Tap quality

- [ ] Touch targets ≥44px **and** ≥8px gap between adjacent targets
- [ ] Press feedback via color, opacity, or elevation — padding/border/width do not change
- [ ] Icon-only controls have an accessible name; decorative icons beside visible text are `aria-hidden`

### Interaction and a11y

- [ ] Default, hover, focus, active on interactive elements
- [ ] Loading, error, empty states where the flow needs them
- [ ] Async submit: control disabled (or second click ignored) with a loading label
- [ ] Keyboard navigable; semantic HTML; visible focus
- [ ] Sticky/fixed chrome and overlays do not cover the focused control (`scroll-padding` matches chrome height)
- [ ] Primary actions work on click/tap — hover is enhancement, not the only path
- [ ] `prefers-reduced-motion` respected when motion is used

### Responsive

- [ ] Works at 320px, 768px, and 1024px without horizontal scroll
- [ ] At 768 and 1024, a multi-column grid has N items in N cells (odd last item spans remaining columns; an empty bordered shell fails) — [layout-patterns.md](layout-patterns.md#grids-and-lists)

### Forms (when the surface has a form)

- [ ] Field groups follow [production-engineering.md](production-engineering.md#forms) (visible label + control + error in one grid cell). One inline error on a paired row: the next row's labels share a y. Odd last field spans remaining columns.

### Honesty

- [ ] State what was NOT verified (build, axe, real devices, screen reader)

---

## Tier B — Marketing surfaces only

Add when building landing pages, portfolios, or campaigns. Also read [layout-patterns.md](layout-patterns.md). Count in the markup.

### Layout (count)

- [ ] Hero: headline ≤2 lines desktop; subtext ≤20 words; stack ≤4 text elements; top padding ≤6rem; primary CTA visible without scroll
- [ ] Logo / "used by" wall lives **under** the hero, not inside it
- [ ] Eyebrows: count `uppercase` + wide tracking above section headlines; count ≤ `ceil(sectionCount / 3)`; hero counts as 1
- [ ] Each layout family appears at most once; no 3 consecutive image+text zigzags
- [ ] Mixed-span grids: ≥2 cells have real visual variation (image, tint, pattern)
- [ ] Stacked CTAs below `md` fill the content column (no unused track beside a short button)
- [ ] Intra-fold gaps follow Lock `density=` ([design-systems.md](design-systems.md#density-bands)); `6rem`–`10rem` is between sections only
- [ ] Horizontal marquee ≤1 per page
- [ ] Nav: one line at desktop `lg`; height ≤80px
- [ ] One filled primary per fold (same CTA may repeat later in AIDA; two competing filled buttons in one fold fail)

### Visual

- [ ] Marketing surface uses real imagery (gen-tool first, then real/seed photo, then labeled `TODO` slots) — not div fake screenshots; zero images is a fail unless the brief is abstract-only
- [ ] Alt text on content images
- [ ] Memorable detail named in the Lock exists in the DOM (one material or spatial break — not a bezel on every card)

### Copy

- [ ] No duplicate CTA intent on the same page
- [ ] CTA labels fit one line at desktop
- [ ] Copy self-audit against [anti-slop.md](anti-slop.md#copy-tells): every visible string re-read; portable or LLM-pattern sentences rewritten; one copy register per page

---

## Tier C — App UI and dashboards only

Add when building dashboards, settings, admin, or dense tools. Also read [product-register.md](product-register.md) and [surfaces.md](surfaces.md).

### Product UI

- [ ] Follows project design system; consistent component vocabulary. Kit theme, type, and radius match DESIGN.md (code floor, not a look)
- [ ] Display fonts not used on labels, buttons, or table data
- [ ] Modals not used when inline or progressive patterns suffice
- [ ] One filled primary action per view; secondary/tertiary visually quieter; destructive separated from the primary and from main nav
- [ ] Input control matches the choice: radio (2–5 exclusive, all visible), checkbox (independent), select (long list), toggle (persistent binary)
- [ ] Nav marks the current location; back restores scroll and filters
- [ ] Lists/tables with ≥50 visible rows paginate or virtualize
- [ ] Craft extra (material enclosure, cinematic motion, macro whitespace) only on the 1–2 Pareto screens named in the Lock

### Forms (when the view has a form)

- [ ] Each field: visible label, semantic `type`/`inputmode`, real `autocomplete`, required indicator, helper/error via `aria-describedby`
- [ ] Validate on blur and submit (errors stay off during typing)
- [ ] Failed submit: focusable error summary plus inline errors
- [ ] Auth fields (if present): paste allowed; `autocomplete` for username/password; no `autocomplete="off"` on those fields

### Dashboard (if applicable)

- [ ] Lock `style=none` unless Look is a named catalog `id`. Zero Catalog table in this run's chat
- [ ] `h1` in `main` is not a greeting ("Welcome back", "Good morning"). Greeting nodes in `main` = 0
- [ ] If KPI cards exist: they are not 4 equal siblings. Each KPI node has four text roles: label, value, delta, time
- [ ] If a pie/donut exists: slice count ≤ 3. Each chart has an adjacent title that is a question or a decision, not a noun ("Traffic", "Devices")
- [ ] CMS/admin home: ≥1 table or work-queue list in `main` (not charts-only)
- [ ] List view with ≥8 rows: ≥1 visible filter control (not only a "Filters" overflow)
- [ ] Each widget and the main list: empty, loading/skeleton, and error exist in markup
- [ ] One primary nav pattern. Destinations include the Job objects (list, create/edit, users), not Analytics-only
- [ ] Avatar control count in chrome ≤ 1. Filled primary count per view = 1
- [ ] Chrome containment: every nav and toolbar control sits inside the rail padding box at 1024 and 1440 ([surfaces.md](surfaces.md#chrome-containment))
- [ ] KPI Value and Delta, live counters, and numeric table columns use `tabular-nums`
- [ ] Zero `transition: all` / `transition-all` in shipped CSS
- [ ] One icon family and one stroke weight in sidebar, header, and row actions

### Performance (page-level app shells)

- [ ] Heavy UI isolated to separate routes/server requests; images sized and lazy-loaded below fold

### Conditional

- [ ] Drag/sort (if present): keyboard and simple-pointer alternative
- [ ] PWA / `viewport-fit=cover` (if present): `env(safe-area-inset-*)` on fixed chrome

---

Short approval is valid for small components when Tier A passes and scope is narrow.
