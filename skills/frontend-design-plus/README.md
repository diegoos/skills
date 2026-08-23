# Frontend Design Plus

This skill tells an agent how to ship working web UI: landings, dashboards, components, posters, HTML/CSS layouts.

The agent follows [`SKILL.md`](SKILL.md). Briefing, dispatch, load map, Lock, crit, visual rubric, verification, and pre-flight live in [`reference/`](reference/).

## What it is for

On a landing or campaign, design is the product. The first impression is what you ship. Marketing composes from the *job*: greenfield asks **Scene** (first-viewport occupancy, or `you-decide` from the brief), then Direction writes *objects*, P0, *kinship*, three occupancy cards with distinct *joins*, a *frame*, and a Sketch. `object-swap=` is required when Inventory has two or more domain nouns; otherwise it is `n/a` (do not invent a thesis). A named style vests craft only when *tension* requires it; a supported custom register may use `style=custom` when the catalog would become costume.

On a dashboard, CMS, CRM, or settings screen, the interface should disappear into the task. *Job* phrase, domain *objects*, and P0, then one named product recipe (`queue-home`, `list-filter`, `editor`, `accounts`) so the operator can scan and persist. A unique poster would be the wrong deliverable.

Redesign asks Aim, Keep, and Scope, then recomposes from what is already on disk. Polish writes a craft audit (spacing, type, color, states) and closes those P0/P1 items. It does not pick a new look.

## How it works

Classify names the surface (component, app UI, or marketing) and the origin from a disk glance: `greenfield`, `redesign`, or `polish`.

The parent scores every briefing field against the prompt and disk in one pass. Remaining blanks go out in one structured question call when the host tool accepts multiple questions. If the tool accepts only one question per call, the agent asks one field per turn and records `questions=serial`. **Use** is still asked because it sets density. Unnamed **Behave** and **Constraints** are `none` unless the prompt already named motion, states, or artifacts. Redesign starts with Aim, Keep, and Scope. Polish skips the form unless the goal is mute. Mode choice is three lines in [`SKILL.md`](SKILL.md). Capability fallbacks live in [execution-modes.md](reference/execution-modes.md) and open at dispatch, not at Classify.

After answers the parent packs a Briefing card and runs three sequential slots ([dispatch.md](reference/dispatch.md)): **Direction** (marketing: *job* → *objects* → *kinship* → *frame* → Sketch → `folds=`; app UI: *job* → *objects* → P0 → `recipe=`), then DESIGN.md + Lock, **Implement** (markup from the Packet Sketch; `tracks=` before folds; app UI returns `main=` / `proof=`), **QA** (anti-slop, written *crit* Q1, visual rubric, verification, and DOM pre-flight). The selected execution mode decides whether slots are handed to workers or run in one window. In `solo`, each slot closes its files before the next; the Packet is the only carry.

`you-decide` and invent-all stay. Direction derives occupancy from *objects* and *kinship* (`fallback=yes` only when labeled). On unnamed Look it records `first-join=`, refuses to ship that first join, then Picks: a catalog `id` only when *tension* matches a When; otherwise `style=custom` or `style=none`. The catalog is not the default marketing look.

Greenfield marketing can still use a named style when *tension* matches a When. Silence on Look is `you-decide`. To lock a look, name the catalog `id` or Item number in the prompt ([design-styles.md](reference/design-styles.md#catalog)). App UI skips that catalog and uses the [product register](reference/product-register.md). Both themes mean two modes and a switch in the chrome ([color.md](reference/color.md#system-theme)). Unnamed hue: the agent asks Palette before picking hex.

## How it runs

| Slot | Who | Reads | Returns |
| --- | --- | --- | --- |
| Parent | Classify + one-pass briefing score, then one structured question call (or serial fallback) | `SKILL.md`, [briefing.md](reference/briefing.md). After the card: [after-briefing.md](reference/after-briefing.md), [dispatch.md](reference/dispatch.md), [load-map.md](reference/load-map.md), [execution-modes.md](reference/execution-modes.md) | Briefing card; prints Design Read + Lock; resumes Implement with P0s |
| Direction | Child (in-process only if no child tool) | Marketing: [composition.md](reference/composition.md), [design-md.md](reference/design-md.md), one style file. App UI: [product-register.md](reference/product-register.md), [design-md.md](reference/design-md.md). See [load-map.md](reference/load-map.md) | Packet with Sketch (marketing greenfield/redesign) + DESIGN.md on disk |
| Implement | Fresh child | [implement.md](reference/implement.md), Packet, DESIGN.md, marketing: [layout-patterns.md](reference/layout-patterns.md#frame-tracks); app UI: [surfaces.md](reference/surfaces.md) | Markup on disk; marketing greenfield/redesign also `See:` / `tracks=` / `proof=` / `distinct=`; app UI also `main=` / `proof=` |
| QA | Sequential after markup | [anti-slop.md](reference/anti-slop.md), [crit.md](reference/crit.md), [visual-rubric.md](reference/visual-rubric.md), [verification.md](reference/verification.md), [preflight-checklist.md](reference/preflight-checklist.md) | Triad + rubric + verification + P0/P1 table; no edits |

Isolated component skips Direction dispatch but still runs Implement, Tier A, the rubric where applicable, and verification. The parent does not open composition, the Catalog, anti-slop, crit, visual-rubric, verification, or pre-flight on marketing or app UI; those references stay in their slots. Worker and window selection comes from [execution-modes.md](reference/execution-modes.md), opened at dispatch.

Ask for a landing, a settings page, or a restyle, or invoke `/frontend-design-plus`. Put this folder in whatever directory your harness uses for skills.

## References

- [DESIGN.md Format spec](https://github.com/google-labs-code/design.md/blob/main/docs/spec.md): token YAML, section order, follow-or-generate.
- [UX-Context Design (NN/G)](https://www.nngroup.com/articles/ux-context-design/): visual identity as in-repo context; constraints and glossary, not personas; use-context steers density.
- [Context Architecture](https://context-architecture.dev/): bind stack, files, and tokens to something that fails when they drift; *cold reader*; disk wins.
- [How we do design critiques at Figma](https://www.figma.com/blog/design-critiques-at-figma/): frame *looking for / not*; silent pass before edits.
- [How to Run a UX Design Critique (UX Tigers)](https://www.uxtigers.com/post/design-crit): frame, silent written crit, prioritize, fix; user problem, not widget recipe.
- [Top 10 UI trends (IxDF)](https://ixdf.org/literature/article/top-10-ui-trends-every-designer-should-know): named style as craft path; Flat 2.0; neumorphism contrast; motion that guides.
- [50 Design Styles (UX Planet)](https://uxplanet.org/50-design-styles-every-designer-should-know-for-better-prompting-56c09d55db62): Look and Direction vocabulary; core elements without locking layout.
- [Dashboard Design UX Patterns (Pencil & Paper)](https://www.pencilandpaper.io/articles/ux-pattern-analysis-data-dashboards): app UI as a decision tool; work queue over chart gallery.
- [Effective Dashboard Design (DataCamp)](https://www.datacamp.com/tutorial/dashboard-design-tutorial): inverted pyramid; chart from a question; KPI needs comparison and time.
- [Details that make interfaces feel better](https://github.com/jakubkrehel/make-interfaces-feel-better): app UI chrome containment, concentric radius, tabular numbers, interruptible product micro.
