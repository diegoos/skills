# Critique

Open once after markup.

| Origin / Mode | In scope |
| --- | --- |
| greenfield | Slop + matching Mode headings |
| redesign | Slop except triad; matching Mode headings |
| polish | Slop except triad and logo-swap; matching Mode headings |
| Isolated component | Slop table, Enter, Deletion |
| `Persuade` with no nav/header rail | skip Surfaces |
| `Operate`, or any chrome this pass touches | Operate UX + Surfaces |
| `Persuade`/`Experience` conversion chrome (form, pricing) | Operate UX |

Done when every Fail-if in scope is gone, or each remaining match has a written reason. Fix this turn.

## Slop

Cite `rule=` when a tell matches. Keep a listed pattern only when the brief names it, disk already ships it, or the sequence is real.

| id | Fail-if |
| --- | --- |
| `model-default-triad` | Greenfield: cream/sand/beige + display serif + any accent; near-black + acid/vermilion/orange; broadsheet (hairline, radius 0, dense columns) |
| `side-stripe` | `border-left` (or inline start) >1px accent on a card, alert, **or blockquote** |
| `gradient-text` | `background-clip: text` on a headline or CTA |
| `glass-default` | Backdrop blur the scene did not name |
| `hero-metric` | Big number + small label + stats row as first-viewport proof |
| `identical-cards` | Icon + heading + blurb × N unless the object is a real catalog |
| `eyebrow-every` | Uppercase eyebrow count > `ceil(sections / 3)` |
| `numbered-markers` | `01`–`05` as section or “practice area” markers with no real sequence |
| `three-feature-cards` | Three equal feature cards as a fold |
| `generic-cta` | Learn more / Saiba mais / Get started / Book now / Compre aqui and that string is not the Job |
| `mesh-hero` | Centered hero + dark mesh |
| `nested-cards` | Card inside a card on Operate |
| `overused-font-inter` | Inter / Geist / Outfit as unexamined brand default |
| `costume-vest` | First viewport is navy+justice, indigo+three cards, or mesh-HUD |
| `placeholder-mass` | Rectangle, letter-in-box, or `Texto` where the object's mass belongs |

If someone could identify the output as generated without hesitation, it failed.

**Enter.** First viewport is the object's mass. A noun only in the H1 fails.

**Deletion.** Name one accessory the brief did not ask for and that is not Signature. Fail if it remains. Extra chrome (parallax, custom cursor, uniform fade-in) fails unless named.

**CTA.** Visible primary is the Job verb+object.

**Persuade.** Logo-swap breaks the read. Navy-for-law, indigo-for-SaaS, cream-serif as warmth fail. The hop "not purple, so editorial serif with a stripe" fails unless Signature is mass.

**Operate.** Four equal KPIs + donut + "Welcome back" fails. `h1` in `main` is the queue or the view. Domain nouns live in rows and empty copy.

**Rewrite:** gradient text, glass default, neon glow, pure `#000`/`#fff`, cream body as warmth, 6-line H1, empty grid cells, zigzag ×3, scroll-cue icons, overlap pills, fake title-block portfolio, portable slogan, Title Case headlines, `Lorem ipsum`, John Doe, unsourced `92%`, elevate/seamless/unleash. Error copy: what happened + the next step.

## Operate UX

Product chrome stays predictable. Same control, same result. One vocabulary. Platform back and search stay where people expect them. Mixing tab + sidebar + bottom nav at the same hierarchy fails.

Proximity groups; one accent; not everything bold. Every action gets hover/active; async gets loading; errors say what happened and how to recover. Exit on every overlay. Undo on destructive when feasible.

One filled primary per view. Nav answers where I am. Back restores scroll and filters. Visible label on every field. Catalog >12 items: filter first.

Task completion, then a11y, then brand.

## Surfaces

Nav, header, toolbar, rails. Done at 1024 and 1440, or failed and fixed.

Controls sit inside the chrome padding box. Inset, `min-width: 0` on the flex child, truncate with a keyboard-reachable full string. Rail padding ≥ control padding. One filled primary per view.

Nested chrome: `outerRadius = innerRadius + padding` (choose independently if padding >24px). Nested cards fail. Icon+label: icon-side padding = text-side minus `2px`, still inside the box.

Same-plane chrome: hairline. Overlay: elevation, one light source. Product-plane chrome uses fill plus hairline.

Hit ≥44px **inside** the parent; ≥8px gap. Live numbers: `tabular-nums`. Smoothing once on `html`. `text-wrap: balance` on view `h1`–`h3` only. Chrome icons: one family, `currentColor`, outline at rest / fill active. Name the properties that change; skip `transition: all`. Press `scale(0.96)`, interruptible.
