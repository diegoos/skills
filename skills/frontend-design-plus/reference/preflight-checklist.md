# Pre-Flight Checklist

Run the tier that matches [task routing](../SKILL.md#task-routing). Fix failures before shipping. Skip tiers that do not apply.

Tier B and C are **mechanical**: count in the DOM. A failed count means the page is not done.

## Tier A — Always (every UI deliverable)

**Direction**

- [ ] Task type identified (component / app UI / marketing)
- [ ] Origin named: `greenfield` (new UI) or `redesign` (existing page). Redesign: [redesign.md](redesign.md) read; audit listed; `mode=preserve|overhaul` in the Lock
- [ ] Design Read declared (required for app UI and marketing)
- [ ] Lock line present: origin, scene, color strategy, layout/motion/density bands, stack
- [ ] Register correct when not an isolated component (brand vs product)

**Viewport and type**

- [ ] Viewport is `width=device-width, initial-scale=1` with no `maximum-scale=1` or `user-scalable=no`
- [ ] Body and form controls ≥16px on mobile (inputs included — iOS zoom)

**Document structure**

- [ ] Skip link is the first focusable control and targets `#main`; `<main id="main">` exists (page/app shell; skip for an isolated component)
- [ ] One `h1` per view; heading levels sequential (no `h1` → `h3` skip)

**Anti-slop**

- [ ] Does not read as generic AI output (purple gradient hero, 3 equal cards, etc.)
- [ ] No em dashes (`—`) in visible copy

**Color**

- [ ] One color strategy chosen; single accent locked page-wide (not a new accent per section)
- [ ] Theme (light/dark) matches the scene, not a reflex default

**Typography and contrast**

- [ ] Clear hierarchy (not everything bold)
- [ ] Body contrast ≥4.5:1; buttons readable on their background
- [ ] Meaningful icons/controls ≥3:1 against adjacent color
- [ ] Headings do not overflow at mobile/tablet breakpoints

**Tap quality**

- [ ] Touch targets ≥44px **and** ≥8px gap between adjacent targets
- [ ] Press feedback via color, opacity, or elevation — padding/border/width do not change
- [ ] Icon-only controls have an accessible name; decorative icons beside visible text are `aria-hidden`

**Interaction and a11y**

- [ ] Default, hover, focus, active on interactive elements
- [ ] Loading, error, empty states where the flow needs them
- [ ] Async submit: control disabled (or second click ignored) with a loading label
- [ ] Keyboard navigable; semantic HTML; visible focus
- [ ] Sticky/fixed chrome and overlays do not cover the focused control (`scroll-padding` matches chrome height)
- [ ] Primary actions work on click/tap — hover is enhancement, not the only path
- [ ] `prefers-reduced-motion` respected when motion is used

**Responsive**

- [ ] Works at 320px without horizontal scroll

**Honesty**

- [ ] State what was NOT verified (build, axe, real devices, screen reader)

---

## Tier B — Marketing surfaces only

Add when building landing pages, portfolios, or campaigns. Also read [layout-patterns.md](layout-patterns.md). Count in the markup.

**Layout (count)**

- [ ] Hero: headline ≤2 lines desktop; subtext ≤20 words; stack ≤4 text elements; top padding ≤6rem; primary CTA visible without scroll
- [ ] Logo / "used by" wall lives **under** the hero, not inside it
- [ ] Eyebrows: count `uppercase` + wide tracking above section headlines; count ≤ `ceil(sectionCount / 3)`; hero counts as 1
- [ ] Each layout family appears at most once; no 3 consecutive image+text zigzags
- [ ] Bento: N items → N cells; ≥2 cells have real visual variation (image, tint, pattern)
- [ ] Horizontal marquee ≤1 per page
- [ ] Nav: one line at desktop `lg`; height ≤80px
- [ ] One filled primary per fold (same CTA may repeat later in AIDA; two competing filled buttons in one fold fail)

**Visual**

- [ ] Marketing surface uses real imagery (gen-tool first, then real/seed photo, then labeled `TODO` slots) — not div fake screenshots; zero images is a fail unless the brief is abstract-only
- [ ] Alt text on content images
- [ ] Memorable detail named in the Lock exists in the DOM (one material or spatial break — not a bezel on every card)

**Copy**

- [ ] No duplicate CTA intent on the same page
- [ ] CTA labels fit one line at desktop
- [ ] Copy self-audit against [anti-slop.md](anti-slop.md#copy-tells): every visible string re-read; portable or LLM-pattern sentences rewritten; one copy register per page

---

## Tier C — App UI and dashboards only

Add when building dashboards, settings, admin, or dense tools. Also read [product-register.md](product-register.md).

**Product UI**

- [ ] Follows project design system; consistent component vocabulary
- [ ] Display fonts not used on labels, buttons, or table data
- [ ] Modals not used when inline or progressive patterns suffice
- [ ] One filled primary action per view; secondary/tertiary visually quieter; destructive separated from the primary and from main nav
- [ ] Input control matches the choice: radio (2–5 exclusive, all visible), checkbox (independent), select (long list), toggle (persistent binary)
- [ ] Nav marks the current location; back restores scroll and filters
- [ ] Lists/tables with ≥50 visible rows paginate or virtualize
- [ ] Craft extra (material enclosure, cinematic motion, macro whitespace) only on the 1–2 Pareto screens named in the Lock

**Forms (when the view has a form)**

- [ ] Each field: visible label, semantic `type`/`inputmode`, real `autocomplete`, required indicator, helper/error via `aria-describedby`
- [ ] Validate on blur and submit (errors stay off during typing)
- [ ] Failed submit: focusable error summary plus inline errors
- [ ] Auth fields (if present): paste allowed; `autocomplete` for username/password; no `autocomplete="off"` on those fields

**Dashboard (if applicable)**

- [ ] Audience and dashboard type clear (overview vs operational vs analytical)
- [ ] KPIs prioritized; color encodes meaning, not decoration
- [ ] Widget loading/error/empty states present
- [ ] Charts match the question; dual encoding (not hue alone); table or text fallback

**Performance (page-level app shells)**

- [ ] Heavy UI isolated to separate routes/server requests; images sized and lazy-loaded below fold

**Conditional**

- [ ] Drag/sort (if present): keyboard and simple-pointer alternative
- [ ] PWA / `viewport-fit=cover` (if present): `env(safe-area-inset-*)` on fixed chrome

---

Short approval is valid for small components when Tier A passes and scope is narrow.
