# Layout patterns

Load when [load-map.md](load-map.md) attaches this file to the current slot. Unanswered blanks belong to the Packet.

Vocabulary and rules for marketing layouts. Implement what the Design Read supports.

## Frame tracks

If the Packet has a Sketch, map `enter` / `rest` / `break` (or two masses when `break=none`) to CSS tracks. Do not pick a named hero family. Track sizes come from Sketch `tracks=`, not `1fr 1fr`.

| Join | DOM |
| --- | --- |
| **stack** | One column. Enter above rest. Medium gap. |
| **split** | Two tracks from Sketch `enter` / `rest` as `fr` (example: `8fr 4fr`). Larger track is the enter *object*. |
| **full-bleed** | Enter fills the viewport. No `max-width` cage on that mass. |
| **overlap** | The same *object* is the field; the Success label sits on that mass (`rest=inset`). |

### First viewport (marketing)

- Fits initial viewport: headline ≤2 lines desktop, subtext ≤20 words
- CTA visible without scroll
- Max 4 text elements: eyebrow OR strip, headline, subtext, CTAs
- Stacked CTAs below `md` fill the content column. A short button with an unused track to its right fails
- Top padding cap: `6rem` (`96px`) max at desktop
- No trust logos, feature bullets, or taglines below CTAs inside hero
- H1 container wide enough (`max-width: 64rem` / `1024px`+) to prevent 4–6 line wraps
- Type as the lead *object* (Packet P0 perception is the headline): the first viewport *is* that type. Text + gradient blob still fails. Do not add a stock photo to pass this rule.
- Asset as the lead *object*: a real visual occupies the enter track. Text + gradient blob is placeholder, not hero

### Anti-center bias

Frame occupancy wins. A centered mass is valid only when Frame already centered it and Lock `layout=contained`.

## First three folds

Greenfield and redesign **marketing** only. Load this section from **Implement** after `tracks=` exists. Packet `folds=` already names leftover *objects* in *job* order ([composition.md](composition.md#map)). Origin `polish` keeps the current family.

Give each leftover *object* the form the object itself asks for. Do not walk this table as a menu.

- schedule, slot, timeline, queue of times → a time-ordered list or calendar, not three equal cards
- proof, quote, metric → one sourced proof
- comparison, plan, spec → a table
- persist, book, buy, contact → one CTA band
- a catalog of independent items → at most one card-family section

Open the table below only when that leftover *object* has no obvious form (table, list, one proof, CTA) ([implement.md](implement.md#one-folds-list-or-one-recipe)). A shape that rewrites Frame occupancy fails. Spec, magazine, FAQ, and CTA band exist only as listed *objects*. A fold that is icon + title + blurb × N fails unless the Inventory object **is** a catalog of items.

| Fold shape | When the leftover *object* is |
| --- | --- |
| **Spec / comparison** | attributes or plans the user compares |
| **Magazine** | editorial body, pull-quote, or text wrapping an image |
| **Featured-vs-rest** | a few lead items plus a remainder |
| **One proof** | quote, metric with source, or product shot |
| **CTA band** | a later persist control that is still a listed *object* |
| **Short FAQ or steps** | a real sequence on the object list |

One card-family section per page still holds ([Cards](#cards)). Each family still appears at most once ([Section layout diversity](#section-layout-diversity)).

Done when each Packet fold exists in the DOM and shows its *object* (redesign: rebuilt from blocks the audit kept). A two-fold page is done when P0 cut removed the third object. A two-mass first viewport (`break=none`) is valid.

## Cards

A card is a **self-contained, clickable unit** (feed item, catalog preview, shareable tile).

- **When:** browsing many independent items; each card can stand alone
- **Not for:** KPI metrics, settings rows, body paragraphs, table rows, form groups
- At most **one** card-family section per marketing page
- Nested cards stay wrong on product UI ([product-register.md](product-register.md))

Magazine and container-free are the constructive exits from a card farm.

## Navigation

- Single line on desktop at `lg`; condense or hamburger if needed
- Height 64–72px typical; max 80px
- Sticky header is the marketing default. **Island / floating pill nav** only when motion is `cinematic` **and** the brief is a one-pager or portfolio
- Search top, footer with company/contact links (user expectations)

## Section layout diversity

- Each layout family appears **at most once** per page
- Page with 8 sections → aim for ≥4 distinct layout families
- Max 2 consecutive image+text zigzag sections (the 3rd consecutive zigzag fails)

| Family | When |
| --- | --- |
| **Magazine** | Columned editorial, pull-quote, text wrapping an image — constructive exit from a card farm |
| **Container-free** | Full-bleed, no `max-width` cage; one idea per fold |
| **Split / zigzag** | Image+text; at most two consecutive |
| **Bento** | Mixed spans; N items → N cells |
| **Spec / comparison** | Side-by-side plans or attributes, not three identical cards |

## Grids and lists

**N items → N cells.** Reshape the grid. A bordered empty shell is a void. An odd last item spans remaining columns (`grid-column: 1 / -1` or equivalent). Apply `grid-flow-dense` when spans mix. 3–5 intentional cells often beats 8 messy ones.

| List size | Prefer |
| --- | --- |
| ≤5 items | Simple list or compact grid |
| 6–10 items | 2-col groups, cards, tabs, accordion |
| Many items | Carousel, marquee (max 1/page), filters, separate page |
| Spec sheet / >5 divided rows | 2-col spec cards, grouped chunks, or featured-vs-rest — not `ul` + `divide-y` on every row |

## Scroll patterns (high-motion brief)

Use intersection observers with CSS class toggles for simple reveals; dedicated scroll-driven libraries for pin/scrub effects.

| Pattern               | Use                                         |
| --------------------- | ------------------------------------------- |
| Sticky scroll stack   | Cards pin and stack                         |
| Horizontal pan        | Vertical scroll drives horizontal gallery   |
| Scroll reveal stagger | Items fade/slide in on enter                |
| Kinetic marquee       | Partner logos, manifesto strip (max 1/page) |

Scroll-driven animation rules: use `start: "top top"` for pin triggers; cleanup listeners on unmount or page leave. Never attach `scroll` listeners that update state or styles on every frame — use compositor-only transforms or CSS scroll-timeline.

## Choice architecture

- Catalog or grid with **>12** items: filters or a featured subset **before** the full grid
- Pricing / plans: side-by-side comparison, not three identical feature cards
- Featured-vs-rest: 3–4 hero items, remainder behind a disclosure or a dedicated page

## Named patterns

| Pattern | When | Not for |
| --- | --- | --- |
| Island nav | Cinematic one-pager / portfolio | Product app shell; default marketing |
| Magnetic nested CTA | Primary brand CTA with Lock enclosure/nested | Product toolbars; every button |
| Sticky scroll stack | High-motion brand, few chapters | Product; more than one stack per page |
| Horizontal pan | Gallery whose sequence is the story | Product tables; a second pan on the same page |

No implementation sketches here. Pin/scrub failure modes: [motion.md](motion.md#scroll-driven-patterns).

## Spatial composition

The Frame masses (*enter* / *rest* / *break*, or two masses) are the first-viewport commit ([composition.md](composition.md#frame)).

- Overlap: negative margins, layered z-index with purpose — only as the *break* mass, and only when that *object* is the overlap
- **Airy brand:** `6rem`–`10rem` padding **between** sections; hero top padding still ≤`6rem`
- Intra-fold stack (headline → subtext → CTAs → media) uses the Lock density band in [design-systems.md](design-systems.md#density-bands), not the between-section scale
- One intentional grid break per section max — the *break* mass named in the Frame, when one exists
- Density band `dense` uses the compact spacing scale in [design-systems.md](design-systems.md#density-bands)
- Track sizes come from Sketch `tracks=`.

## Background treatments

Field from the scene sentence and the style Path (paper, ink, metal, void). A `fixed` overlay with `pointer-events-none` may hold grain or a geometric screen when that Path names it. Mesh or noise as atmosphere only when the *thesis* or the brief names a field.

## Responsive collapse

For every multi-column layout, declare `<768px` behavior in the same component. If the desktop layout uses overlap or rotation, **turn those off** below `768px` (touch targets). Mixed `col-span` / `row-span` reset to one column. Recheck occupancy at `768px` and `1024px` ([grids and lists](#grids-and-lists)). `auto-fit` / `minmax` that leaves a hole at tablet fails.

Example (replace the desktop tracks with Sketch `tracks=`, e.g. split `8fr 4fr`):

```html
<div class="grid-responsive">
  <div class="grid-main" data-mass="enter">...</div>
  <div class="grid-sidebar" data-mass="rest">...</div>
</div>
```

```css
.grid-responsive {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: 1fr;
}

@media (min-width: 768px) {
  .grid-responsive {
    grid-template-columns: 8fr 4fr;
  }
}
```

## Page theme lock

One visible mode (light or dark) for the whole page. Lock `theme=system` still one mode at a time; the chrome control changes the page ([color.md](color.md#system-theme)). Mid-page flip to a second mode is broken unless the brief names a color-block story.

## Footer

- Company info, contact, legal links
- No version strings on marketing pages

## Pattern selection

Select patterns that serve the brief, content structure, motion level (static page → no scroll hijack), and register (product → skip Awwwards scroll stacks).

Variety across **sections** matters more than novelty within one first viewport. The Sketch is the composition commit ([composition.md](composition.md#frame)). Packet `folds=` names leftover *objects*; Implement places those objects first and opens this file's fold table only as a lookup.
