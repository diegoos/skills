# Frontend Design Plus

The skill tells an agent how to ship working web UI that does not look or read like default model output. Use it for a new page or a restyle of one that already exists: landings, dashboards, components, posters, HTML/CSS layouts.

Skip it when the work is backend, SQL, CI, or docs. The instructions the agent follows are in [`SKILL.md`](SKILL.md). Extra rules live in [`reference/`](reference/) and load only for the kind of surface being built.

## What it is for

Two jobs, different stances.

On a landing or campaign, design is the product. The visitor's first impression is the deliverable.

On a dashboard or settings screen, the interface should disappear into the task. Familiar chrome, one primary action, the project's tokens.

Either way the output is code, not a mock. Touch targets, contrast, and real copy are part of done.

## How it works

The agent names the surface (component, app UI, or marketing) and whether this is a new UI or a redesign. It reads only the refs for that case. Before markup it writes a one-line Design Read and a Lock: origin, scene, color strategy, layout, motion, density, stack.

Then it builds. A new UI gets new files. A redesign patches what is already there, on the current stack, after a short audit.

It finishes by counting things in the DOM (pre-flight A always, B on marketing, C on app UI) and by checking layout and copy against [`anti-slop.md`](reference/anti-slop.md).

Ask for a landing, a settings page, or a restyle, or invoke `/frontend-design-plus`. Put this folder in whatever directory your harness uses for skills.
