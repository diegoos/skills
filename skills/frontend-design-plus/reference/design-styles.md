# Design styles

Named styles are agent guides. They describe how a look behaves: type attitude, material, motion, density, and the cliché to refuse. The design the user already chose stays in charge.

Keep, in this order: briefing answers, Look, DESIGN.md, project tokens. Then use this folder to fill leftover blanks. Layout families still come from the briefing, DESIGN.md, and [layout-patterns.md](layout-patterns.md) (marketing) or [product-register.md](product-register.md) (app UI).

## Load

Open this file at Briefing only when the current blank is Look, origin is greenfield, task type is **marketing**, and Look is blank (print the Catalog table, then four fitting `AskQuestion` options). Open **one** file from [design-styles/](design-styles/) at Direction after answers. Hex and typefaces in that file are fallbacks for empty color and type slots. Do not open this folder at Classify.

On app UI, leave this folder closed and Lock `style=none`, unless Look is a named catalog `id` (craft blanks only; layout stays [product-register.md](product-register.md)). On `redesign` or `polish`, follow DESIGN.md, project tokens, and the current CSS. Leave this folder closed. Lock `style=none`. Origin detection: SKILL.md Classify; existing-surface rules: [redesign.md](redesign.md).

## Pick

Greenfield **marketing** only, after briefing answers (or invent-all). Skip this section on app UI except a named catalog `id` (step 1 only; do not match When on skipped `none`). Unanswered Look belongs to [briefing.md](briefing.md#look); do not pick an id in that turn.

**Median cluster** (you-decide and invent-all skip these unless the user named the id): `saas`, `enterprise`, `material-design`, `modern-dark`, `professional`, `flat-design`. Job = "SaaS product" or "B2B tool" is not a When.

1. If Look or the prompt names an `id` from the catalog, use that id. Authorship wins. The slop test still runs ([anti-slop.md](anti-slop.md)).
2. Else if Look is `you-decide` or `none`, or invent-all skipped the form: match job + audience + success + use + behave to one **When**. Write 2–3 sentences that name which When matched which fields. Open only that file. Refuse the median cluster. Refuse the [anti-slop.md](anti-slop.md) category default (developer portfolio is not `terminal` / `cyberpunk` / `web3` / `industrial` spec sheet; fintech is not navy-teal `saas`). If two Whens fit, take the farther from Inter + indigo + 16px radius. Behave may break ties (`cinematic` → `kinetic`, not `saas`).
3. Else if Look names sites or a metaphor without an id: one clause of *why* maps to one **When**. Do not blend two files. Cap 1–3 refs.
4. Write `style=<id>` on the Lock. Done when that id is in the Lock, the matching file is in context, and (you-decide / invent-all) the Pick sentences exist.

Skip this folder when the user named a live component library to follow as-is (Polaris, Carbon, USWDS). `style=none`. Quiet constraints still override Lock bands.

## Commit

After the one file is in context, write these into DESIGN.md **Layout** and the Lock before markup. Extract from that file's Craft and Path. Do not invent a second id.

- **Spatial** — grid stance, gutters, max column occupancy, type-scale jump, radius set, shadow recipe, motion `150–250ms ease-out` ([motion.md](motion.md)).
- **One loud thing** — numeric contrast: display type ≥3× body, or one block ≥8/12 columns, or radius `0` against `4px` controls. Marketing Lock already names this break.
- **Subtraction** — the Path cliché to delete until Job + Success still hold.
- **Forbids** — that Path cliché plus [anti-slop.md](anti-slop.md). Pair each with the do-instead already in those files.

A second style's tokens in CSS fail this step.

## Catalog

Print this table in chat at marketing Look (columns: Item, Style, Default Theme Mode, Short description). Style is the `id` in Title Case. Default Theme Mode is Mode. Short description is Description. Keep Item numbers stable so "item 13" maps to that row. Do not print this table on app UI.

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

Sample systems from [Design Prompts](https://www.designprompts.dev/) sit in this repo under `_/design-styles/prompts/`. Lock names an id. Page structure comes from the briefing and layout-patterns.md / product-register.md.
