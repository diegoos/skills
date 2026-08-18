# Typography

Load when type pairing is still blank after the style file and DESIGN.md ([load-map.md](load-map.md)). Unanswered blanks: [briefing.md](briefing.md).

Type controls what users read first, how long they stay, and whether they trust the product.

## Core rule

If users cannot read it comfortably, the design fails.

## Font count

| Register | Typical approach                       |
| -------- | -------------------------------------- |
| Brand    | Display + body (2 families max)        |
| Product  | One well-tuned family often sufficient |

More than three families reads as indecision. One family with strong weight/size contrast can beat a timid pair.

## Font pairing (structure, not a fashion list)

Register first: product = one family (or the project/system stack). Brand = display + body, two families max.

Pick the **construction contrast**, then a face that is not a reflex default:

- Serif display + sans body — editorial, publication, genuine luxury
- Geometric sans display + humanist sans body — modern brand without a serif tell
- One family, strong weight/size contrast — product and most SaaS landings
- Mono as accent only — code, tabular numbers, never marketing body
- Condensed display — headlines ≥32px only, never labels or forms
- Script — one hero word max, never prices, legal, or UI

**When / not_for by role:** all-caps ≤4 words; display never on buttons, table data, or form labels.

Run the reflex-reject list in [anti-slop.md](anti-slop.md) **before** locking the pair. Outfit and Plus Jakarta Sans are overused as unexamined defaults — allowed when this procedure picked them on purpose, not as the first grab. Do not treat Geist, Clash Display, or PP Editorial New as a "premium available" stack; they are the next Inter.

Prove the pair: x-height at 16px body; H1 overflow at every breakpoint; locale coverage (script/CJK/RTL) if the brief needs it.

## Typography system (define upfront)

Lock styles at project start and reuse everywhere:

| Role                | Purpose                   |
| ------------------- | ------------------------- |
| Display / H1        | Page title — one per page |
| H2 / H3             | Section structure         |
| Body                | Default reading text      |
| Secondary / caption | Metadata, hints           |
| Button / label      | Interactive text          |

Each role specifies: family, size, weight, line-height, letter-spacing, color token.

Do not invent per-section. Developers and designers must share one scale.

## Hierarchy

Guide the eye with **size + weight + color**, not bold everywhere:

- Heading: larger, bolder
- Body: regular weight, comfortable size
- Secondary: smaller, lower contrast (still ≥4.5:1 on bg)

Scale ratio ≥1.25 between steps. Flat scales (1.1× apart) read as uncommitted.

**Never bold every line** — hierarchy collapses when everything shouts.

## Line length and spacing

- Body prose: **45–75ch** max width
- Body line-height: **1.4–1.6** (140–160% of font size)
- Display headings: tighter tracking floor ≥ -0.04em; add line-height when italic includes descenders (`y`, `g`, `j`, `p`, `q`)
- Light text on dark backgrounds: add 0.05–0.1 to line-height

Dense text feels unprofessional and tires readers. Generous line-height is cheap usability.

## Color and contrast

- Primary text: not pure black on white — use off-black ink tokens
- Secondary text: muted but still WCAG AA against its background
- Never rely on color alone for meaning — pair with weight, icon, or label
- Gray text on colored backgrounds fails — darken to bg hue or use transparency

## Button and UI label typography

- Short, clear, sufficient weight (not hairline on buttons)
- Verb + object ("Save changes", not "OK")
- Large enough for touch (body and form controls ≥16px on mobile)
- `font-variant-numeric: tabular-nums` on prices, data columns, and timers
- URLs, IDs, and user tokens wrap with `overflow-wrap: anywhere` — never `word-break: break-all` on prose
- Prefer wrapping over truncation; if truncating, ellipsis plus a keyboard-reachable full string (tooltip or expand)
- No all-caps body copy — reserve uppercase for short labels ≤4 words

## Heading techniques

- `text-wrap: balance` on h1–h3 for even line lengths
- `text-wrap: pretty` on long prose to reduce orphans
- Hero/display ceiling: `clamp()` max ≤6rem unless poster brief
- Test headline copy at every breakpoint — overflow is a layout bug

## Scanning patterns

Users scan before they read. Match layout to content type:

| Pattern | Best for |
| --- | --- |
| **F-pattern** | Text-heavy pages (articles, docs, blogs) — key info left-aligned, bold headings, bullets |
| **Z-pattern** | Sparse marketing pages — logo top-left, CTA top-right, diagonal to bottom CTA |

For F-pattern: align important content left; use short bold headings; break long paragraphs with lists.

For Z-pattern: place primary CTA along the Z path; don't bury action center-only on wide hero without visual guide.

## Whitespace as typography partner

Whitespace is not empty space — it groups related content and separates sections. Without breathing room, hierarchy fails even with correct font sizes.

## When typography conflicts with brand expression

Brand can use distinctive display faces. Product prioritizes legibility at small sizes and dense layouts. Never sacrifice contrast or size for style on functional UI (forms, tables, nav labels).
