# Implement

Open from the Implement slot ([dispatch.md](dispatch.md)). Unanswered blanks belong to the Packet, not this file. Do not open this file at Classify or during Briefing.

Compose the first viewport from the Packet. Marketing greenfield/redesign: the Sketch. App UI: `recipe=`. Do not load QA files.

## First viewport

The first viewport **is** the Packet Sketch at the occupancy numbers in DESIGN.md Layout. Marketing greenfield/redesign: enter, rest, and *break* (or two masses when `break=none`) are on screen at those tracks. Do not pad empty `fr` with a stock photo. Polish: keep the current family; close the craft-audit items. App UI: `Sketch=none`; `main` on a Pareto screen is the work queue or list, not chrome and not a greeting.

Headlines and the primary CTA come from the Packet. Wordmark and `<title>` use Lock `name=`.

### Viewport proof (marketing greenfield/redesign)

This phase has its own done before folds.

1. Markup: `data-mass="enter"` / `"rest"` / `"break"` (omit `break` when `break=none`).
2. CSS tracks cite the Sketch numbers ([layout-patterns.md](layout-patterns.md#frame-tracks)).
3. Measure: `getBoundingClientRect().width / viewport` rounded to 12 columns. Capture 1440 of the first viewport when the harness has screenshot or browser this run — required then. Without that tool: DOM rects. `scrollWidth > clientWidth` at 375 goes in `proof`.
4. Return:

```txt
See: <object in the largest mass>
tracks=enter <n/12 measured> rest <n|inset|below> break <n|none>
proof=<1440 path | DOM rects>
```

Done when the return block exists, `|measured − Sketch| ≤ 1` column, and `See:` is the enter *object*. Do not open [layout-patterns.md](layout-patterns.md#first-three-folds) until this holds. Marketing text+blob as the enter mass fails unless Packet P0 perception is type — then do not add invented media.

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

Done when the return block exists and `main=` matches Packet `recipe=` (`queue-home` → `queue`, `list-filter` → `list`, `editor` → `canvas`, `accounts` → `people`, `recipe=none` → `settings`). Do not return `See:` or `tracks=`.

App UI screenshot, when the harness has one: `main` is the work queue or list (or the settings shell).

## One folds list or one recipe

Marketing: ship Packet Frame occupancy, the Sketch, and `folds=`. Fold 2 and fold 3 show leftover Inventory *objects* in *job* order. A two-fold page is done when P0 cut removed the third object. Map Frame *joins* to tracks ([layout-patterns.md](layout-patterns.md#frame-tracks)). After `tracks=` exists, open [layout-patterns.md](layout-patterns.md#first-three-folds) only when a leftover *object* has no obvious form (table, list, one proof, CTA). Do not walk that section as a menu.

App UI: ship Packet `recipe=` and `Pareto=` when the view is a CMS/admin/CRM home, list, editor, or accounts. Settings and other tools follow the app shell in [surfaces.md](surfaces.md) when that path is attached; `recipe=none` and `main=settings`. `main` is the work queue or list. Greeting in `main` fails.

A component kit is a *code floor*. Theme, type, radius, and copy come from DESIGN.md.

## Craft

When `style_path` is set, map that file's Craft onto the *thesis* already in DESIGN.md. Fill type, material, motion, radius, and shadow where DESIGN.md left them blank. Craft does not rewrite occupancy. A Path that names a hero family loses to the *frame*.

CSS custom properties map 1:1 to DESIGN.md tokens. Lock `theme=system`: two palettes plus a labeled chrome control ([color.md](color.md#system-theme) when attached).

## Files

Greenfield: write the tree in [file-architecture.md](file-architecture.md) when attached. Default with no framework: `index.html`, `main.css`, `main.js` at the surface root; HTML has no stylesheet dump.

Redesign and polish: patch the existing files on the current stack ([redesign.md](redesign.md) when attached). Keep functionality. Polish stops at craft levers 1–5 plus missing states on controls this pass touches.

## Work order

Top-down while writing. Open the owner only when that row is attached this slot ([load-map.md](load-map.md)).

| # | Focus | Check | Fail when |
| --- | --- | --- | --- |
| 1 | A11y | Contrast 4.5:1, visible focus, keyboard | Removing focus rings |
| 2 | Touch | Targets ≥44px, 8px gap, press feedback | Hover-only actions |
| 3 | Perf | LCP/CLS, reserved space | Layout shift |
| 4 | Direction | Packet Sketch + DESIGN.md | Markup that ignores Sketch, Thesis, or Lock `name=` |
| 5 | Layout | Mobile-first; N items → N cells at 768; Sketch occupancy; chrome in rail | Empty tracks; tracks that do not match Sketch; overflow rail |
| 6 | Type/color | DESIGN.md tokens | Raw hex, gray-on-gray |
| 7 | Motion | Recipe matches Lock `motion=` | One duration for everything |
| 8 | Forms | Labels; field-group grid; error keeps row | Independent columns; placeholder-as-label |
| 9 | Nav | Predictable back, one primary per view | Overloaded chrome |
| 10 | Data | Chart matches the operator question | Chart gallery, color-only encoding |

## Production baseline

| Requirement | Minimum |
| --- | --- |
| **States** | Default, hover, focus, active, disabled; loading, error, empty when async |
| **Accessibility** | Semantic HTML, labels, keyboard nav, visible focus, WCAG 2.2 AA contrast |
| **Responsive** | Mobile-first; touch targets ≥44px with ≥8px gap; no horizontal overflow on 320px; viewport allows zoom |
| **Design system** | Reuse project tokens, DESIGN.md, and components |
| **Files** | Markup, styles, and behavior in the project's (or default) split; CSS tokens match DESIGN.md |

## File done

Greenfield-with-no-framework has `index.html`, `main.css`, and `main.js` on disk. First viewport matches the Packet: marketing greenfield/redesign matches `style=` (or `none` when *tension* needs no named look), Look, *scene*, *thesis*, Sketch, occupancy rectangles, `folds=`, and the `See:` / `tracks=` / `proof=` return; polish: current family; app UI matches Pareto, the `main=` / `proof=` return, and `recipe=` when that view is a CMS/admin/CRM home, list, editor, or accounts (`recipe=none` on settings/shell). Lock `theme=system` ships two modes and a chrome switch. Resume-from-QA: every P0 in the table is in the DOM or discarded with a user-goal reason. Resume may correct `tracks=` CSS; it does not change `join=`. Resume does not invent Inventory to change `object-swap=n/a`.
