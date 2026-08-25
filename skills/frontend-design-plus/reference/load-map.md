# Load map

Open this file from [after-briefing.md](after-briefing.md) after the Briefing card exists, to attach paths to a slot in [dispatch.md](dispatch.md). Origin `polish` on marketing or app UI: open from [polish.md](polish.md); skip after-briefing and dispatch. Open [execution-modes.md](execution-modes.md) with dispatch after the Briefing card exists; do not open it at Classify or while scoring briefing fields. If briefing answers do not exist and the form was not skipped, close this file and open [briefing.md](briefing.md). Greenfield marketing with Job still missing occupancy (A/B pick or named Scene), or Look still missing the Style answer: same. Polish mute with Focus still blank: close this file and stay on [polish.md](polish.md).

Attach only the rows that match this run **and** this slot. A row that does not match stays closed. The parent attaches paths; it does not open Direction, Implement, or QA bodies except on [isolated component](after-briefing.md#isolated-component).

## Polish

Stay-closed SSOT for `origin=polish` on marketing and app UI. Isolated component still uses [after-briefing.md](after-briefing.md#isolated-component).

Never attach: [briefing.md](briefing.md), [catalog.md](catalog.md), [design-styles.md](design-styles.md), `design-styles/*.md`, [composition.md](composition.md), [brand-register.md](brand-register.md), [product-register.md](product-register.md), [layout-patterns.md](layout-patterns.md), [dispatch.md](dispatch.md), [after-briefing.md](after-briefing.md), [crit.md](crit.md), [ux-principles.md](ux-principles.md), [visual-language.md](visual-language.md).

| Step | Attach | Stay closed extras |
| --- | --- | --- |
| Audit | [redesign.md](redesign.md#craft-audit). [design-md.md](design-md.md) only when DESIGN.md is missing (extract from current CSS). | [color.md](color.md) unless `focus=color`; [typography.md](typography.md) unless `focus=hierarchy`; [design-systems.md](design-systems.md) unless `focus=rhythm` |
| Implement | [implement.md](implement.md), DESIGN.md (path in the slim packet), [redesign.md](redesign.md), [verification.md](verification.md) | [file-architecture.md](file-architecture.md), [layout-patterns.md](layout-patterns.md), [assets.md](assets.md) unless Constraints named media |
| Implement signal | `focus=a11y` or constraints i18n/RTL: [production-engineering.md](production-engineering.md#harden). `focus=states`: [production-engineering.md](production-engineering.md). App UI chrome: [surfaces.md](surfaces.md). `focus=color`: [color.md](color.md). `focus=hierarchy`: [typography.md](typography.md). `focus=rhythm`: [design-systems.md](design-systems.md). Behave fluid/cinematic: [motion.md](motion.md) | — |
| QA slim | [anti-slop.md](anti-slop.md) Always + polish branch, [preflight-checklist.md](preflight-checklist.md) Tier A, [verification.md](verification.md), [visual-rubric.md](visual-rubric.md) (skip Structural necessity and Domain specificity), [quality-cases.md](quality-cases.md) | [crit.md](crit.md), [performance.md](performance.md) |

Done when every matching row for the current step is open and every file in Never attach stayed closed.

## Parent

Open [after-briefing.md](after-briefing.md), [dispatch.md](dispatch.md), and [execution-modes.md](execution-modes.md) after the Briefing card exists. [product-context.md](product-context.md) is briefing-only; after the card, copy cells from the card and keep that file closed. Stay closed: [composition.md](composition.md), [design-styles.md](design-styles.md), [catalog.md](catalog.md), `design-styles/*.md`, [anti-slop.md](anti-slop.md), [crit.md](crit.md), [visual-rubric.md](visual-rubric.md), [verification.md](verification.md), [preflight-checklist.md](preflight-checklist.md), [implement.md](implement.md), [product-register.md](product-register.md), [product-context.md](product-context.md), [ux-principles.md](ux-principles.md), [layout-patterns.md](layout-patterns.md). Isolated component is the exception: [implement.md](implement.md) plus Component rows below, [anti-slop.md](anti-slop.md) Always, [preflight-checklist.md](preflight-checklist.md) Tier A, [verification.md](verification.md). Skip [crit.md](crit.md). [visual-rubric.md](visual-rubric.md) when scoring craft; skip Structural necessity and Domain specificity.

## Direction

| Origin | Attach | Stay closed |
| --- | --- | --- |
| `greenfield` | — | [redesign.md](redesign.md) |
| `redesign` | [redesign.md](redesign.md) | [design-styles.md](design-styles.md), `design-styles/*.md` |
| `polish` | skip this slot — [polish.md](polish.md) | [dispatch.md](dispatch.md) Direction; see [Polish](#polish) |

| Task | Attach | Stay closed |
| --- | --- | --- |
| **Component** | skip this slot | — |
| **App UI** | [design-md.md](design-md.md), [product-register.md](product-register.md) | [layout-patterns.md](layout-patterns.md), [assets.md](assets.md), [composition.md](composition.md), [ux-principles.md](ux-principles.md), [design-styles.md](design-styles.md), [catalog.md](catalog.md), `design-styles/*.md` unless Look is a named catalog `id` |
| **Marketing** | [design-md.md](design-md.md). Greenfield or redesign: [composition.md](composition.md) first. [brand-register.md](brand-register.md) only **after** Frame and Sketch exist (same slot; occupancy is already committed). | [product-register.md](product-register.md), [ux-principles.md](ux-principles.md), [layout-patterns.md](layout-patterns.md) |

| Signal | Attach | Stay closed |
| --- | --- | --- |
| Greenfield **marketing** Look is a catalog `id` | that one `design-styles/<id>.md` and [design-styles.md](design-styles.md) (Pick step 1 + Commit) | the rest of `design-styles/`, [catalog.md](catalog.md) |
| Greenfield **marketing** Look is an Item number | [catalog.md](catalog.md) to map the number if the table is not already in chat, then that one `design-styles/<id>.md` and [design-styles.md](design-styles.md) | the rest of `design-styles/` |
| Greenfield **marketing** Look names 1–3 sites with a craft *why* and no `id` | [catalog.md](catalog.md) to map the *why* onto one Description row, then that one `design-styles/<id>.md` and [design-styles.md](design-styles.md) | the rest of `design-styles/` |
| Greenfield **marketing** Look is `you-decide` / `none` (Style **no**, invent-all, or unnamed after they declined) | Lock `style=none`. Craft from the enter object in DESIGN.md. Do not match catalog **When**. | [design-styles.md](design-styles.md), [visual-language.md](visual-language.md) unless `style=custom`, `design-styles/`, [catalog.md](catalog.md) |
| Greenfield marketing uses `style=custom` | [visual-language.md](visual-language.md) | `design-styles/`, [design-styles.md](design-styles.md), [catalog.md](catalog.md) |
| App UI Look is a named catalog `id` | that one `design-styles/<id>.md` (craft blanks only; layout stays [product-register.md](product-register.md)) | the rest of `design-styles/`, [catalog.md](catalog.md) |
| App UI uses `style=custom` by explicit request | [visual-language.md](visual-language.md) | `design-styles/`, [design-styles.md](design-styles.md), [catalog.md](catalog.md) |
| App UI Look is skipped / `none` | — | [design-styles.md](design-styles.md), [catalog.md](catalog.md), `design-styles/*.md` |
| App UI or marketing (palette in play) | [color.md](color.md) | — |
| Parent re-dispatch for invalid Lock | [design-read-examples.md](design-read-examples.md) | — |
| Type pairing still blank after the style file and DESIGN.md | [typography.md](typography.md) | — |
| Density-band recipe is not already in DESIGN.md **Layout** | [design-systems.md](design-systems.md) | — |
| Polish Focus is `a11y`, Packet `constraints=` names i18n/RTL, briefing Constraints named i18n/RTL, or the user named edge cases / production-ready | [production-engineering.md](production-engineering.md#harden) | — |

Stay closed on Direction: [implement.md](implement.md), [anti-slop.md](anti-slop.md), [crit.md](crit.md), [preflight-checklist.md](preflight-checklist.md), [file-architecture.md](file-architecture.md), [surfaces.md](surfaces.md), [production-engineering.md](production-engineering.md) unless the Harden signal attached it, [motion.md](motion.md), [assets.md](assets.md), [layout-patterns.md](layout-patterns.md), [product-context.md](product-context.md), [visual-language.md](visual-language.md) unless `style=custom`, [catalog.md](catalog.md) unless Look is an Item number or 1–3 sites with a craft *why*, [design-read-examples.md](design-read-examples.md) unless the parent named an invalid Lock.

## Implement

Always attach [implement.md](implement.md) and DESIGN.md (path in the Packet).

Always attach [verification.md](verification.md) for the viewport return and evidence block.

| Origin / task | Attach | Stay closed |
| --- | --- | --- |
| `greenfield` (not isolated component) | [file-architecture.md](file-architecture.md) | — |
| `redesign` | [redesign.md](redesign.md) | [file-architecture.md](file-architecture.md) |
| `polish` | [redesign.md](redesign.md); see [Polish](#polish) | [file-architecture.md](file-architecture.md), [layout-patterns.md](layout-patterns.md), [composition.md](composition.md), [catalog.md](catalog.md), [design-styles.md](design-styles.md), `design-styles/*.md` |
| **Component** (parent in-process) | [production-engineering.md](production-engineering.md), [file-architecture.md](file-architecture.md) when greenfield. [design-md.md](design-md.md) when `DESIGN.md` exists or the component introduces tokens | [brand-register.md](brand-register.md), [layout-patterns.md](layout-patterns.md), [product-register.md](product-register.md), [composition.md](composition.md), [assets.md](assets.md) unless the user asked for a visual restyle |
| **App UI** | [surfaces.md](surfaces.md), [production-engineering.md](production-engineering.md), [motion.md](motion.md) Product micro, [product-register.md](product-register.md) (named `recipe=` heading; do not pick a new recipe) | [layout-patterns.md](layout-patterns.md), [composition.md](composition.md), [design-styles.md](design-styles.md) |
| **Marketing** | Greenfield or redesign: [layout-patterns.md](layout-patterns.md) (Frame tracks first, then First three folds to confirm Packet `:<form>`), [production-engineering.md](production-engineering.md#resilient-text). Polish: skip layout-patterns ([Polish](#polish)). | [product-register.md](product-register.md), [ux-principles.md](ux-principles.md). Full [production-engineering.md](production-engineering.md) only when the surface has forms or async, or the Harden row below matches |

| Signal | Attach | Stay closed |
| --- | --- | --- |
| Packet `style_path` is not `none` | that one `design-styles/<id>.md` | the rest of `design-styles/`, [design-styles.md](design-styles.md) |
| Packet `language_path` is not `none` | [visual-language.md](visual-language.md) | `design-styles/`, [design-styles.md](design-styles.md) |
| Behave or Lock `fluid` / `cinematic` | [motion.md](motion.md) | — |
| Behave `still` / `none` on **marketing** | — | [motion.md](motion.md) |
| Constraints or Look name photo, video, or illustration | [assets.md](assets.md) | — |
| No media named | — | [assets.md](assets.md) |
| Palette or theme in play | [color.md](color.md) | — |
| Lock names a nested enclosure, hairline, or island CTA | [material-craft.md](material-craft.md) | — |
| Marketing `greenfield` or `redesign` | [performance.md](performance.md) | — |
| App UI Packet *job* has media or a chart in the first paint | [performance.md](performance.md) | — |
| App UI first paint has no media or chart | — | [performance.md](performance.md) |
| Type pairing still blank | [typography.md](typography.md) | — |
| Density-band recipe missing from DESIGN.md **Layout** | [design-systems.md](design-systems.md) | — |
| App UI | [ux-principles.md](ux-principles.md). Dashboards heading only when Packet *job* asks a chart or BI question | — |
| Focus is a11y, Packet `focus=a11y`, Packet `constraints=` names i18n/RTL, or the user named edge cases / production-ready | [production-engineering.md](production-engineering.md#harden) | — |
| App UI and the prompt names onboarding, first-run, empty, or activation | [product-register.md](product-register.md#onboard) | — |

Stay closed on Implement: [briefing.md](briefing.md), [product-context.md](product-context.md), [composition.md](composition.md), [design-styles.md](design-styles.md), [catalog.md](catalog.md), [anti-slop.md](anti-slop.md), [crit.md](crit.md), [preflight-checklist.md](preflight-checklist.md).

## Fast

When Lock `mode=fast`, also stay closed even if a matching row would attach:

- [design-read-examples.md](design-read-examples.md) unless the parent named an invalid Lock
- [typography.md](typography.md) when DESIGN.md already names type
- [color.md](color.md) when Theme and Palette already have owners

## QA

| When | Attach |
| --- | --- |
| After markup, before calling the surface done | [anti-slop.md](anti-slop.md), [crit.md](crit.md), [visual-rubric.md](visual-rubric.md), [quality-cases.md](quality-cases.md), [verification.md](verification.md) |
| Marketing `greenfield` or `redesign` | also [performance.md](performance.md) (targets for `performance=verified`) |
| After the written *crit* | [preflight-checklist.md](preflight-checklist.md) (tier from [task routing](../SKILL.md#task-routing)) |

Stay closed on QA: [composition.md](composition.md), [design-styles.md](design-styles.md), [catalog.md](catalog.md), [implement.md](implement.md), [briefing.md](briefing.md), [product-context.md](product-context.md). Use the Packet for briefing facts.

Done when every matching row for the current slot is in that slot's prompt and every non-matching file stayed closed.
