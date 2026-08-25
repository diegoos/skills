# Catalog

Briefing opens this file and prints this table only on Style pick after the user said yes ([briefing.md](briefing.md#look)). Direction opens it when Look is an Item number and the table is not already in chat. A named `id` attaches that style file and leaves this table closed. On `you-decide` / invent-all, keep it closed. Do not open [design-styles.md](design-styles.md) from this file. Do not print this table on app UI. Do not print it before Style **yes**.

Keep Item numbers stable so "item 13" maps to that row.

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

Sample systems from [Design Prompts](https://www.designprompts.dev/) sit in this repo under `_/design-styles/prompts/`. Lock names an id. Occupancy and recipe stay in the Packet; this table does not open composition, product-register, or layout-patterns.
