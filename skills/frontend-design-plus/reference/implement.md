# Implement

Open from the Implement slot ([dispatch.md](dispatch.md)). Unanswered blanks belong to the Packet, not this file. Do not open this file at Classify or during Briefing.

The layout kit is the full Packet plus DESIGN.md plus the attached Implement paths. Marketing greenfield/redesign: the first viewport **is** the Sketch. App UI: `recipe=` plus the matching heading in [product-register.md](product-register.md) when attached; do not pick a new recipe. Do not load QA files. Do not reopen [composition.md](composition.md).

## First viewport

The first viewport **is** the Packet Sketch at the occupancy numbers in DESIGN.md Layout. Marketing greenfield/redesign: enter, rest, and *break* (or two masses when `break=none`) are on screen at those tracks. Do not pad empty `fr` with a stock photo. Polish: keep the current family; close the craft-audit items. App UI: `Sketch=none`; `main` on a Pareto screen is the work queue or list, not chrome and not a greeting.

Headlines and the primary CTA come from the Packet. H1, subtext, and CTA *divide*: each piece does one job. The visible primary label **is** Packet Success (verb+object). Wordmark and `<title>` use Lock `name=`. Do not vest `first-character-costume=`.

### Viewport proof (marketing greenfield/redesign)

This phase has its own done before folds.

1. Markup: `data-mass="enter"` / `"rest"` / `"break"` (omit `break` when `break=none`).
2. CSS tracks cite the Sketch numbers (layout-patterns Frame tracks when that file is attached).
3. Measure columns: `getBoundingClientRect().width / viewport` rounded to 12. Measure scale: computed `font-size` of the largest text inside `[data-mass="enter"]` vs `body` (same Frame tracks heading). Capture 1440 of the first viewport when the harness has screenshot or browser this run — required then. Without that tool: DOM rects. `scrollWidth > clientWidth` at 375 goes in `proof`.
4. Return:

```txt
See: <enter object noun as it appears in that rectangle's text, alt, or figcaption>
tracks=enter <n/12 measured> rest <n|inset|below> break <n|none>
scale=<enter px>/<body px> | mass
proof=<1440 path | DOM rects>
distinct=<Packet first-character-costume=; one markup or CSS fact that still kills it after the wordmark is removed>
cta=<Success verb+object on the primary control>
```

`See:` is the visible noun in the enter rectangle. The `data-mass` attribute is not `See:`. `distinct=` is the costume plus one fact: object, *join*, reading order, material, or interaction. `data-mass`, a utility class name, and a color token are not facts.

**Verification return:** use the [verification](verification.md) block with `proof=browser`, `dom`, `static`, or `unverified`. Do not call an uninspected render a pass.

Done when the return block exists, `|measured − Sketch| ≤ 1` column, `See:` is the enter *object* as visible text or media in that rectangle, `scale=` holds (Frame tracks), and `cta=` is the Success label on the primary control. The primary CTA is visible without scroll in the first viewport. P0 and CTA sit on Packet `scan=`. The H1 wraps to at most two lines at desktop. A component kit does not define the look (theme, type, radius, and copy come from DESIGN.md). `first-character-costume=` is not on screen. Do not use First three folds until this holds (marketing only; layout-patterns stays closed on app UI and component). Marketing text+blob as the enter mass fails unless Packet P0 perception is type — then do not add invented media.

### Viewport proof (app UI)

This phase has its own done before extra craft.

1. `main` holds the work the recipe names (queue, list, canvas, people) or the settings shell when `recipe=none`.
2. Greeting nodes in `main` = 0.
3. Capture 1440 of `main` when the harness has screenshot or browser this run — required then. Without that tool: DOM.
4. Return:

```txt
main=<queue|list|canvas|people|settings>
proof=<1440 path | DOM>
```

**Verification return:** use the [verification](verification.md) block with the evidence level and any unverified visual or interaction checks.

Done when the return block exists and `main=` matches Packet `recipe=` (`queue-home` → `queue`, `list-filter` → `list`, `editor` → `canvas`, `accounts` → `people`, `recipe=none` → `settings`). Do not return `See:`, `tracks=`, or `scale=`.

App UI screenshot, when the harness has one: `main` is the work queue or list (or the settings shell).

## One folds list or one recipe

Marketing: ship the Sketch and `folds=`. Fold 2 and fold 3 show leftover Inventory *objects* in *job* order, in the `:<form>` Packet already named. A two-fold page is done when P0 cut removed the third object. Do not add a family to complete a page template. When [layout-patterns.md](layout-patterns.md) is attached: map `join=` under Frame tracks first; after `tracks=` holds, use First three folds only to **confirm** each Packet `:<form>` is on screen. App UI and component: do not open layout-patterns. A fold that is icon + title + blurb × N fails unless the Inventory object is a catalog of items. A fold missing `:<form>` fails; resume Direction.

App UI: ship Packet `recipe=` and `Pareto=` when the view is a CMS/admin/CRM home, list, editor, or accounts. Settings and other tools follow the app shell in [surfaces.md](surfaces.md) when that path is attached; `recipe=none` and `main=settings`. `main` is the work queue or list. Greeting in `main` fails.

A component kit is a *code floor*. Theme, type, radius, and copy come from DESIGN.md.

## Craft

When `style_path` is set, map that file's Craft onto the *thesis* already in DESIGN.md. Fill type, material, motion, radius, and shadow where DESIGN.md left them blank. Craft does not rewrite occupancy. A Path that names a hero family loses to the *frame*.

CSS custom properties map 1:1 to DESIGN.md tokens. Lock `theme=system`: two palettes plus a labeled chrome control ([color.md](color.md#system-theme) when attached).

## Files

Greenfield: write the tree in [file-architecture.md](file-architecture.md) when attached. Default with no framework: `index.html`, `main.css`, `main.js` at the surface root; HTML has no stylesheet dump.

Redesign and polish: patch the existing files on the current stack ([redesign.md](redesign.md) when attached). Keep functionality. Polish stops at craft levers 1–5 plus missing states on controls this pass touches.

## Work order

Viewport proof first (marketing greenfield/redesign: Sketch on screen; app UI: `main=`). Polish: skip viewport proof; close the craft-audit items. Then the [Production baseline](#production-baseline). Mechanical counts belong to QA pre-flight, not this slot. Open the owner only when that row is attached ([load-map.md](load-map.md)).

**Layout-first.** Write the skeleton (grid, flex, or stack) and name alignment (`justify-content`, `align-items`, Sketch `tracks=` when present) before injecting copy or images. Do not rely on browser defaults for alignment.

**Nesting.** After three or four layout wrappers, extract a subcomponent in `PascalCase`. Properties stay `camelCase` in JS.

**Tokens after Lock.** Color, space, type, and radius in surface CSS use DESIGN.md names. Raw hex or ad-hoc `px` on the surface fails, except: one bootstrap in DESIGN.md; `1px` hairline when the Lock named it; media-query breakpoints. A missing token: add it to DESIGN.md, then use the name. Do not invent `#6366f1`.

## Production baseline

| Requirement | Minimum |
| --- | --- |
| **States** | Default, hover, focus, active, disabled; loading, error, empty when async |
| **Accessibility** | Semantic HTML, labels, keyboard nav, visible focus, WCAG 2.2 AA contrast |
| **Responsive** | Mobile-first; touch targets ≥44px with ≥8px gap; no horizontal overflow on 320px; viewport allows zoom |
| **Design system** | Reuse project tokens, DESIGN.md, and components |
| **Files** | Markup, styles, and behavior in the project's (or default) split; CSS tokens match DESIGN.md |

## File done

Greenfield-with-no-framework has `index.html`, `main.css`, and `main.js` on disk. Marketing greenfield/redesign Viewport proof holds (`See:` / `tracks=` / `scale=` / `proof=` / `distinct=` / `cta=`; `|measured − Sketch| ≤ 1`; `See:` visible in the enter rectangle; `scale=` holds; CTA visible without scroll; H1 ≤2 lines desktop; P0+CTA on `scan=`; costume off screen) and each Packet fold is on screen in its `:<form>` with no extra family. Polish: current family. App UI: `main=` / `proof=` matches `recipe=` (`none` → settings). Lock `theme=system` ships two modes and a chrome switch. The [verification](verification.md) block declares evidence and gaps. Resume-from-QA: every P0 in the table is in the DOM or discarded with a user-goal reason. Resume may correct `tracks=` CSS or enter type scale; it does not change `join=`. Resume does not invent Inventory nouns. Resume does not vest `first-character-costume=`.
