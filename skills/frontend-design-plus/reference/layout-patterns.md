# Layout patterns

Load when [load-map.md](load-map.md) attaches this file to the current slot (marketing Implement). Unanswered blanks belong to the Packet. Occupancy numbers and `:<form>` already live in the Packet; this file maps them to CSS. Do not pick `join=` here.

Vocabulary and rules for marketing layouts. Implement what the Design Read supports. Work Frame tracks through viewport proof before using First three folds.

## Frame tracks

If the Packet has a Sketch, map `enter` / `rest` / `break` (or two masses when `break=none`) to CSS tracks. Do not pick a named hero family. Track sizes come from Sketch `tracks=` as `fr` or `%`, not `1fr 1fr` and not a first-viewport width in `px`. Tracks are fluid between the Sketch's named break.

| Join | DOM |
| --- | --- |
| **stack** | One column. Enter above rest. Medium gap. |
| **split** | Two tracks from Sketch `enter` / `rest` as `fr` (example: `8fr 4fr`). Larger track is the enter *object*. |
| **full-bleed** | Enter fills the viewport. No `max-width` cage on that mass. |
| **overlap** | The same *object* is the field; the Success label sits on that mass (`rest=inset`). |

### First viewport (marketing)

- Fits initial viewport: headline ≤2 lines desktop, subtext ≤20 words
- CTA visible without scroll; label is Packet Success (verb+object)
- Max 4 text elements: eyebrow OR strip, headline, subtext, CTAs
- Stacked CTAs below `md` fill the content column. A short button with an unused track to its right fails
- Top padding cap: `6rem` (`96px`) max at desktop
- No trust logos, feature bullets, or taglines below CTAs in the first viewport
- H1 container wide enough (`max-width: 64rem` / `1024px`+) to prevent 4–6 line wraps
- Type as the lead *object* (Packet P0 perception is the headline): the first viewport *is* that type. Text + gradient blob still fails. Do not add a stock photo to pass this rule.
- Asset as the lead *object*: a real visual occupies the enter track. Text + gradient blob is placeholder, not hero
- Packet `scan=` holds P0 and CTA on the path (pyramid = first look; Z = corners; F = left column)
- Packet `form=` is how enter renders. `catalog-cards` only when the enter object *is* a catalog
- Loud enter (`scale=`): computed `font-size` of the largest text in `[data-mass="enter"]` is ≥3× `body`, or enter span is ≥8/12, or `join=` is `overlap` / `full-bleed`. Stack with type as P0 takes the 3× branch (`scale=<enter px>/<body px>`). The mass branch returns `scale=mass`.

### Anti-center bias

Sketch occupancy wins. A centered mass is valid only when the Sketch already centered it and Lock `layout=contained`. `layout=` is a containment band; it does not pick `join=`.

## First three folds

Greenfield and redesign **marketing** only. Use this heading after Frame tracks and `tracks=` exist. Packet `folds=` already names leftover *objects* with `:<form>` in *job* order. Do not reopen [composition.md](composition.md). Origin `polish` keeps the current family.

Put each leftover *object* on screen in the Packet form. Confirm; do not pick a different family.

| Packet `form=` | DOM |
| --- | --- |
| `list` | time-ordered list, calendar, or queue |
| `table` | comparison or spec table |
| `magazine` | editorial body, pull-quote, text wrapping an image |
| `one-proof` | one sourced quote, metric, or product shot |
| `cta` | one persist band |
| `catalog-cards` | at most one card-family section |
| `split-tasks` | two sibling tasks; not a hero + rail |

A shape that rewrites Frame occupancy fails. Spec, magazine, FAQ, and CTA band exist only as listed *objects*. A fold that is icon + title + blurb × N fails unless the Inventory object **is** a catalog of items. A fold whose DOM form ≠ Packet `:<form>` fails.

One card-family section per page still holds ([Cards](#cards)). Each family appears at most once ([Section layout diversity](#section-layout-diversity)). Do not add a fold to chase variety.

Done when each Packet fold exists in the DOM in its named form (redesign: rebuilt from blocks the audit kept). A two-fold page is done when P0 cut removed the third object. A two-mass first viewport (`break=none`) is valid when enter contrast holds.

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
- Sticky header is the marketing default. **Island / floating pill nav** only when Lock `motion=cinematic` **and** Behave named cinematic (one-pager or portfolio)
- Search top, footer with company/contact links (user expectations)

## Section layout diversity

The page map is Packet `folds=` with `:<form>`. Each layout family appears **at most once**. Do not add a fold to vary the page. A two-fold page is complete. Max 2 consecutive image+text zigzag sections (the 3rd consecutive zigzag fails).

| Family | When a Packet fold uses it |
| --- | --- |
| **Magazine** | `:<form>` is `magazine` |
| **Container-free** | `join=full-bleed` or a fold that is the field |
| **Split / zigzag** | `join=split` or `split-tasks`; at most two consecutive |
| **Spec / comparison** | `:<form>` is `table` |
| **Catalog cards** | `:<form>` is `catalog-cards` — at most one |

Bento is not a default replacement for three feature cards. Mixed spans only when the Inventory object is a set of independent items with unequal weight.

## Grids and lists

**N items → N cells.** Reshape the grid. A bordered empty shell is a void. An odd last item spans remaining columns (`grid-column: 1 / -1` or equivalent). Apply `grid-flow-dense` when spans mix. 3–5 intentional cells often beats 8 messy ones.

| List size | Prefer |
| --- | --- |
| ≤5 items | Simple list or compact grid |
| 6–10 items | 2-col groups, cards, tabs, accordion |
| Many items | Carousel, marquee (max 1/page), filters, separate page |
| Spec sheet / >5 divided rows | 2-col spec cards, grouped chunks, or featured-vs-rest — not `ul` + `divide-y` on every row |

## Scroll patterns

Open only when Lock `motion=cinematic` **and** Behave named cinematic. Default marketing `motion=still` does not use this section.

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

Only when Lock `motion=cinematic` **and** Behave named cinematic. Default marketing does not open this shelf.

| Pattern | When | Not for |
| --- | --- | --- |
| Island nav | Cinematic one-pager / portfolio | Product app shell; default marketing |
| Magnetic nested CTA | Primary brand CTA with Lock enclosure/nested | Product toolbars; every button |
| Sticky scroll stack | High-motion brand, few chapters | Product; more than one stack per page |
| Horizontal pan | Gallery whose sequence is the story | Product tables; a second pan on the same page |

No implementation sketches here. Pin/scrub failure modes: [motion.md](motion.md#scroll-driven-patterns).

## Spatial composition

The Frame masses (*enter* / *rest* / *break*, or two masses) are the first-viewport commit (Packet Sketch). Do not reopen [composition.md](composition.md).

- Overlap: negative margins, layered z-index with purpose — only as the *break* mass, and only when that *object* is the overlap
- **Airy brand:** `6rem`–`10rem` padding **between** sections; first-viewport top padding still ≤`6rem`
- Intra-fold stack (headline → subtext → CTAs → media) uses the Lock density band in [design-systems.md](design-systems.md#density-bands), not the between-section scale
- One intentional grid break per section max — the *break* mass named in the Frame, when one exists
- Density band `dense` uses the compact spacing scale in [design-systems.md](design-systems.md#density-bands)
- Track sizes come from Sketch `tracks=`.

## Background treatments

Field from the scene sentence and the style Path (paper, ink, metal, void). A `fixed` overlay with `pointer-events-none` may hold grain or a geometric screen when that Path names it. Mesh or noise as atmosphere only when the *thesis* or the brief names a field.

## Responsive collapse

For every multi-column layout, declare `<768px` behavior in the same component. If the desktop layout uses overlap or rotation, **turn those off** below `768px` (touch targets). Mixed `col-span` / `row-span` reset to one column. Recheck occupancy at `768px` and `1024px` ([grids and lists](#grids-and-lists)). `auto-fit` / `minmax` that leaves a hole at tablet fails. First-viewport tracks stay fluid (`fr` / `%`); a `px` width on the first-viewport grid fails.

An *object* that appears in a narrow `rest` track and again in a wide fold adapts to its **parent**, not to the page viewport: wrap that object in a container and use `@container` for its micro-layout. Viewport `lg` must not turn a 4-column proof into a hero.

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

Ship Packet `folds=` in the named `:<form>`. Do not add a fold to complete a page template. Motion patterns in [Scroll patterns](#scroll-patterns) stay closed unless Lock `motion=cinematic` and Behave named cinematic. Product register skips those stacks.

The Sketch is the first-viewport commit (Packet Sketch). Implement places leftover *objects* in Packet form. Do not reopen [composition.md](composition.md).
