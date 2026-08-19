# Frontend Design Plus

Tells an agent how to ship working web UI: landings, dashboards, components, posters, HTML/CSS layouts. Skip backend, SQL, CI, or docs-only work.

The agent follows [`SKILL.md`](SKILL.md). Briefing, Lock, load map, crit, and pre-flight live in [`reference/`](reference/).

## What it is for

On a landing or campaign, design is the product. The visitor's first impression is the deliverable.

On a dashboard or settings screen, the interface should disappear into the task. Familiar chrome, one primary action, the project's tokens.

The output is code. Touch targets, contrast, and real copy are part of done.

## How it works

Classify names the surface (component, app UI, or marketing) and the origin from a disk glance: `greenfield`, `redesign`, or `polish`.

Unless the user said invent-all, each remaining blank is one `AskQuestion` call. After answers: follow or write `DESIGN.md`, then a Design Read and a Lock, then markup. A written *crit* and a DOM pre-flight close the pass.

Greenfield marketing can pick a named style from the catalog. App UI skips that catalog and uses the [product register](reference/product-register.md). Both themes means two modes and a switch in the chrome ([color.md](reference/color.md#system-theme)). Unnamed hue: the agent asks Palette before picking hex.

Ask for a landing, a settings page, or a restyle, or invoke `/frontend-design-plus`. Put this folder in whatever directory your harness uses for skills.

## Sources

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
- [Design Prompts](https://www.designprompts.dev/): sample systems the style guides distill. Hex and typefaces in those samples are fallbacks when the user left color and type blank.
