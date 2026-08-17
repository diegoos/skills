# Frontend Design Plus

Tells an agent how to ship working web UI: landings, dashboards, components, posters, HTML/CSS layouts. Skip backend, SQL, CI, or docs-only work.

The agent follows [`SKILL.md`](SKILL.md). Extra rules live in [`reference/`](reference/) and load only for the kind of surface being built.

## What it is for

On a landing or campaign, design is the product. The visitor's first impression is the deliverable.

On a dashboard or settings screen, the interface should disappear into the task. Familiar chrome, one primary action, the project's tokens.

The output is code. Touch targets, contrast, and real copy are part of done.

## How it works

The agent names the surface (component, app UI, or marketing) and whether this is a new UI or a redesign. It reads only the refs for that case.

Unless the user said to invent everything, it runs a one-batch *briefing* for every blank (name, audience, success, look, stack when the repo has none) and ends the turn until those answers arrive. A bio or "unique" does not skip the form. It invents no product name.

It follows `DESIGN.md` when the repo has one, or writes one to the [DESIGN.md spec](https://github.com/google-labs-code/design.md/blob/main/docs/spec.md) before markup. CSS tokens map to that file.

Before markup it writes a one-line Design Read and a Lock: origin, name, scene, color strategy, layout, motion, density, stack. Greenfield with no stack uses `index.html`, `main.css`, and `main.js` unless the user picked a framework.

A new UI gets new files on that split. A redesign patches what is already there, on the current stack, after a short audit.

It finishes with a written *crit* (common AI layout, one alternative layout family), then by counting things in the DOM (pre-flight A always, B on marketing, C on app UI) and by checking layout and copy against [`anti-slop.md`](reference/anti-slop.md).

Ask for a landing, a settings page, or a restyle, or invoke `/frontend-design-plus`. Put this folder in whatever directory your harness uses for skills.

## Sources

What each publication became in the skill:

| Source                                                                                        | What the skill took                                                                                    |
| --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| [DESIGN.md Format spec](https://github.com/google-labs-code/design.md/blob/main/docs/spec.md) | Token YAML, section order, follow-or-generate                                                          |
| [UX-Context Design (NN/G)](https://www.nngroup.com/articles/ux-context-design/)               | Visual identity as in-repo context; constraints and glossary, not personas; use-context steers density |
| [Context Architecture](https://context-architecture.dev/)                                     | Bind stack, files, and tokens to something that fails when they drift; *cold reader*; disk wins        |
| [How we do design critiques at Figma](https://www.figma.com/blog/design-critiques-at-figma/)  | Frame *looking for / not*; silent pass before edits                                                    |
| [How to Run a UX Design Critique (UX Tigers)](https://www.uxtigers.com/post/design-crit)      | Frame → silent written crit → prioritize → fix; user problem, not widget recipe                        |
