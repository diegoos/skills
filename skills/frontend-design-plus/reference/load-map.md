# Load map

Open this file from [after-briefing.md](after-briefing.md) after the Briefing card exists, to attach paths to a slot in [dispatch.md](dispatch.md). If briefing answers do not exist and the form was not skipped, close this file and open [briefing.md](briefing.md). Greenfield marketing Scene still blank: same.

Attach only the rows that match this run **and** this slot. A row that does not match stays closed. The parent attaches paths; it does not open Direction, Implement, or QA bodies except on [isolated component](after-briefing.md#isolated-component).

## Parent

Open [after-briefing.md](after-briefing.md) and [dispatch.md](dispatch.md). Stay closed: [composition.md](composition.md), [design-styles.md](design-styles.md), `design-styles/*.md`, [anti-slop.md](anti-slop.md), [crit.md](crit.md), [preflight-checklist.md](preflight-checklist.md), [implement.md](implement.md), [product-register.md](product-register.md), [ux-principles.md](ux-principles.md), [layout-patterns.md](layout-patterns.md). Isolated component is the exception: [implement.md](implement.md) plus Component rows below, then pre-flight A.

## Direction

| Origin | Attach | Stay closed |
| --- | --- | --- |
| `greenfield` | — | [redesign.md](redesign.md) |
| `redesign` | [redesign.md](redesign.md) | [design-styles.md](design-styles.md), `design-styles/*.md` |
| `polish` | [redesign.md](redesign.md) craft audit | [design-styles.md](design-styles.md), `design-styles/*.md`, [composition.md](composition.md), [layout-patterns.md](layout-patterns.md) |

| Task | Attach | Stay closed |
| --- | --- | --- |
| **Component** | skip this slot | — |
| **App UI** | [design-md.md](design-md.md), [product-register.md](product-register.md) | [layout-patterns.md](layout-patterns.md), [assets.md](assets.md), [composition.md](composition.md), [ux-principles.md](ux-principles.md), [design-styles.md](design-styles.md), `design-styles/*.md` unless Look is a named catalog `id` |
| **Marketing** | [design-md.md](design-md.md), [brand-register.md](brand-register.md). Greenfield or redesign: [composition.md](composition.md) | [product-register.md](product-register.md), [ux-principles.md](ux-principles.md), [layout-patterns.md](layout-patterns.md) |

| Signal | Attach | Stay closed |
| --- | --- | --- |
| Greenfield **marketing** Look is a catalog `id` | that one `design-styles/<id>.md` | the rest of `design-styles/` |
| Greenfield **marketing** Look is `you-decide` / `none` (including unnamed), or invent-all on marketing | [design-styles.md](design-styles.md) Pick, then one `design-styles/<id>.md` when Pick is not `none` | the rest of `design-styles/` |
| App UI Look is a named catalog `id` | that one `design-styles/<id>.md` (craft blanks only; layout stays [product-register.md](product-register.md)) | the rest of `design-styles/` |
| App UI Look is skipped / `none` | — | [design-styles.md](design-styles.md), `design-styles/*.md` |
| App UI or marketing (palette in play) | [color.md](color.md) | — |
| Parent re-dispatch for invalid Lock | [design-read-examples.md](design-read-examples.md) | — |
| Type pairing still blank after the style file and DESIGN.md | [typography.md](typography.md) | — |
| Density-band recipe is not already in DESIGN.md **Layout** | [design-systems.md](design-systems.md) | — |

Stay closed on Direction: [implement.md](implement.md), [anti-slop.md](anti-slop.md), [crit.md](crit.md), [preflight-checklist.md](preflight-checklist.md), [file-architecture.md](file-architecture.md), [surfaces.md](surfaces.md), [production-engineering.md](production-engineering.md), [motion.md](motion.md), [assets.md](assets.md), [layout-patterns.md](layout-patterns.md), [design-read-examples.md](design-read-examples.md) unless the parent named an invalid Lock.

## Implement

Always attach [implement.md](implement.md) and DESIGN.md (path in the Packet).

| Origin / task | Attach | Stay closed |
| --- | --- | --- |
| `greenfield` (not isolated component) | [file-architecture.md](file-architecture.md) | — |
| `redesign` or `polish` | [redesign.md](redesign.md) | [file-architecture.md](file-architecture.md) |
| **Component** (parent in-process) | [production-engineering.md](production-engineering.md), [file-architecture.md](file-architecture.md) when greenfield. [design-md.md](design-md.md) when `DESIGN.md` exists or the component introduces tokens | [brand-register.md](brand-register.md), [layout-patterns.md](layout-patterns.md), [product-register.md](product-register.md), [composition.md](composition.md), [assets.md](assets.md) unless the user asked for a visual restyle |
| **App UI** | [surfaces.md](surfaces.md), [production-engineering.md](production-engineering.md), [motion.md](motion.md) Product micro | [layout-patterns.md](layout-patterns.md), [composition.md](composition.md), [design-styles.md](design-styles.md) |
| **Marketing** | [layout-patterns.md](layout-patterns.md#frame-tracks) | [product-register.md](product-register.md), [ux-principles.md](ux-principles.md). [production-engineering.md](production-engineering.md) unless the surface has forms or async. [layout-patterns.md](layout-patterns.md#first-three-folds) stays closed until Implement has `tracks=` and a leftover *object* has no obvious form |

| Signal | Attach | Stay closed |
| --- | --- | --- |
| Packet `style_path` is not `none` | that one `design-styles/<id>.md` | the rest of `design-styles/`, [design-styles.md](design-styles.md) |
| Behave or Lock `fluid` / `cinematic` | [motion.md](motion.md) | — |
| Behave `still` / `none` on **marketing** | — | [motion.md](motion.md) |
| Constraints or Look name photo, video, or illustration | [assets.md](assets.md) | — |
| No media named | — | [assets.md](assets.md) |
| Palette or theme in play | [color.md](color.md) | — |
| Lock names a nested enclosure, hairline, or island CTA | [material-craft.md](material-craft.md) | — |
| LCP/CLS, hero media, or layout shift is in scope | [performance.md](performance.md) | — |
| Type pairing still blank | [typography.md](typography.md) | — |
| Density-band recipe missing from DESIGN.md **Layout** | [design-systems.md](design-systems.md) | — |
| App UI Packet *job* asks a chart or BI question | [ux-principles.md](ux-principles.md#dashboards-and-data-ui) | — |
| App UI Packet *job* has no chart | — | [ux-principles.md](ux-principles.md) |

Stay closed on Implement: [briefing.md](briefing.md), [composition.md](composition.md), [design-styles.md](design-styles.md) (the Catalog), [anti-slop.md](anti-slop.md), [crit.md](crit.md), [preflight-checklist.md](preflight-checklist.md).

## QA

| When | Attach |
| --- | --- |
| After markup, before calling the surface done | [anti-slop.md](anti-slop.md), [crit.md](crit.md) |
| After the written *crit* | [preflight-checklist.md](preflight-checklist.md) (tier from [task routing](../SKILL.md#task-routing)) |

Stay closed on QA: [composition.md](composition.md), [design-styles.md](design-styles.md), [implement.md](implement.md), [briefing.md](briefing.md). Use the Packet for briefing facts.

Done when every matching row for the current slot is in that slot's prompt and every non-matching file stayed closed.
