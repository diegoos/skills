# UX principles

Load when [load-map.md](load-map.md) attaches this file to the current slot. Unanswered blanks belong to the Packet.

Apply with the register (brand vs product) in SKILL.md.

## Consistency builds trust

Four kinds, all required on product chrome:

- **Visual** — tokens, type, space, radius
- **Functional** — the same control does the same thing
- **Internal** — one product, one vocabulary, including across breakpoints
- **External** — platform conventions (back, search placement, native selects)

Product **never** surprises in the chrome. Brand may break external consistency **once**; that break is the memorable detail named in the Lock. Mixing tab + sidebar + bottom nav at the same hierarchy is not a creative break.

## Visual hierarchy techniques

| Technique | Use |
| --- | --- |
| **Proximity** | Group related items; separate unrelated groups with space |
| **Repetition** | Repeat patterns (card rhythm, nav placement) for predictability |
| **Color / contrast** | One accent for primary CTA; don't decorate with rainbow palettes |
| **Size / weight** | Important content larger or bolder — not everything bold |
| **Whitespace** | Breathing room reduces cognitive load |

**Scanning patterns:** Packet `scan=` owns the first-viewport path. This file does not choose `join=`. Do not reopen [composition.md](composition.md).

## Feedback and micro-interactions

Every user action needs visible response:

- Hover/active states on interactive elements
- Loading indicators for async work (skeleton > spinner in content areas)
- Success/error confirmation (toast, inline message, checkmark)
- Form validation on **blur and submit** — not on every keystroke. Field contract is in [production-engineering.md](production-engineering.md#forms) when that file is attached.

Product UI: 150–250ms. Brand surfaces can be more expressive when the brief supports motion.

## User control

- Theme switch when Lock `theme=system`: [color.md](color.md#system-theme)
- Dismissible modals, popovers, banners — always provide exit
- Undo for destructive actions when feasible

Avoid trapping users in flows. No auto-play video with sound; defer non-critical overlays.

## Mobile-first and responsive

Design smallest screens first, then scale up. Test across device sizes before shipping. Responsive design is not optional decoration.

## Accessibility

Semantic HTML, keyboard navigation, visible focus, WCAG 2.2 AA contrast, and `prefers-reduced-motion` are ship gates. Implementation patterns: [production-engineering.md](production-engineering.md). Focused controls stay visible: sticky chrome and overlays do not cover them (WCAG 2.4.11; `scroll-padding` matches chrome height).

Z-index uses the named scale in [design-systems.md](design-systems.md#z-index-scale) (`dropdown` → `sticky` → `modal-backdrop` → `modal` → `toast` → `tooltip`). Arbitrary `z-9999` fails.

Auth: paste on password fields; 2FA and passkey copy names the next step only (enter the code, use the device). Do not invent a second hero pitch on those screens.

## Cognitive load and choice

- Simplify navigation paths
- Limit form fields to what's necessary
- Catalog or grid with **>12** items: filters or a featured subset **before** the full grid
- Pricing / plans: side-by-side comparison, not three identical cards
- Default to the most common user path
- Multi-step flows: real step count, Back and Cancel always, input preserved. A bar that advances by itself is not progress.

## Navigation

Clear navigation answers: where am I, what is available, how do I find it?

Use sticky headers for primary nav, logical menu hierarchy, breadcrumbs when depth warrants, and search that matches real query behavior. Mark the current location. Back restores scroll, filters, and input — never silently reset the stack. Key screens have a URL. Bottom nav (when used) ≤5 items, icon **and** label, top-level only. Adaptive: sidebar ≥1024px; bottom or top nav on small screens. Destructive actions sit apart from normal nav.

## Forms

Field contract, validation, error summary, and control choice live in [production-engineering.md](production-engineering.md#forms). UX constraints that stay here:

- Minimum fields; don't ask for unnecessary data
- Never placeholder-as-label; link text must stand alone ("View pricing", not "click here")
- Reuse information already supplied in the same process (do not ask for email twice)
- Wizard: real steps, Back, Cancel, preserved input — not a self-advancing bar

## CTAs and conversion

- **Product:** one filled primary per **view**; secondary and tertiary quieter; destructive separated
- **Marketing:** one filled primary per **fold**; the same Success verb may repeat later; two competing filled buttons in one fold fail. The repeat is not a new layout family.
- Verb + object labels; 3 words max on the primary when it would wrap
- Keep the CTA cluster tight; separate it from competing blocks. A short button with an unused column beside it fails
- Concrete verbs; avoid decorative punctuation that makes copy feel templated

## Microcopy and sample content

Copy is a design material and one of the loudest slop signals. The words ship with the UI — generic or placeholder text fails the anti-slop bar regardless of the visuals. This covers UI microcopy and example content only, not brand messaging or long-form copywriting.

**Realistic sample content** (the most common practical failure):

- Never ship `Lorem ipsum`, `John Doe`, `Acme`, `Nexus`, or unsourced stats (`92%`, `4.1×`). QA scores copy tells; do not open [anti-slop.md](anti-slop.md) from this file.
- Generate plausible names, companies, dates, and values that fit the domain and locale of the brief.
- Write text at **realistic length** — short labels stay short, descriptions run as long as real ones would. Test the layout at those lengths.

**Voice consistency** — copy register is this Job's nouns. Hold it across buttons, empty states, and errors. Errors stay dry (what happened + next step). Mixed register reads as assembled, not authored.

**State copy patterns:**

| State | Shape |
| --- | --- |
| Empty | Name what's missing + the one action that fixes it (teach, don't just say "No data") |
| Loading | Usually none — a skeleton communicates; add text only for long waits |
| Error | What happened + how to recover, no blame (see Error handling below) |
| Onboarding | One next step at a time; don't front-load every feature |

Button, CTA, label, and form-text rules live in **CTAs and conversion** and **Forms** above.

## Media (images, video)

Format, srcset, photography selection, SVG, and delivery: [assets.md](assets.md) when attached. Video: no autoplay with sound; poster image; respect reduced motion.

## Error handling

- Errors explain what happened and how to recover
- Avoid blame ("Invalid input" → "Enter an email like `name@example.com`")
- Preserve user input on failed submission
- Network errors: retry path when applicable

## Dashboards and data UI

Dashboards are **decision tools**, not chart galleries. CMS / admin / operator **home** is a work queue. Pick one named recipe per view (Packet `recipe=`). Scaffold tells wait for QA; do not open [anti-slop.md](anti-slop.md) from this file. Design remaining analytics views for the audience:

| Audience   | Needs                              |
| ---------- | ---------------------------------- |
| Executives | Overview KPIs, trends, exceptions  |
| Operators  | Real-time detail, filters, actions |
| Analysts   | Drill-down, export, comparison     |

**Rules:**

- Define dashboard type (overview, operational, analytical) — one primary type per view
- Prioritize KPIs; group related data; plain-language labels
- Color encodes meaning (status, alerts) — not rainbow decoration
- **Question → chart family:** trend over time → line/area; compare categories → bar (sorted); part-to-whole → waffle/stacked (pie/donut only ≤3 slices with a visible difference); correlation → scatter; KPI vs target → number + bullet, not a gauge gallery; no question → table. Chart library only if the repo already has one (Recharts, Chart.js, or the project kit).
- **Cardinality:** <4 points → stat card; >6 series → noise; >15 categories → table/search
- Dual encoding: never hue alone (pattern, direct label, dashed vs solid). Provide a table or a one-sentence insight as fallback
- `font-variant-numeric: tabular-nums` on prices, columns, timers
- Widget loading/error/empty states required
- Lazy-load heavy widgets; virtualize lists/tables with **≥50** visible rows; collapse to single column on mobile

**Anti-patterns:** identical metric card grids with no hierarchy; decorative charts; too many real-time streams competing for attention. Home-as-analytics on a CMS IA fails the same scaffold test (QA).

Use established systems for enterprise patterns (Fluent, Carbon, Polaris). TanStack Table / AG Grid for large data.

## Testing

- Usability on real tasks (not "does it look good?")
- Multiple breakpoints; keyboard and screen reader spot checks
- Watch what users **do**, not only what they say

## When UX conflicts with aesthetics

Resolve in this order:

1. **Task completion** — user must be able to finish the job
2. **Accessibility** — non-negotiable floor
3. **Performance** — slow is unusable; see [performance.md](performance.md)
4. **Brand expression** — bold aesthetics within the above constraints

A beautiful page that hides the CTA or breaks keyboard nav is a failed design. Accessibility is solved on the enter object: contrast on the real pair, accessible name matches the visible label, alt on the photo, `prefers-reduced-motion` as the motion branch. A gray card that replaces the enter mass fails occupancy.
