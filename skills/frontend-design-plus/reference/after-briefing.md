# After briefing

Open this file when every briefing field has an owner (quoted user string, disk evidence, you-decide on Look, or invent-all), or when the form was skipped (*invent-all*, or polish with no blanks). If a blank remains, open [briefing.md](briefing.md) instead.

## Pace

- **Load.** Open [load-map.md](load-map.md) and only the files it assigns.
- **One intent per lookup.** Open the one owning file; retry once narrower; if still empty, follow the [priority table](#priority-order) and say the fallback is the table.
- **One surface per pass.** Finish *crit* + that surface's pre-flight before the next page or variant.
- **Pause on reflex.** Centered hero, three equal cards, purple gradient, or four equal KPI cards with Welcome back: return to direction ([anti-slop.md](anti-slop.md)). A component kit is a *code floor*; theme, type, radius, and copy come from DESIGN.md.
- **Slop test then crit.** After markup, [anti-slop.md](anti-slop.md) and [crit.md](crit.md) before calling the surface done. Question 1 = yes, or a logo-swap that still reads, blocks pre-flight.

## Workflow

1. **Headlines.** Marketing: write the H1 and the primary CTA as sentences in the briefing voice **before** choosing a layout family. If either sentence could sit on a CRM, a bank, and a dentist, rewrite it. App UI: write three operator questions this view answers in ten seconds, then the primary-action sentence ([product-register.md](product-register.md#dashboards)). A feature list is not a composition. Keep those sentences for Direction.
2. **Load.** Open [load-map.md](load-map.md). Load only assigned files. Done when each assigned file is in context and every non-matching file stayed closed.
3. **DESIGN.md.** Follow the file if present; otherwise write it to the spec before markup ([design-md.md](design-md.md)). **Layout** names grid, gutter, occupancy, type-scale jump, radius set, and motion recipe. Later surfaces reconcile to this file; a missing `primary` is a gap, not a new accent. Copy `name=` from the briefing into front matter. Done when `name` matches the briefing and tokens are the palette the CSS will use.
4. **Declare.** Design Read + Lock on app UI and marketing. Color strategy when palette or theme is in play ([color.md](color.md#color-strategies)). Map **Name** onto `name=`, **Stack** onto `stack=`, **Use** onto `density=` (hours of expert work → `dense`; minutes per month → `airy`), **Behave** onto `motion=` (`none`/`still` → `still`; hover/scroll → `fluid`; cinematic named → `cinematic`), **Theme** onto `theme=` (`light` / `dark` / `system`), and **Look** onto `style=` ([briefing.md](briefing.md#look)). Done when briefing has owners and both lines exist. No markup before that.
5. **Direction.** Greenfield **marketing**: pick one style `id` ([design-styles.md](design-styles.md)); load that one file. If Look was `you-decide` or invent-all skipped the form, write a 2–3 sentence **Pick** that names which **When** matched which fields; refuse the median cluster and the category default. Refs that span two ids: pick the closer When and say which ref lost. The file is a craft *path* (type, color, material, motion, density). Commit one spatial system and one loud numeric contrast from that file ([design-styles.md](design-styles.md#commit)). App UI, redesign, and polish: Lock `style=none`; follow DESIGN.md, tokens, and current CSS; leave the Catalog closed. App UI layout families from the briefing headlines, DESIGN.md, and [product-register.md](product-register.md). Marketing layout families from the briefing headlines, DESIGN.md, and [layout-patterns.md](layout-patterns.md). Polish keeps the current family. Marketing Lock names one material or spatial break. App UI Lock names the 1–2 Pareto screens. Done when `style=<id|none>` and those names are in the Lock.
6. **Implement.** Greenfield: write files per [file-architecture.md](file-architecture.md). Redesign and polish: patch the existing files on the current stack (scan → diagnose → fix in [redesign.md](redesign.md)); keep functionality. Polish stops at craft levers 1–5. Reuse the project design system when it exists: the kit is a code floor; wrap it with DESIGN.md tokens. Map CSS variables to DESIGN.md tokens. During this step, walk the [priority table](#priority-order). Done when greenfield-with-no-framework has `index.html`, `main.css`, and `main.js` on disk, HTML has no stylesheet dump, and the first viewport matches the Lock: marketing matches `style=` and Look; app UI matches Pareto screens, [product-register.md](product-register.md#dashboards), and [surfaces.md](surfaces.md); Lock `theme=system` matches [color.md](color.md#system-theme).
7. **Crit.** Frame from the briefing, then a silent written triad with no edits, then rank and fix ([crit.md](crit.md)). Done when question 1 is no (or the brief named that scaffold, or polish kept the disk scaffold), the first viewport fails a logo-swap, P0 is fixed, and the alternative is a layout family in the DOM (greenfield/redesign) or in-place craft (polish) or rejected with a user-goal reason. Praise does not ship.
8. **Pre-flight.** Run the matching tier in [preflight-checklist.md](preflight-checklist.md). Tiers B and C pass as DOM counts. Tab interactive elements. State what was not verified. Done when every applicable box is checked or failed and fixed.

**Design Read** (one sentence):

> Reading this as: \<page kind> for \<audience>, with a \<vibe> language, leaning toward \<register or design system>.

**Lock** (next line):

> Lock: origin=\<greenfield|redesign|polish>; name=\<briefing name or invented>; scene=\<place/time/mood>; style=\<id|none>; theme=\<light|dark|system>; color=\<restrained|committed|full|drenched>; layout=\<contained|offset|wild>; motion=\<still|fluid|cinematic>; density=\<airy|regular|dense>; stack=\<detected, asked, or html+css+js>.

Quiet constraints (a11y-first, regulated, public-sector, kids) override Lock bands. Each dial must change spacing, layout family, or motion recipe. A Lock that only labels fails Declare. Redesign, polish, and app UI lock `style=none` unless Look is a named catalog `id`. Density-band and Lock-band recipes load at Load ([load-map.md](load-map.md)). Constraints that include a voice sample own the headline register; otherwise write headlines from Job + Success in plain register. Use the briefing name in the wordmark and document title. Invent-all: Lock `name=invented`; name from the job as a descriptive noun (`Invoice desk`, `API uptime`), never a coined startup or handle (`Nexus`, `Cloudly`, `swe-13`).

Product chrome stays consistent. If the Lock shape is unclear: [design-read-examples.md](design-read-examples.md).

## Priority order

During Implement and Crit, work top-down. Pre-flight is the ship gate; this table is work order. Open the owner file when that row is in play.

| #   | Focus      | Check                                                                       | Anti-pattern                                                       | Owner                                                                                                              |
| --- | ---------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| 1   | A11y       | Contrast 4.5:1, visible focus, keyboard                                     | Removing focus rings                                               | [preflight A](preflight-checklist.md)                                                                              |
| 2   | Touch      | Targets ≥44px, 8px gap, press feedback                                      | Hover-only actions                                                 | [production-engineering.md](production-engineering.md)                                                             |
| 3   | Perf       | LCP/CLS, reserved space                                                     | Layout shift                                                       | [performance.md](performance.md)                                                                                   |
| 4   | Direction  | Briefing answers + DESIGN.md + Read + Lock                                  | Invented name; markup before answers or Lock                       | [briefing.md](briefing.md), [design-md.md](design-md.md)                                                           |
| 5   | Layout     | Mobile-first; N items → N cells at 768; app UI chrome stays inside the rail | Empty tracks; control overflowing the sidebar                      | [layout-patterns.md](layout-patterns.md) / [product-register.md](product-register.md) / [surfaces.md](surfaces.md) |
| 6   | Type/color | Named strategy, tokens                                                      | Raw hex, gray-on-gray                                              | [color.md](color.md), [typography.md](typography.md)                                                               |
| 7   | Motion     | Recipe matches the Lock band                                                | One duration for everything                                        | [motion.md](motion.md)                                                                                             |
| 8   | Forms      | Labels; field-group grid; error keeps row                                   | Independent columns; error staggers next row; placeholder-as-label | [production-engineering.md](production-engineering.md#forms)                                                       |
| 9   | Nav        | Predictable back, one primary per view                                      | Overloaded chrome                                                  | [ux-principles.md](ux-principles.md)                                                                               |
| 10  | Data       | Chart matches the question                                                  | Chart gallery, color-only encoding                                 | [ux-principles.md](ux-principles.md#dashboards-and-data-ui)                                                        |

## Production baseline

| Requirement       | Minimum                                                                                                |
| ----------------- | ------------------------------------------------------------------------------------------------------ |
| **States**        | Default, hover, focus, active, disabled; loading, error, empty when async                              |
| **Accessibility** | Semantic HTML, labels, keyboard nav, visible focus, WCAG 2.2 AA contrast                               |
| **Responsive**    | Mobile-first; touch targets ≥44px with ≥8px gap; no horizontal overflow on 320px; viewport allows zoom |
| **Design system** | Reuse project tokens, `DESIGN.md`, and components                                                      |
| **Files**         | Markup, styles, and behavior in the project's (or default) split; CSS tokens match DESIGN.md           |

Patterns: [production-engineering.md](production-engineering.md) at Load when the map assigns it.
