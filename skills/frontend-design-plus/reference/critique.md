# Critique

Open once after markup. Confirm the DESIGN.md spine held. Do not invent a second look.

When the table lists Design or Copy, open [anti-slop.md](anti-slop.md) in the same pass.

| Origin / Mode                                             | In scope                                                                                                           |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| greenfield                                                | Design + Copy + matching Mode headings                                                                             |
| redesign                                                  | Design except triad and `cream-warmth`; Copy; matching Mode headings                                               |
| polish                                                    | Design except triad, `cream-warmth`, and logo-swap; Copy only on strings this pass changes; matching Mode headings |
| Isolated component                                        | Design table, Enter, Deletion. Copy if the control has a visible label. Fit if the control sits in chrome          |
| `Persuade` with no nav/header rail                        | skip Surfaces                                                                                                      |
| `Operate`, or any chrome this pass touches                | Operate UX + Surfaces                                                                                              |
| `Persuade`/`Experience` conversion chrome (form, pricing) | Operate UX                                                                                                         |

Done when every spine row below that applies holds, and every Fail-if in [anti-slop.md](anti-slop.md) in scope is gone, or each remaining match has a written reason. Fix this turn.

**Enter**: First viewport includes a live fragment of the object (the brief, the queue, the kiln), not H1 plus CTA alone. A noun only in the H1 fails. At 375 that fragment sits below a one-row header with the drawer closed; an open menu in flow fails (`drawer-stuck`).

**Deletion**: Name one fold the brief did not ask for and that is not Signature, including a close how-it-works. Fail if it remains. Motion chrome (parallax, custom cursor, uniform fade-in) fails unless named.

**CTA**: Visible primary is the Job verb+object. Same action, same label (`label-drift`).

**Persuade**: Logo-swap breaks the read. Navy-for-law, indigo-for-SaaS fail. Costume hop and cream+serif: [anti-slop.md](anti-slop.md#design) (`model-default-triad`). The fold after enter names a different object noun or is the create control (`repeat-hero`).

**Operate**: Four equal KPIs + donut + "Welcome back" fails. `h1` in `main` is the queue or the view. Domain nouns live in rows and empty copy.

## Operate UX

Product chrome stays predictable. Same control, same result. One vocabulary. Platform back and search stay where people expect them. One nav pattern per hierarchy.

Proximity groups; one accent; not everything bold. Every action gets hover/active; async gets loading; errors say what happened and how to recover. Exit on every overlay. Undo on destructive when feasible.

One filled primary per view. Nav answers where I am. Back restores scroll and filters. Visible label on every field. Catalog >12 items: filter first.

Task completion, then a11y, then brand.

## Surfaces

Nav, header, toolbar, rails. Done at 375, 1024, and 1440, or failed and fixed.

Controls sit inside the chrome padding box. Inset, `min-width: 0` on the flex child, truncate with a keyboard-reachable full string. Rail padding ≥ control padding. One filled primary per view. Destinations in one row at 1440; at 375 wordmark plus at most two controls, drawer closed, filled primary in the hero. Chrome Fail-ifs: [anti-slop.md](anti-slop.md#design) (`drawer-stuck`, `header-chrome-budget`, `chrome-overlap`, `wrapped-cta`, `header-second-primary`, `cta-pair-375`, `equal-row-375`).

Nested chrome: `outerRadius = innerRadius + padding` (choose independently if padding >24px). Nested cards fail. Icon+label: icon-side padding = text-side minus `2px`, still inside the box.

Same-plane chrome: hairline. Overlay: elevation, one light source. Product-plane chrome uses fill plus hairline.

Hit ≥44px **inside** the parent; ≥8px gap. Live numbers: `tabular-nums`. Smoothing once on `html`. `text-wrap: balance` on view `h1`–`h3` only. Chrome icons: one family, `currentColor`, outline at rest / fill active. Name the properties that change; skip `transition: all`. Press `scale(0.96)`, interruptible.
