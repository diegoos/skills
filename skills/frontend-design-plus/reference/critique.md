# Critique

Open once after markup.

| Origin / Mode                                             | In scope                                                                                                |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| greenfield                                                | Slop + Copy + matching Mode headings                                                                    |
| redesign                                                  | Slop except triad; Copy; matching Mode headings                                                         |
| polish                                                    | Slop except triad and logo-swap; Copy only on strings this pass changes; matching Mode headings         |
| Isolated component                                        | Slop table, Enter, Deletion. Copy if the control has a visible label. Fit if the control sits in chrome |
| `Persuade` with no nav/header rail                        | skip Surfaces                                                                                           |
| `Operate`, or any chrome this pass touches                | Operate UX + Surfaces                                                                                   |
| `Persuade`/`Experience` conversion chrome (form, pricing) | Operate UX                                                                                              |

Done when every Fail-if in scope is gone, or each remaining match has a written reason. Fix this turn.

## Slop

Cite `rule=` when a tell matches. Keep a listed pattern only when the brief names it, disk already ships it, or the sequence is real.

At most **one** fold of N equal blocks. How-it-works is the object's UI, not `01`–`04` plus a second pain grid.

| id                      | Fail-if                                                                                                                                                           |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `model-default-triad`   | Greenfield: cream/sand/beige + display serif + any accent; near-black + acid/vermilion/orange; broadsheet (hairline, radius 0, dense columns)                     |
| `side-stripe`           | `border-left` (or inline start) >1px accent on a card, alert, **or blockquote**                                                                                   |
| `gradient-text`         | `background-clip: text` on a headline or CTA                                                                                                                      |
| `glass-default`         | Backdrop blur the scene did not name                                                                                                                              |
| `hero-metric`           | Big number + small label + stats row as first-viewport proof                                                                                                      |
| `identical-cards`       | Icon + heading + blurb × N unless the object is a real catalog. A second equal-block fold fails                                                                   |
| `eyebrow-every`         | Uppercase eyebrow count > `ceil(sections / 3)`                                                                                                                    |
| `numbered-markers`      | `01`–`05` as section or “practice area” markers with no real sequence                                                                                             |
| `three-feature-cards`   | Three equal feature cards as a fold                                                                                                                               |
| `generic-cta`           | Learn more / Saiba mais / Get started / Book now / Compre aqui and that string is not the Job                                                                     |
| `mesh-hero`             | Centered hero + dark mesh                                                                                                                                         |
| `nested-cards`          | Card inside a card on Operate                                                                                                                                     |
| `overused-font-inter`   | Inter / Geist / Outfit as unexamined brand default                                                                                                                |
| `costume-vest`          | First viewport is navy+justice, indigo+three cards, or mesh-HUD                                                                                                   |
| `placeholder-mass`      | Rectangle, letter-in-box, or `Texto` where the object's mass belongs                                                                                              |
| `off-domain-logos`      | “Used by” / source ticker uses brands the brief did not name and that are not the Job's objects (fintech logos on a clipping product; Notion/Figma on a news Job) |
| `chrome-overlap`        | A control intersects another control, the wordmark, or the padding edge (circular “Criar meu primeiro tópico” over the nav)                                       |
| `wrapped-cta`           | Primary label wraps to 2+ lines, or the button collapses to a circle or square because width ran out                                                              |
| `header-second-primary` | Header and hero both show a filled primary in the same 375 viewport                                                                                               |

If someone could identify the output as generated without hesitation, it failed.

**Enter.** First viewport includes a live fragment of the object (the brief, the queue, the kiln), not H1 plus CTA alone. A noun only in the H1 fails. At 375 that fragment sits below the header with no overlap.

**Deletion.** Name one accessory the brief did not ask for and that is not Signature. Fail if it remains. Extra chrome (parallax, custom cursor, uniform fade-in) fails unless named.

**CTA.** Visible primary is the Job verb+object.

**Persuade.** Logo-swap breaks the read. Navy-for-law, indigo-for-SaaS, cream-serif as warmth fail. The hop "not purple, so editorial serif with a stripe" fails unless Signature is mass.

**Operate.** Four equal KPIs + donut + "Welcome back" fails. `h1` in `main` is the queue or the view. Domain nouns live in rows and empty copy.

**Visual leftover.** Neon glow, pure `#000`/`#fff`, cream body as warmth, 6-line H1, empty grid cells, zigzag ×3, scroll-cue icons, overlap pills, fake title-block portfolio.

## Copy

UI strings. Active voice. Name the control. One specific claim from the object. Sentence case. Keep a listed pattern only when the brief names it, disk already ships it, or the string is legal/FAQ. One short fragment for emphasis is not a fail. Error and empty: what happened + the next step.

| id                  | Fail-if                                                                                                                                            |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sales-inflate`     | vibrant / seamless / elevate / unleash / groundbreaking, or a portable slogan (“radar de inteligência”, “sem o ruído”) that the brief did not name |
| `not-x-but-y`       | “Não é feed, é…” / “It's not X, it's Y” in the H1 or lead                                                                                          |
| `forced-triad-copy` | Three parallel phrases or three benefits that exist only to close the rhythm                                                                       |
| `vague-proof`       | “2.400+ profissionais”, “4.9/5”, “usado por Stone” (or unsourced `92%`) when the brief and disk do not give the number or the brand                |
| `title-case-ui`     | Title Case in headlines or nav labels                                                                                                              |
| `em-dash-ui`        | Em dash or en dash in labels or the H1                                                                                                             |
| `chatbot-leftover`  | “I hope this helps”, `Lorem ipsum`, John Doe                                                                                                       |
| `heading-echo`      | First sentence under an H2 only restates the heading                                                                                               |
| `optimistic-close`  | Closing band is a slogan with no Job verb                                                                                                          |

## Operate UX

Product chrome stays predictable. Same control, same result. One vocabulary. Platform back and search stay where people expect them. Mixing tab + sidebar + bottom nav at the same hierarchy fails.

Proximity groups; one accent; not everything bold. Every action gets hover/active; async gets loading; errors say what happened and how to recover. Exit on every overlay. Undo on destructive when feasible.

One filled primary per view. Nav answers where I am. Back restores scroll and filters. Visible label on every field. Catalog >12 items: filter first.

Task completion, then a11y, then brand.

## Surfaces

Nav, header, toolbar, rails. Done at 375, 1024, and 1440, or failed and fixed.

Controls sit inside the chrome padding box. Inset, `min-width: 0` on the flex child, truncate with a keyboard-reachable full string. Rail padding ≥ control padding. One filled primary per view. At 375 the header is wordmark plus a text control or menu; the filled primary lives in the hero (`chrome-overlap`, `wrapped-cta`, `header-second-primary`).

Nested chrome: `outerRadius = innerRadius + padding` (choose independently if padding >24px). Nested cards fail. Icon+label: icon-side padding = text-side minus `2px`, still inside the box.

Same-plane chrome: hairline. Overlay: elevation, one light source. Product-plane chrome uses fill plus hairline.

Hit ≥44px **inside** the parent; ≥8px gap. Live numbers: `tabular-nums`. Smoothing once on `html`. `text-wrap: balance` on view `h1`–`h3` only. Chrome icons: one family, `currentColor`, outline at rest / fill active. Name the properties that change; skip `transition: all`. Press `scale(0.96)`, interruptible.
