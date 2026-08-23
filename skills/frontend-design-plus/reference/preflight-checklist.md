# Pre-Flight Checklist

Run from the QA slot ([dispatch.md](dispatch.md#qa)) after *crit*. Isolated component: this window. Unanswered blanks: the Packet. Run the tier that matches [task routing](../SKILL.md#task-routing). QA records each box pass or fail and does not edit. The parent resumes Implement with failed boxes as P0. Skip tiers that do not apply.

Tier B and C are **mechanical**: count in the DOM. A failed count means the page is not done.

## Tier A — Always (every UI deliverable)

### Direction

- [ ] Task type identified (component / app UI / marketing)
- [ ] Origin named: `greenfield` (new UI), `redesign` (existing page from the briefing), or `polish` (improve existing UI). Existing surface: [redesign.md](redesign.md) read; audit listed (redesign: keep/retire vs Aim; polish: [craft audit](redesign.md#craft-audit) with P0/P1 closed); Lock `style=none`; Catalog closed
- [ ] Briefing: every remaining blank asked and answered this run via `AskQuestion` (one field per turn), or *invent-all*. A chat dump of questions fails. Skipping Scene, Theme, Palette, Use, or Stack while still blank (when those apply) fails. Unnamed Behave and Constraints are owner `none`; asking them when the prompt did not name motion, states, artifacts, or restrictions fails. App UI: Scene and Look skipped as `none`; a Catalog table in chat fails. Greenfield marketing Scene blank required `You decide from the brief` plus two occupancy readings ([briefing.md](briefing.md#scene)). Greenfield marketing Look was not asked: unnamed Look is owner `you-decide`; a Catalog table in the parent chat fails ([briefing.md](briefing.md#look)). Greenfield marketing Scene `you-decide` / invent-all: occupancy from *objects* and *kinship* in [composition.md](composition.md); `fallback=yes` only with “fallback, not thesis”. Greenfield marketing Look `you-decide` (including silence) / invent-all: Pick written and matched to Packet *tension* ([design-styles.md](design-styles.md#pick)). Redesign: Aim, Keep, and Scope have owners ([briefing.md](briefing.md#redesign)); Scene was not asked; Use asked if still blank; Behave and Constraints not asked unless Aim named them. Polish: form skipped, or one Focus ask when the goal was mute ([briefing.md](briefing.md#polish)). Redesign, polish, and app UI: Catalog closed; app UI Look is `none` unless the user named an `id`. Inferred wordmark, audience, CTA, style-from-job, theme-from-job, palette-from-job, or occupancy-from-job fails — [briefing.md](briefing.md)
- [ ] `DESIGN.md` followed or created; CSS tokens match — [design-md.md](design-md.md)
- [ ] Files match [file-architecture.md](file-architecture.md) (default: `index.html` + `main.css` + `main.js`; no stylesheet dumped into HTML)
- [ ] Design Read declared (required for app UI and marketing)
- [ ] Lock line present: origin, name, scene (quoted Scene or composition sentence; owner exists), theme (`light` / `dark` / `system`), color strategy, layout/motion/density bands, stack. Marketing greenfield/redesign: Sketch; `folds=`; Packet `job=`, `P0=`, `tension=`, `object-swap=` (foreign P0 + because, or `n/a` per [composition.md](composition.md#frame)), `fallback=` (`yes` includes “fallback, not thesis”). CMS/admin/CRM/list/editor/accounts: `recipe=` and `Pareto=`. Other app UI: `Pareto=`; `recipe=none` valid on settings. Redesign: `aim=`, `keep=`, `scope=`
- [ ] *Crit* written; that file's done criterion holds for this task type and origin — [crit.md](crit.md)
- [ ] Register correct when not an isolated component (brand vs product)

### Viewport and type

- [ ] Viewport is `width=device-width, initial-scale=1` with no `maximum-scale=1` or `user-scalable=no`
- [ ] Body and form controls ≥16px on mobile (inputs included — iOS zoom)

### Document structure

- [ ] Skip link is the first focusable control and targets `#main`; `<main id="main">` exists (page/app shell; skip for an isolated component)
- [ ] One `h1` per view; heading levels sequential (no `h1` → `h3` skip)

### Anti-slop

- [ ] Does not read as generic AI output — slop test for this task type ([anti-slop.md](anti-slop.md#the-slop-test))
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
- [ ] Visible control text is in the accessible name (`aria-label` contains it, or there is no `aria-label`) — [production-engineering.md](production-engineering.md#labels)
- [ ] Sticky/fixed chrome and overlays do not cover the focused control (`scroll-padding` matches chrome height)
- [ ] Primary actions work on click/tap — hover is enhancement, not the only path
- [ ] `prefers-reduced-motion` respected when motion is used

### Responsive

- [ ] Works at 320px, 768px, and 1024px without horizontal scroll
- [ ] At 768 and 1024, a multi-column grid has N items in N cells (odd last item spans remaining columns; an empty bordered shell fails) — [layout-patterns.md](layout-patterns.md#grids-and-lists)

### Forms (when the surface has a form)

- [ ] Field groups follow [production-engineering.md](production-engineering.md#forms) (visible label + control + error in one grid cell). One inline error on a paired row: the next row's labels share a y. Odd last field spans remaining columns.

### Honesty

- [ ] State what was NOT verified (build, axe, real devices, screen reader, screenshot/browser). An unverified visual tell is not a fail. Missing Sketch or missing `tracks=` on marketing greenfield/redesign is a fail, not unverified. Missing `main=` / `proof=` on app UI is a fail, not unverified.

---

## Tier B — Marketing surfaces only

Add when building landing pages, portfolios, or campaigns. Also read [layout-patterns.md](layout-patterns.md). Count in the markup.

### Layout (count)

- [ ] Hero: headline ≤2 lines desktop; subtext ≤20 words; stack ≤4 text elements; top padding ≤6rem; primary CTA visible without scroll
- [ ] Logo / "used by" wall lives **under** the hero, not inside it
- [ ] Eyebrows: count `uppercase` + wide tracking above section headlines; count ≤ `ceil(sectionCount / 3)`; hero counts as 1
- [ ] Greenfield/redesign: DESIGN.md **Layout** contains the *thesis*, occupancy, and the Sketch ([composition.md](composition.md#frame)). Implement returned `tracks=`; Q1 in [crit.md](crit.md) holds. Packet `object-swap=`: skip the still-reads fail when the line is `n/a`; otherwise a foreign P0 in measured enter still reading fails. Lock `scene=` has an owner. Packet `fallback=yes` is visible and includes “fallback, not thesis”. Packet `folds=` names leftover *objects*; those sections exist; each fold shows its *object*. A two-fold page is valid when P0 cut removed the third object. Polish: current family kept; no new folds; `Sketch=none`
- [ ] Each layout family appears at most once; no 3 consecutive image+text zigzags
- [ ] Mixed-span grids: ≥2 cells have real visual variation (image, tint, pattern)
- [ ] Stacked CTAs below `md` fill the content column (no unused track beside a short button)
- [ ] Intra-fold gaps follow Lock `density=` ([design-systems.md](design-systems.md#density-bands)); `6rem`–`10rem` is between sections only
- [ ] Horizontal marquee ≤1 per page
- [ ] Nav: one line at desktop `lg`; height ≤80px
- [ ] One filled primary per fold (same CTA may repeat later in AIDA; two competing filled buttons in one fold fail)

### Visual

- [ ] Marketing surface uses real imagery when the lead *object* is an asset (gen-tool first, then real/seed photo, then labeled `TODO` slots) — not div fake screenshots. Type as P0: zero images in the first viewport is valid; do not add a stock photo to pass this box. Abstract-only brief: zero images is valid.
- [ ] Alt text on content images
- [ ] Memorable detail named in the Lock exists in the DOM (the *break* mass when one exists — not a bezel on every card; two-mass page: enter/rest contrast). First viewport matches the Sketch masses and measured `tracks=` in DESIGN.md Layout

### Copy

- [ ] No duplicate CTA intent on the same page
- [ ] CTA labels fit one line at desktop
- [ ] Copy self-audit against [anti-slop.md](anti-slop.md#copy-tells): every visible string re-read; portable or LLM-pattern sentences rewritten; one copy register per page

---

## Tier C — App UI and dashboards only

Add when building dashboards, settings, admin, or dense tools. Count from the Packet and the DOM. Dashboard tells: [anti-slop.md](anti-slop.md#dashboard-tells).

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
- [ ] If the view is CMS/admin/CRM home, list, editor, or accounts: Lock `recipe=` matches that view. Home (`recipe=queue-home`): ≥1 table or work-queue list in `main` (not charts-only)
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
