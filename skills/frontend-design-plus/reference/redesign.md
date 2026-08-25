# Redesign and polish

Load when [load-map.md](load-map.md) attaches this file (`origin=redesign` or `origin=polish`). Polish: [polish.md](polish.md) opens the [craft audit](#craft-audit) in the same window; do not wait for a Direction slot. Greenfield skips this file. Do not open this file to detect origin; SKILL.md Classify is enough.

Misclassifying origin is the usual source of bad output: a rewrite of a live page, a catalog style on a determined look, or a timid restyle of a blank file.

## Detect origin

Name `greenfield`, `redesign`, or `polish` before markup. Evidence, in order:

1. The user says polish, tighten, improve craft, fix spacing, contrast, states, or a11y, and does not ask for a new look → `polish`.
2. The user says redesign, restyle, redo the layout, new IA, or "rethink this page" → `redesign`.
3. The target path, route, or URL already has markup, and the brief is "make this match / better" without a new look → `polish`.
4. The target already has markup, and the briefing names a new job, audience, success, or composition → `redesign`.
5. Otherwise `greenfield`: new surface, empty path, or the user approved a full restart.

If origin is still unclear, ask once: new UI, redesign this page from your briefing, or polish what is here?

Existing surface: follow DESIGN.md, project tokens, current CSS, stack, wordmark, and copy voice. Lock `style=none`. Leave [design-styles.md](design-styles.md) closed. A catalog `id` on redesign or polish fails this file. Do not overlay a second default system (Shadcn theme, catalog craft) on a live brand.

Polish that uncovers an IA problem the user did **not** name: list it as a finding. Do not recompose. If they named the IA problem, stop this slot and return to the parent: origin is `redesign`. The parent opens briefing Redesign. Do not open [briefing.md](briefing.md) from Direction or Implement.

## Sequence

1. **Scan.** Read the existing page and its stack: framework, styling method, tokens, neighbors. Stay on that stack. Check the lockfile before any new dependency. Tailwind: read v3 vs v4 before touching config. No framework: vanilla CSS.
2. **Diagnose.** Write the audit. Redesign: keep / retire / missing against Aim ([Audit before changing](#audit-before-changing)). Polish: the [craft audit](#craft-audit). Every item is keep, unify, or fix. Name filler to delete. Done when the ranked list exists; no visual edit before that. If DESIGN.md tokens ≠ shipped CSS, patch DESIGN.md from CSS in the same Diagnose pass ([design-md.md](design-md.md)).
3. **Fix.** Patch the files that already ship the surface. Improve what is there. Polish keeps the current layout family and visual language; success is deletion and craft, not a new look. Redesign may recompose from Aim/Keep/Scope, still on the current stack, still without breaking routes or behavior. Disk owns color, type, and radius unless the briefing names a token change. Test the flows you touched after each cluster of changes.

## Audit before changing

Redesign: document the current state, then mark each block keep, retire, or missing **against Aim**. Filler that does not serve Aim goes. A block that serves Aim is not swapped for fashion.

- Brand tokens: color, type, logo treatment, radii. Prefer `DESIGN.md` when it exists ([design-md.md](design-md.md))
- Information architecture: page tree, primary nav, conversion paths
- Content blocks: what works, what is filler
- Patterns to keep: signature interactions, recognisable hero, copy voice (Keep)
- Patterns to retire: slop tells for this task type ([anti-slop.md](anti-slop.md#the-slop-test)), broken layout, dead links (`href="#"`), missing hover/focus/loading/empty/error
- SEO baseline: ranking pages, titles, structured data, OG images
- Dial reading: infer current layout / motion / density bands as the starting point, not the marketing baseline
- Code: semantic landmarks, alt text, z-index scale, imports that exist in the lockfile

Done when the list exists and every remaining block maps to Aim or Keep. Direction then runs *composition* from those keep blocks (*job* → *objects* → *kinship* from Aim + keep, no Scene ask) when [composition.md](composition.md) is already attached, or names `recipe=` (app UI, if Aim is queue vs gallery). Do not attach composition from this file.

## Craft audit

Polish only. Written list, zero edits. Open the owner file when that row has a finding **and** [load-map.md](load-map.md) attaches that path to this slot. Otherwise name the fail; Implement or QA opens the owner. Each row is keep, unify, or fix.

| Row | Owner | Fail when |
| --- | --- | --- |
| Rhythm | [design-systems.md](design-systems.md#spacing-scale), density band | Ad-hoc gaps; section padding that ignores Lock `density=`; marketing hero top padding >`6rem` ([layout-patterns.md](layout-patterns.md#first-viewport-marketing)) |
| Hierarchy | [typography.md](typography.md#typography-system-define-upfront) | Five title sizes; body = label; `h1` is not the job of this view |
| Color | [color.md](color.md#building-a-palette) | Hex outside the token set; second accent per section; success = brand accent; grey-on-grey |
| Chrome | [surfaces.md](surfaces.md) on app UI | CTA kisses the rail; drop shadow fakes an overlay on the product plane; `transition: all` |
| Occupancy | [layout-patterns.md](layout-patterns.md#grids-and-lists) | Empty tracks; N items not in N cells |
| States | [production-engineering.md](production-engineering.md) | Missing hover/focus/disabled on a control this pass touches; missing loading/empty/error where that control is async |
| Harden | [production-engineering.md](production-engineering.md#harden) | Data overflow, missing `lang`/`dir` when Constraints named i18n, or one error string covering validation, network, and permission |
| Anti-slop | Matching branch of [anti-slop.md](anti-slop.md#the-slop-test) | Greeting `h1`, donut >3, decorative punctuation, portable slogan, overflow. Not category-reflex or logo-swap |
| Distill | [anti-slop.md](anti-slop.md) deletion check | Extra chrome the brief did not ask for still on the page |
| Copy | [anti-slop.md](anti-slop.md#copy-tells) | Portable slogan, divide fail, generic CTA |
| Motion | [motion.md](motion.md#product-micro) on app UI | Product micro missing on press; new cinematic layer |

Rank: **P0** contrast, overflow, hierarchy that hides the action, inconsistent accent, hit area. **P1** space/type scale, occupancy, states on the touched flow. **P2** radius trivia, motion. Direction is this list plus Lock `style=none` on redesign. On polish, [polish.md](polish.md) writes the slim packet; no new folds; no new recipe.

Done when every P0 and P1 on the list is closed. "Looks more polished" does not close.

## Preservation

- Keep URL slugs, anchor IDs, and primary nav labels stable unless asked
- Extract brand colors before applying [color.md](color.md) strategies; an existing purple stays purple until the user asks to kill it
- Preserve copy voice unless the user asked for a rewrite. Visual modernisation leaves the words.
- Honor existing accessibility wins (focus, alt, keyboard, contrast)
- Keep analytics event names, form field `name`s, and section IDs that tracking depends on
- Keep the styling system the project already uses
- Same chrome (button, input, nav item) three times with one-off styles: promote tokens and one shared component ([design-systems.md](design-systems.md#extract) when that file is attached; otherwise name the three sites here)

## Levers (stop when the brief is satisfied)

**Polish** uses 1–5, plus missing states on controls this pass touches (row States in the craft audit). **Redesign** may continue through 8 when Scope asks. Polish does not re-roll the aesthetic and does not pick a catalog `id`. Unify tokens; do not invent a palette.

1. Typography refresh (same families unless DESIGN.md already names a change)
2. Spacing and rhythm
3. Color recalibration (unify neutrals; keep the brand accent)
4. Hover, focus, and press states
5. Motion layer matching the current Lock band
6. Hero and key-section recomposition (redesign, inside Scope)
7. Loading, empty, and error states (redesign anywhere in Scope; polish only on controls this pass touches)
8. Full block replacement, only when the existing block cannot be saved (redesign, Scope `page` or `flow`)

Tokens that change globally (color, type, radius, space) belong in the design-token layer, not as one-off overrides per page. One token set; themes swap values. Polish patches tokens only for contrast or a named DESIGN.md gap.

## Never change silently

Require explicit user approval before changing:

- URL structure / route slugs
- Primary nav labels
- Form field names or order
- Brand logo or wordmark
- Legal, consent, or cookie copy
- Framework or CSS library migration

## See also

Load-map owns which of these files this slot may open. This list names owners, not extra opens: brand-register (marketing Direction after Frame), product-register (app UI Direction), composition (marketing Direction when attached), layout-patterns (Implement after `tracks=`), anti-slop (QA), production-engineering (Implement when attached).
