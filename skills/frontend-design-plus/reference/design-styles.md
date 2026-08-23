# Design styles

Named styles are agent guides. They describe how a look behaves: type attitude, material, motion, density, and the cliché to refuse. The design the user already chose stays in charge.

Keep, in this order: briefing answers, Scene occupancy, Look, DESIGN.md, project tokens. Then use this folder to fill leftover blanks. Marketing folds: [composition.md](composition.md) *map* lists leftover *objects*; [layout-patterns.md](layout-patterns.md#first-three-folds) is an Implement lookup, not a menu. App UI recipes: [product-register.md](product-register.md#dashboards). A named style vests craft after *tension* and occupancy exist.

## Load

Open this file in the Direction slot when Look is a catalog `id`, or when Look is `you-decide` / `none` / invent-all on greenfield marketing ([dispatch.md](dispatch.md), [load-map.md](load-map.md)). Hex and typefaces in the matching style file are fallbacks for empty color and type slots. Do not open this folder at Classify or Briefing. Printing the Catalog table in the parent chat fails [briefing.md](briefing.md). The parent orchestrator does not open this file.

On app UI, leave this folder closed and Lock `style=none`, unless Look is a named catalog `id` (craft blanks only; layout stays [product-register.md](product-register.md)). On `redesign` or `polish`, follow DESIGN.md, project tokens, and the current CSS. Leave this folder closed. Lock `style=none`. Origin detection: SKILL.md Classify; existing-surface rules: [redesign.md](redesign.md).

## Pick

Greenfield **marketing** only, after briefing answers (or invent-all). Skip this section on app UI except a named catalog `id` (step 1 only; do not match When on skipped `none`). Unnamed greenfield marketing Look is `you-decide` ([briefing.md](briefing.md#look)); run this Pick after Frame.

**Quiet-chrome cluster** (`saas`, `enterprise`, `material-design`, `modern-dark`, `professional`, `flat-design`): not a default because the job is a SaaS product or a B2B tool. Match only when Packet *tension* is quiet chrome (the interface should recede).

**Second-hop cluster** (`kinetic`, `organic`, `swiss-minimalist`, `newsprint`, `monochrome`, `bold-typography`): not the automatic next pick after refusing quiet chrome. Match only when *tension* names that axis (acid type, editorial serif, visible Swiss grid). “Then editorial” without *tension* fails.

**Model-default triad** (cream ~`#F4F1EA` + high-contrast serif + terracotta; near-black + one acid or vermilion; broadsheet hairline, radius 0, dense columns): not a first Pick on `you-decide` / invent-all. Match only when Packet *tension* names that axis (paper field + serif + clay accent; phosphor on black; news columns). Brief names it, brief wins. `newsprint` only when *tension* asks for columns, not as “not SaaS.” Authorship (`id` named) is still step 1.

1. If Look or the prompt names an `id` from the catalog, use that id. Authorship wins. QA still runs the slop test.
2. Else if Look is `you-decide` or `none` (including unnamed greenfield marketing Look), or invent-all skipped the form: catalog is not the default. (a) If Packet *tension* matches one **When**, use that `id`, vest craft only, leave occupancy untouched, and write 2–3 sentences that name which When matched *tension* **and** which *frame* mass (`enter` / `rest` / *break*) the Path vests. (b) Else set `style=custom` and open [visual-language.md](visual-language.md), or set `style=none` and fill craft from DESIGN.md. Do not pick `saas`, `enterprise`, or the cream-serif-terracotta triad without *tension*. A named look without *tension* fails — leave `style=none`. Scene occupancy is not a license for `newsprint`, `botanical`, or `cyberpunk`. Refuse the id whose Path cliché **is** the occupancy. If two Whens fit, take the one whose Path vests the P0 mass. Behave may break ties (`cinematic` → a When that names cinematic motion). Do not pick “the farther from Inter.”
3. Else if Look names sites or a metaphor without an id: one clause of *why* maps to one **When**. Do not blend two files. Cap 1–3 refs.
4. Write `style=<id>`, `style=custom`, or `style=none` on the Lock. Done when that value is in the Lock, the matching file or custom register is in context when not `none`, and (you-decide / unnamed / invent-all) the Pick or custom-language evidence exists and names a *frame* mass when marketing uses a Frame.

Skip this folder when the user named a live component library to follow as-is (Polaris, Carbon, USWDS). `style=none`. Quiet constraints still override Lock bands.

## Commit

After the one catalog file or custom register is in context, map Craft onto the *thesis* already in DESIGN.md **Layout**. Extract type, material, motion, radius, and shadow from that file's Craft and Path, or from [visual-language.md](visual-language.md). Do not invent a second id. Do not choose a hero family here. Craft does not rewrite Frame occupancy. A Path that names a hero family loses to the *frame*.

- **Spatial** — confirm occupancy numbers and type-scale jump from the *frame* / *thesis*; fill gutters, radius set, shadow recipe, motion `150–250ms ease-out` only where DESIGN.md left them blank (cinematic Lock may exceed that band).
- **One loud thing** — numeric contrast that serves the *break* mass when one exists: display type ≥3× body, or one block spanning most of the first viewport, or radius `0` against `4px` controls. Two-mass page: enter/rest contrast is the loud thing. Marketing Lock already names this break.
- **Folds** — confirm `folds=` from the *map* ([composition.md](composition.md)). Missing folds or a family name that rewrites occupancy: stop and open that file.
- **Subtraction** — the Path cliché to delete until Job + Success still hold.
- **Forbids** — that Path cliché. Pair it with the do-instead already in this file's Path.

A second style's tokens in CSS fail this step.

## Catalog

Direction reads this table for Pick. Keep Item numbers stable so "item 13" maps to that row. Do not print this table in the parent chat. Do not print it on app UI.

| Item| id                 | Mode | Font | Description                                                                                                      |
| --- | ------------------ | ---- | ---- | ---------------------------------------------------------------------------------------------------------------- |
| 1   | `monochrome`       | light| serif| A stark editorial system on pure black and white. No accent colors: contrast, oversized serif, geometric layouts.|
| 2   | `bauhaus`          | light| sans | Primaries, hard geometry, form follows function. Type and blocks sit on a visible workshop grid.                 |
| 3   | `modern-dark`      | dark | sans | Near-black product night with one indigo signal. Quiet chrome, not a neon HUD.                                   |
| 4   | `newsprint`        | light| serif| Paper, ink, and column grid. Headlines behave like a front page, not a SaaS hero.                                |
| 5   | `saas`             | light| sans | Product-clean app chrome. Layout must still pass category-reflex; do not treat this as the default landing.      |
| 6   | `luxury`           | light| serif| Alabaster surfaces, wide-tracked labels, scarce gold. Quiet wealth, not hotel navy.                              |
| 7   | `terminal`         | dark | mono | Phosphor shell, all monospace. A command line as the page, not a fake git-diff card.                             |
| 8   | `swiss-minimalist` | light| sans | Visible grid, grotesk type, Swiss red as the only signal.                                                        |
| 9   | `kinetic`          | dark | sans | Type is the surface. Acid flood, cinematic motion, one loud word.                                                |
| 10  | `flat-design`      | light| sans | Solid fills, Flat 2.0 affordance, no decorative shadow.                                                          |
| 11  | `art-deco`         | dark | serif| Fan geometry, champagne, gold rule. Evening dress, not a dashboard.                                              |
| 12  | `material-design`  | light| sans | Tonal surfaces, elevation, pill controls. Follow Material roles, not a purple gradient.                          |
| 13  | `neo-brutalism`    | light| sans | Thick ink, hard offset shadow, loud type. Raw and flat, not soft clay.                                           |
| 14  | `bold-typography`  | dark | sans | The headline is the layout. One display line occupies the first viewport.                                        |
| 15  | `academia`         | dark | serif| Library night, brass, manuscript serif. Scholarship as atmosphere.                                               |
| 16  | `cyberpunk`        | dark | mono | High-contrast neon on black, chamfer HUD, glitch on the live signal.                                             |
| 17  | `web3`             | dark | sans | Void plus Bitcoin orange. Mono on data, not a generic crypto gradient.                                           |
| 18  | `playful-geometric`| light| sans | Memphis stickers, hard shapes, confetti behind type. Toys with a grid.                                           |
| 19  | `minimal-dark`     | dark | sans | Three slates, one amber, hairline rules. Quiet night UI.                                                         |
| 20  | `claymorphism`     | light| sans | Inflated pastel volume, extra contrast so depth still reads.                                                     |
| 21  | `professional`     | light| serif| Ivory editorial, one gold, hairline rules. Consultancy, not beige craft.                                         |
| 22  | `botanical`        | light| serif| Forest, arch, plant motion. Living matter as structure.                                                          |
| 23  | `vaporwave`        | dark | sans | Magenta/cyan void, glitch with reduced-motion freeze.                                                            |
| 24  | `enterprise`       | light| sans | B2B product voice, committed indigo. Skip unless the user named this id.                                         |
| 25  | `sketch`           | light| sans | Organic wobble, handwritten labels, paper texture. Marker and pencil, real words.                                |
| 26  | `industrial`       | light| sans | Chassis, 45° light, safety-orange press. Workshop metal, not a spec-sheet title block.                           |
| 27  | `neumorphism`      | light| sans | Soft extrusion. Contrast before depth so controls stay findable.                                                 |
| 28  | `organic`          | light| sans | Moss, blob radii, grain. Soft volume without claymorphism puff.                                                  |
| 29  | `maximalism`       | dark | sans | Drenched chroma, one CTA. Excess with a single action.                                                           |
| 30  | `retro`            | light| sans | Bevel, 0 radius, system primaries. Early-web honesty, not nostalgia stickers.                                    |

Sample systems from [Design Prompts](https://www.designprompts.dev/) sit in this repo under `_/design-styles/prompts/`. Lock names an id. Page structure comes from [composition.md](composition.md) (marketing) or [product-register.md](product-register.md) (app UI). Fold-shape vocabulary at Implement: [layout-patterns.md](layout-patterns.md).
