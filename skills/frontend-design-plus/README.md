# Frontend Design Plus

The agent ships working web UI: landings, dashboards, components, posters, HTML/CSS.

Follow [`SKILL.md`](SKILL.md). Briefing, polish, dispatch, load map, Lock, crit, rubric, verification, and pre-flight live in [`reference/`](reference/). Public terms are in [`SKILL.md`](SKILL.md#words): Job, Success, Origin, Mode, Lock, Packet, Occupancy, Sketch, Token, Slot, Recipe, Verification.

## What it is for

Marketing treats design as the product. On a loose prompt the agent infers how this domain's layout should behave, names the category cliché to refuse, and asks one A/B occupancy: two first-viewport massings and two Success verbs. If Look is still unnamed, it asks whether you want a catalog style. Yes prints [catalog.md](reference/catalog.md) and you pick an id. No locks `style=none`; Direction crafts from the enter object. An `id` or Item already in the prompt skips that question. Direction then lists domain objects, cuts to P0, groups what shares a rectangle, and writes a Sketch. The Sketch footer is occupancy for the rest of the run. How original the first-viewport split is stays the model's job, not a Packet gate.

App UI (dashboard, CMS, CRM, settings) should recede into the task. Job, domain objects, P0, then one Recipe (`queue-home`, `list-filter`, `editor`, `accounts`). Skip occupancy A/B. A poster is the wrong deliverable.

Redesign asks Aim, Keep, and Scope, then recomposes from disk. Polish keeps the look: [polish.md](reference/polish.md) writes a craft audit and patches in the same window. It does not open briefing, catalog, or composition.

## How it works

Classify names component, app UI, or marketing, and origin from a disk glance: `greenfield`, `redesign`, or `polish`.

`origin=polish` sets `mode=fast`. Mute polish asks one Focus question, then audits and patches. Stay-closed files: [load-map.md](reference/load-map.md#polish).

Greenfield marketing with a Job: infer domain behavior and the cliché to refuse, then A/B, then Style if Look is blank. No Job: ask Job only. invent-all skips the form; Direction writes one Sketch. Unnamed Behave and Constraints are `none`. Mode is three lines in [`SKILL.md`](SKILL.md). `fast` on greenfield/redesign keeps slot order; extra stay-closed files are in [load-map.md](reference/load-map.md#fast). Open [execution-modes.md](reference/execution-modes.md) at dispatch.

After answers (not polish), the parent packs a Briefing card and runs Direction, Implement, and QA ([dispatch.md](reference/dispatch.md)). The Packet starts with Intent, Layout, and Tokens. Marketing Direction: Job → objects → first-viewport masses → Sketch → `folds=`, then brand-register. App UI Direction: Job → objects → P0 → `recipe=`. Implement markup from the layout kit (full Packet + DESIGN.md + Implement rows); `tracks=` and `scale=` before folds; CTA is Success; app UI returns `main=` / `proof=`. QA covers the category cliché, generic CTA ([anti-slop.md](reference/anti-slop.md)), copy divide, crit Q1, rubric, verification, and pre-flight. The parent checks Packet presence and Sketch/Inventory overlap. Occupancy grammar stays in Direction. `solo` closes each slot's files before the next; the Packet is the only carry.

`folds=` is the page map. A two-fold page is complete.

App UI uses the [product register](reference/product-register.md). Theme `system` is two palettes and a chrome switch ([color.md](reference/color.md#system-theme)). Unnamed hue: craft from the object after Frame, not navy-for-law or indigo-for-SaaS.

## How it runs

| Slot | Who | Reads | Returns |
| --- | --- | --- | --- |
| Parent | Classify + character inference, then A/B (or Job if empty), then Style if Look is unnamed | `SKILL.md`, [briefing.md](reference/briefing.md) (opens [product-context.md](reference/product-context.md) when scoring Job/Audience/Constraints). After the card: [after-briefing.md](reference/after-briefing.md), [dispatch.md](reference/dispatch.md), [load-map.md](reference/load-map.md), [execution-modes.md](reference/execution-modes.md) | Briefing card; prints Design Read + Lock; checks Packet presence and Sketch/Inventory overlap; resumes Implement with P0s. Keeps return blocks, not worker walks |
| Direction | Child (in-process only if no child tool) | Marketing: [composition.md](reference/composition.md) first, then [brand-register.md](reference/brand-register.md) after Frame, [design-md.md](reference/design-md.md), one style file when Look named an id, [visual-language.md](reference/visual-language.md) only when `style=custom`. App UI: [product-register.md](reference/product-register.md), [design-md.md](reference/design-md.md). See [load-map.md](reference/load-map.md) | Packet with Sketch (marketing greenfield/redesign) + DESIGN.md on disk |
| Implement | Fresh child | Layout kit: full Packet, DESIGN.md, [implement.md](reference/implement.md), marketing: [layout-patterns.md](reference/layout-patterns.md); app UI: [surfaces.md](reference/surfaces.md) + [product-register.md](reference/product-register.md) for the named recipe | Markup on disk; marketing greenfield/redesign also `See:` / `tracks=` / `scale=` / `proof=` / `distinct=` / `cta=`; app UI also `main=` / `proof=` |
| QA | Sequential after markup | [anti-slop.md](reference/anti-slop.md), [crit.md](reference/crit.md), [visual-rubric.md](reference/visual-rubric.md), [quality-cases.md](reference/quality-cases.md), [verification.md](reference/verification.md), [preflight-checklist.md](reference/preflight-checklist.md); marketing greenfield/redesign also [performance.md](reference/performance.md) | Triad + rubric + verification + P0/P1 table; no edits |

Isolated component skips the dispatch table. [after-briefing.md](reference/after-briefing.md#isolated-component) runs Implement, anti-slop Always, Tier A, verification, and the rubric with Structural and Domain skipped. Polish marketing or app UI skips dispatch the same way ([polish.md](reference/polish.md)): craft audit, Implement, Tier A, no crit. Closed files for the parent: [load-map.md](reference/load-map.md#parent). Worker and window selection comes from [execution-modes.md](reference/execution-modes.md), opened at dispatch.

Ask for a landing, a settings page, a restyle, or a polish pass. The harness may invoke this skill on those intents. Put this folder in whatever directory your harness uses for skills.

## Non-goals

This skill does not ship a CLI anti-pattern detector, live browser variant picker, hooks, or 23 named slash commands. Use [Impeccable](https://github.com/pbakaus/impeccable) if you want that product layer. It does not match a product type to a landing template or an industry palette. That matcher is [UI UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill). Occupancy still comes from the Job and the A/B pick, not from a category look.

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
- [The age of creative agents (Adobe)](https://blog.adobe.com/en/publish/2026/04/15/the-age-of-creative-agents-rise-creative-director): human as creative director; one A/B direction instead of silent invention.
