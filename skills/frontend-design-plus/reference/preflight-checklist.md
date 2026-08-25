# Pre-Flight Checklist

Run from the QA slot ([dispatch.md](dispatch.md#qa)) after *crit*. Isolated component: this window. Origin `polish` on marketing or app UI: this window after Implement ([polish.md](polish.md)); **Tier A only** — skip Tier B and C. Unanswered blanks: the Packet (or the slim packet on polish). Run the tier that matches [task routing](../SKILL.md#task-routing), except polish. QA records each box pass or fail and does not edit. The parent resumes Implement with failed boxes as P0. Skip tiers that do not apply. Score boxes from the Packet, DESIGN.md, and the DOM. Do not open other `reference/` files to complete a box.

Tier B and C are **mechanical**: count in the DOM. A failed count means the page is not done.

## Tier A — Always (every UI deliverable)

### Direction

- [ ] Task type identified (component / app UI / marketing)
- [ ] Origin named: `greenfield` (new UI), `redesign` (existing page from the briefing), or `polish` (improve existing UI). Existing surface: redesign keep/retire vs Aim; polish Audit P0/P1 closed ([polish.md](polish.md)); Lock `style=none`; Catalog closed
- [ ] Briefing card is complete (every applicable field has an owner) — skip on polish; slim packet instead
- [ ] `DESIGN.md` followed or created; CSS tokens match that file
- [ ] Files match the greenfield default when origin is greenfield: `index.html` + `main.css` + `main.js`; no stylesheet dumped into HTML
- [ ] Design Read declared (required for app UI and marketing) — skip on polish
- [ ] Packet Lock `layout=` does not pick `join=`
- [ ] *Crit* written; that file's done criterion holds for this task type and origin — skip this box on an isolated component or polish (no crit slot)
- [ ] Register correct when not an isolated component (brand vs product)

### Viewport and type

- [ ] Viewport is `width=device-width, initial-scale=1` with no `maximum-scale=1` or `user-scalable=no`
- [ ] Body and form controls ≥16px on mobile (inputs included — iOS zoom)

### Document structure

- [ ] Skip link is the first focusable control and targets `#main`; `<main id="main">` exists (page/app shell; skip for an isolated component)
- [ ] One `h1` per view; heading levels sequential (no `h1` → `h3` skip)

### Anti-slop

- [ ] Does not read as generic AI output — slop test for this task type ([anti-slop.md](anti-slop.md#the-slop-test))
- [ ] Visible punctuation and typography fit the copy register; LLM residue is rewritten, while justified punctuation is allowed ([anti-slop.md](anti-slop.md#copy-tells))

### Color

- [ ] One color strategy chosen; single accent locked page-wide (not a new accent per section)
- [ ] Lock `theme=light` or `theme=dark`: that one palette on `html`; theme-control count = 0
- [ ] Lock `theme=system`: light tokens and dark tokens both in CSS; labeled theme control count ≥ 1 in chrome; activating it sets `data-theme` or a class on `html` and surface tokens change. Media-query-only (control count = 0) fails. Dark-only or light-only CSS fails
- [ ] Dark `--surface` / `--surface-raised` are near-neutral charcoal unless Palette named a tinted field or Lock `color=drenched`

### Typography and contrast

- [ ] Clear hierarchy (not everything bold)
- [ ] Body contrast ≥4.5:1; buttons readable on their background
- [ ] Meaningful icons/controls ≥3:1 against adjacent color
- [ ] Headings do not overflow at mobile/tablet breakpoints
- [ ] Chip, badge, and compact labels reflow at 320 without clipping; overflow uses `+n` or an accessible full-value path
- [ ] Emoji-as-icon count in nav, settings, and controls = 0
- [ ] Interactive controls that a reset left as `cursor: default` use `cursor: pointer`

### Tap quality

- [ ] Touch targets ≥44px **and** ≥8px gap between adjacent targets
- [ ] Press feedback via color, opacity, or elevation — padding/border/width do not change
- [ ] Icon-only controls have an accessible name; decorative icons beside visible text are `aria-hidden`

### Interaction and a11y

- [ ] Default, hover, focus, active on interactive elements
- [ ] Loading, error, empty states where the flow needs them
- [ ] Async submit: control disabled (or second click ignored) with a loading label
- [ ] Keyboard navigable; semantic HTML; visible focus
- [ ] Visible control text is in the accessible name (`aria-label` contains it, or there is no `aria-label`)
- [ ] Sticky/fixed chrome and overlays do not cover the focused control (`scroll-padding` matches chrome height)
- [ ] Primary actions work on click/tap — hover is enhancement, not the only path
- [ ] `prefers-reduced-motion` respected when motion is used

### Harden (when attached)

Skip unless Packet `focus=a11y`, Constraints named i18n/RTL, or the user named edge cases / production-ready. Do not open other `reference/` files for these boxes.

- [ ] Long strings, dense lists, and large numbers do not clip chrome
- [ ] `lang` (and `dir` when RTL) present when Constraints named i18n
- [ ] Validation, network, and permission errors are distinct messages

### Responsive

- [ ] Works at 320px, 768px, and 1024px without horizontal scroll
- [ ] At 768 and 1024, a multi-column grid has N items in N cells (odd last item spans remaining columns; an empty bordered shell fails)

### Forms (when the surface has a form)

- [ ] Field groups: visible label + control + error in one grid cell. One inline error on a paired row: the next row's labels share a y. Odd last field spans remaining columns.
- [ ] Real `autocomplete` tokens (`name`, `email`, `username`, `current-password`, address). Auth fields allow paste; no `autocomplete="off"` on username/password
- [ ] No extra step that asks the user to retype a value already on the form. App UI: the P0 action is reachable without a greeting hop in `main`

### Honesty

- [ ] The [verification.md](verification.md) block exists with an evidence level, viewport results, automated accessibility status, performance level, and `not-verified=`. An unverified visual tell is not a pass. Missing Sketch, `tracks=`, or `scale=` on marketing greenfield/redesign is a fail, not unverified. Polish: Sketch absence is expected. Unused screenshot/browser this run on occupancy visual claims is P0. Missing `main=` / `proof=` on app UI is a fail, not unverified.
- [ ] The [visual-rubric.md](visual-rubric.md) block exists, every applicable criterion has evidence, and any threshold failure is in the P0/P1 table.

---

## Tier B — Marketing surfaces only

Skip on origin `polish` ([polish.md](polish.md)). Add when building landing pages, portfolios, or campaigns. Count in the markup.

### Layout (count)

- [ ] First viewport: headline ≤2 lines desktop, primary CTA visible without scroll, top padding ≤`6rem`, Packet `scan=` / `form=` hold
- [ ] Logo / "used by" wall lives **under** the first viewport, not inside it
- [ ] Eyebrows: count `uppercase` + wide tracking above section headlines; count ≤ `ceil(sectionCount / 3)`; first viewport counts as 1
- [ ] Greenfield/redesign: Q1 in [crit.md](crit.md) holds. Packet `folds=` sections exist in named `:<form>`. A two-fold page is valid. Polish: current family kept; no new folds
- [ ] Each layout family appears at most once; no extra fold to vary the page; no 3 consecutive image+text zigzags
- [ ] Mixed-span grids: ≥2 cells have real visual variation (image, tint, pattern)
- [ ] Stacked CTAs below `md` fill the content column (no unused track beside a short button)
- [ ] Intra-fold gaps follow Lock `density=`; `6rem`–`10rem` is between sections only
- [ ] Horizontal marquee ≤1 per page, and only when Lock `motion=cinematic` and Behave named cinematic
- [ ] Nav: one line at desktop `lg`; height ≤80px
- [ ] One filled primary per fold (same Success verb may repeat later; two competing filled buttons in one fold fail)

### Visual

- [ ] Marketing surface uses real imagery when the lead *object* is an asset (gen-tool first, then real/seed photo, then labeled `TODO` slots) — not div fake screenshots. Type as P0: zero images in the first viewport is valid; do not add a stock photo to pass this box. Abstract-only brief: zero images is valid.
- [ ] Alt text on content images
- [ ] Memorable detail named in the Lock exists in the DOM (the *break* mass when one exists — not a bezel on every card; two-mass page: enter/rest contrast). First viewport matches the Sketch masses and measured `tracks=` in DESIGN.md Layout

### Copy

- [ ] No duplicate CTA intent on the same page
- [ ] CTA labels fit one line at desktop
- [ ] Copy self-audit against [anti-slop.md](anti-slop.md#copy-tells): every visible string re-read; *divide* holds; portable or LLM-pattern sentences rewritten; one copy register per page

---

## Tier C — App UI and dashboards only

Skip on origin `polish` ([polish.md](polish.md)). Add when building dashboards, settings, admin, or dense tools. Count from the Packet and the DOM. Dashboard tells: [anti-slop.md](anti-slop.md#dashboard-tells).

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
- [ ] Auth fields (if present): paste allowed; `autocomplete` for username/password; no `autocomplete="off"` on those fields. 2FA/passkey copy names the next step (enter code, use device) without a new pitch

### Dashboard (if applicable)

- [ ] Lock `style=none` unless Look is a named catalog `id` or the user explicitly requested `style=custom`. Zero Catalog table in this run's chat
- [ ] `h1` in `main` is not a greeting ("Welcome back", "Good morning"). Greeting nodes in `main` = 0
- [ ] If KPI cards exist: they are not 4 equal siblings. Each KPI node has four text roles: label, value, delta, time
- [ ] If a pie/donut exists: slice count ≤ 3. Each chart has an adjacent title that is a question or a decision, not a noun ("Traffic", "Devices")
- [ ] If the view is CMS/admin/CRM home, list, editor, or accounts: Lock `recipe=` matches that view. Home (`recipe=queue-home`): ≥1 table or work-queue list in `main` (not charts-only)
- [ ] List view with ≥8 rows: ≥1 visible filter control (not only a "Filters" overflow)
- [ ] Each widget and the main list: empty, loading/skeleton, and error exist in markup
- [ ] One primary nav pattern. Destinations include the Job objects (list, create/edit, users), not Analytics-only
- [ ] Avatar control count in chrome ≤ 1. Filled primary count per view = 1
- [ ] Chrome containment: every nav and toolbar control sits inside the rail padding box at 1024 and 1440
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
