# Layout patterns

Vocabulary and rules for marketing layouts. Implement what the Design Read supports.

## Hero paradigms

| Pattern | When |
| --- | --- |
| **Asymmetric split** | Strong asset + strong message; bold layout brief |
| **Editorial manifesto** | Message IS the design; minimal asset |
| **Cinematic center** | Wide container, centered type, full-bleed bg |
| **Kinetic type** | Typography as primary visual |
| **Scroll-pinned hero** | Content scrolls over fixed hero (high-motion brief) |
| **Magazine** | Columned editorial, pull-quote, text wrapping an image |
| **Container-free** | Full-bleed, no `max-width` cage; one idea per fold |

### Hero rules (marketing)

- Fits initial viewport: headline ≤2 lines desktop, subtext ≤20 words
- CTA visible without scroll
- Max 4 text elements: eyebrow OR strip, headline, subtext, CTAs
- Top padding cap: `6rem` (`96px`) max at desktop
- No trust logos, feature bullets, or taglines below CTAs inside hero
- H1 container wide enough (`max-width: 64rem` / `1024px`+) to prevent 4–6 line wraps
- Real visual required — text + gradient blob is placeholder, not hero

### Anti-center bias

When the Lock layout band is `offset` or `wild`, prefer split, magazine, container-free, or pinned structures. Centered hero is for `contained` manifesto/launch/editorial briefs.

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

## Bento grids

- Asymmetric CSS Grid with mixed `col-span` / `row-span`
- Apply `grid-flow-dense` to avoid empty cells
- **N items → N cells** — reshape grid, don't leave voids
- 3–5 intentional cells often beats 8 messy ones
- At least 2–3 cells need visual variation — not all white text cards

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

- Overlap: negative margins, layered z-index with purpose
- **Airy brand:** `6rem`–`10rem` padding **between** sections; hero top padding still ≤`6rem`
- One intentional grid break per section max — the memorable irregularity named in the Lock
- Density band `dense` uses the compact spacing scale in [design-systems.md](design-systems.md#density-bands)

## Background treatments

- Gradient meshes, noise (on `fixed` overlay with `pointer-events-none` only)
- Layered transparencies, grain, geometric patterns

## Responsive collapse

For every multi-column layout, declare `<768px` behavior in the same component. If the desktop layout uses overlap or rotation, **turn those off** below `768px` (touch targets). Bento `col-span` / `row-span` reset to one column.

Example:

```html
<div class="grid-responsive">
  <div class="grid-main">...</div>
  <div class="grid-sidebar">...</div>
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
    grid-template-columns: 7fr 5fr;
  }
}
```

## Page theme lock

One theme (light, dark, or `prefers-color-scheme`) for whole page. Mid-page flip to warm paper on dark site is broken unless brief requires a deliberate color-block story.

## Footer

- Company info, contact, legal links
- No version strings on marketing pages

## Pattern selection

Select patterns that serve the brief, content structure, motion level (static page → no scroll hijack), and register (product → skip Awwwards scroll stacks).

Variety across **sections** matters more than novelty within one hero.
