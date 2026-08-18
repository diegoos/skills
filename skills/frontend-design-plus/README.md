# Frontend Design Plus

Tells an agent how to ship working web UI: landings, dashboards, components, posters, HTML/CSS layouts. Skip backend, SQL, CI, or docs-only work.

The agent follows [`SKILL.md`](SKILL.md). After Classify it opens [`briefing.md`](reference/briefing.md) before scoring fields and asks each blank with `AskQuestion`. After answers, [`after-briefing.md`](reference/after-briefing.md) owns Design Read, Lock, and markup. Extra rules in [`reference/`](reference/) load then, only for the origin, task type, and answers of that run.

## What it is for

On a landing or campaign, design is the product. The visitor's first impression is the deliverable.

On a dashboard or settings screen, the interface should disappear into the task. Familiar chrome, one primary action, the project's tokens.

The output is code. Touch targets, contrast, and real copy are part of done.

## How it works

The agent names the surface (component, app UI, or marketing) and the origin from a disk glance: `greenfield` (new UI), `redesign` (existing UI from the user briefing), or `polish` (improve existing UI). Classify fills type and origin only.

Unless the user said invent-all, each remaining blank is one `AskQuestion` call (name, audience, success, use, look, behave, stack when the repo has none). A bio or "unique" does not skip the form. Options come from the prompt; Other is a typed answer. Greenfield Look blank: it prints the [style catalog](reference/design-styles.md) as a table, then asks four styles that fit the job plus a specify option. `you-decide` matches the briefing to one catalog When and skips the median cluster (`saas`, `enterprise`, `modern-dark`, and the other trap ids). Redesign and polish follow DESIGN.md, tokens, and current CSS; they leave the catalog closed and lock `style=none`. It invents no product name. A prompt that already named Audience, Look, and Success skips leftover blanks only.

It follows `DESIGN.md` when the repo has one, or writes one to the [DESIGN.md spec](https://github.com/google-labs-code/design.md/blob/main/docs/spec.md) before markup. CSS tokens map to that file.

Before markup it writes the H1 and primary CTA, then a one-line Design Read and a Lock: origin, name, scene, style id, color strategy, layout, motion, density, stack. Greenfield style is a craft path; layout still comes from the briefing and the layout refs. Greenfield with no stack uses `index.html`, `main.css`, and `main.js` unless the user picked a framework.

A new UI gets new files on that split. Redesign and polish patch what is already there, on the current stack, after a short audit. Polish stops at craft (spacing, contrast, states, deletion); redesign may recompose from the briefing. A component kit is a code floor: theme and type come from DESIGN.md.

It finishes with a written *crit* (common AI layout, logo-swap, one alternative layout family), then by counting things in the DOM (pre-flight A always, B on marketing, C on app UI) and by checking layout and copy against [`anti-slop.md`](reference/anti-slop.md). The first viewport has to match that Lock and Look.

Ask for a landing, a settings page, or a restyle, or invoke `/frontend-design-plus`. Put this folder in whatever directory your harness uses for skills.

## Sources

- [DESIGN.md Format spec](https://github.com/google-labs-code/design.md/blob/main/docs/spec.md): token YAML, section order, follow-or-generate.
- [UX-Context Design (NN/G)](https://www.nngroup.com/articles/ux-context-design/): visual identity as in-repo context; constraints and glossary, not personas; use-context steers density.
- [Context Architecture](https://context-architecture.dev/): bind stack, files, and tokens to something that fails when they drift; *cold reader*; disk wins.
- [How we do design critiques at Figma](https://www.figma.com/blog/design-critiques-at-figma/): frame *looking for / not*; silent pass before edits.
- [How to Run a UX Design Critique (UX Tigers)](https://www.uxtigers.com/post/design-crit): frame, silent written crit, prioritize, fix; user problem, not widget recipe.
- [Top 10 UI trends (IxDF)](https://ixdf.org/literature/article/top-10-ui-trends-every-designer-should-know): named style as craft path; Flat 2.0; neumorphism contrast; motion that guides.
- [50 Design Styles (UX Planet)](https://uxplanet.org/50-design-styles-every-designer-should-know-for-better-prompting-56c09d55db62): Look and Direction vocabulary; core elements without locking layout.
- [Design Prompts](https://www.designprompts.dev/): sample systems the style guides distill. Hex and typefaces in those samples are fallbacks when the user left color and type blank.
