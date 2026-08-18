# Load map

Open this file from [after-briefing.md](after-briefing.md). If briefing answers do not exist and the form was not skipped, close this file and open [briefing.md](briefing.md).

Load only the rows that match this run. A row that does not match stays closed.

## By origin

| Origin       | Open                       | Stay closed                                                |
| ------------ | -------------------------- | ---------------------------------------------------------- |
| `greenfield` | —                          | [redesign.md](redesign.md)                                 |
| `redesign`   | [redesign.md](redesign.md) | [design-styles.md](design-styles.md), `design-styles/*.md` |
| `polish`     | [redesign.md](redesign.md) | [design-styles.md](design-styles.md), `design-styles/*.md` |

## By task type

| Task          | Open                                                                                                                                                                                                                                            | Stay closed                                                                                                                                                                                     |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Component** | [production-engineering.md](production-engineering.md), [file-architecture.md](file-architecture.md) when origin is greenfield. [design-md.md](design-md.md) when `DESIGN.md` exists or the component introduces tokens.                        | [brand-register.md](brand-register.md), [layout-patterns.md](layout-patterns.md), [product-register.md](product-register.md), [assets.md](assets.md) unless the user asked for a visual restyle |
| **App UI**    | [design-md.md](design-md.md), [product-register.md](product-register.md), [ux-principles.md](ux-principles.md), [production-engineering.md](production-engineering.md). [file-architecture.md](file-architecture.md) when origin is greenfield. | [layout-patterns.md](layout-patterns.md), [assets.md](assets.md)                                                                                                                                |
| **Marketing** | [design-md.md](design-md.md), [brand-register.md](brand-register.md), [layout-patterns.md](layout-patterns.md). [file-architecture.md](file-architecture.md) when origin is greenfield.                                                         | [product-register.md](product-register.md), [ux-principles.md](ux-principles.md). [production-engineering.md](production-engineering.md) unless the surface has forms or async                  |

## From briefing answers

| Signal                                                  | Open                                                                                     | Stay closed                  |
| ------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------- |
| Behave or Lock `fluid` / `cinematic`                    | [motion.md](motion.md)                                                                   | —                            |
| Behave `still` / `none`                                 | —                                                                                        | [motion.md](motion.md)       |
| Constraints or Look name photo, video, or illustration  | [assets.md](assets.md)                                                                   | —                            |
| No media named                                          | —                                                                                        | [assets.md](assets.md)       |
| Greenfield Look is a catalog `id`                       | that one `design-styles/<id>.md` at Direction                                            | the rest of `design-styles/` |
| Greenfield Look is `you-decide` / `none`, or invent-all | [design-styles.md](design-styles.md) Pick, then one `design-styles/<id>.md` at Direction | the rest of `design-styles/` |
| App UI or marketing (palette in play)                   | [color.md](color.md) at Declare                                                          | —                            |

## After Lock

| Signal                                                 | Open                                               |
| ------------------------------------------------------ | -------------------------------------------------- |
| Lock names a nested enclosure, hairline, or island CTA | [material-craft.md](material-craft.md)             |
| Lock shape is unclear                                  | [design-read-examples.md](design-read-examples.md) |

## After markup

| When                            | Open                                                                                                  |
| ------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Before calling the surface done | [anti-slop.md](anti-slop.md), [crit.md](crit.md)                                                      |
| After *crit*                    | [preflight-checklist.md](preflight-checklist.md) (tier from [task routing](../SKILL.md#task-routing)) |

## On demand (never at Classify)

| File                                   | Open when                                                   |
| -------------------------------------- | ----------------------------------------------------------- |
| [typography.md](typography.md)         | Type pairing still blank after the style file and DESIGN.md |
| [performance.md](performance.md)       | LCP/CLS, hero media, or layout shift is in scope            |
| [design-systems.md](design-systems.md) | Density-band recipe is not already in DESIGN.md **Layout**  |

Done when every matching row is in context and every non-matching file stayed closed.
