---
name: frontend-design-plus
description: >-
  Ship working web UI (components, pages, landings, dashboards, posters, HTML/CSS) after a one-field briefing. Skip backend, SQL, CI, or docs-only work.
disable-model-invocation: true
metadata:
  version: 0.0.1
  author: "Diego Oliveira"
  tags:
    - frontend
    - design
    - ui
    - ux
---

# Frontend Design Plus

The first user-facing output on an unanswered run is one `AskQuestion` for the next blank field.

## Pace

- **Classify from disk.** Name only task type and origin from the prompt plus a repo glance (`package.json`, existing markup, `DESIGN.md`). No `reference/` files. Classify does not fill briefing fields. If origin is unclear, ask once with `AskQuestion` and end the turn.
- **This turn's file is [briefing.md](reference/briefing.md).** Open it before scoring any field. invent-all or an isolated component skip it (then [after-briefing.md](reference/after-briefing.md)).
- **Unanswered.** No invent-all, and [briefing.md](reference/briefing.md) still has a blank that applies this origin: call `AskQuestion` for the first blank and end the turn. Markup, Design Read, Lock, and a numbered list of questions in chat fail this turn.
- **After answers.** When every field has an owner, or briefing.md skipped the form, open [after-briefing.md](reference/after-briefing.md). That file orchestrates Direction, Implement, and QA ([dispatch.md](reference/dispatch.md)). If blanks remain, stay on briefing.md.

## Workflow

1. **Classify.** Pick component, app UI, or marketing ([task routing](#task-routing)). Glance at `package.json` for whether a stack exists. Name **origin**: `greenfield` (new UI), `redesign` (existing UI, new composition from the user briefing), or `polish` (existing UI, improve craft, keep the look). If origin is unclear, ask once and end the turn. Done when task type and origin are named, no briefing field was filled, and no `reference/` file was opened this step.
2. **Briefing.** Open [briefing.md](reference/briefing.md) and follow it. Done when that file's done criterion holds.

## Task routing

Name the type at Classify. After answers, [after-briefing.md](reference/after-briefing.md) packs a Briefing card and [dispatch.md](reference/dispatch.md) attaches slot files from [load-map.md](reference/load-map.md). Dispatch each slot as a child agent when the harness has that tool; in-process only when it does not. The parent does not open composition, the Catalog, anti-slop, crit, pre-flight, product-register, or ux-principles, except an isolated component (pre-flight A in this window).

| Task type     | Examples                                                        | Pre-flight |
| ------------- | --------------------------------------------------------------- | ---------- |
| **Component** | Button, modal, card, form field                                 | A          |
| **App UI**    | Dashboard, CMS, CRM, admin. Recipe, not a poster.               | A + C      |
| **Marketing** | Landing, portfolio, campaign, about                             | A + B      |
