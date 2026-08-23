---
name: frontend-design-plus
description: >-
  Ship working web UI (components, pages, landings, dashboards, posters, HTML/CSS) after a batched briefing. Skip backend, SQL, CI, or docs-only work.
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

The first user-facing output on an unanswered `full` run is the structured question call for every remaining briefing blank. The host's question interface may be `AskQuestion` or an equivalent structured tool. A numbered list of questions in the chat message fails this turn.

## Execution mode

Choose the mode from these three lines. Do not open [execution-modes.md](reference/execution-modes.md) here.

- `full` — default for marketing and app UI when the harness can hand off slots.
- `solo` — same slot order in one window when no child-agent tool exists.
- `fast` — isolated component, polish with a named focus, or a complete low-risk prompt.

The mode changes orchestration, not the quality gates. Declare `mode=` in the Lock. Question-interface fallbacks live in [execution-modes.md](reference/execution-modes.md); open that file at dispatch, or in `solo` when closing slot files.

## Pace

- **Classify from disk.** Name only task type and origin from the prompt plus a repo glance (`package.json`, existing markup, `DESIGN.md`). No `reference/` files. Classify does not fill briefing fields. If origin is unclear, ask once through the host's question interface and end the turn. Do not mix origin with briefing fields.
- **This turn's file is [briefing.md](reference/briefing.md).** Open it once. Score every applicable field against the prompt and disk before any question. invent-all or an isolated component skip it (then [after-briefing.md](reference/after-briefing.md)).
- **Unanswered.** No invent-all, and [briefing.md](reference/briefing.md) still has blanks that apply this origin: send every remaining blank in one structured question call when the host tool accepts multiple questions, then end the turn. If the host accepts only one question per call, ask the first remaining blank and declare `questions=serial`. Markup, Design Read, Lock, and an unstructured dump of questions fail this turn.
- **After answers.** When every field has an owner, or briefing.md skipped the form, open [after-briefing.md](reference/after-briefing.md). That file orchestrates Direction, Implement, and QA ([dispatch.md](reference/dispatch.md)). If blanks remain, stay on briefing.md.

## Workflow

0. **Mode.** Choose `full`, `solo`, or `fast` from the three lines above. Done when the mode is named. Do not open `reference/` this step.
1. **Classify.** Pick component, app UI, or marketing ([task routing](#task-routing)). Glance at `package.json` for whether a stack exists. Name **origin**: `greenfield` (new UI), `redesign` (existing UI, new composition from the user briefing), or `polish` (existing UI, improve craft, keep the look). If origin is unclear, ask once and end the turn. Done when task type and origin are named, no briefing field was filled, and no `reference/` file was opened this step.
2. **Briefing.** Open [briefing.md](reference/briefing.md) and follow it. Done when that file's done criterion holds for the selected mode.

## Task routing

Name the type at Classify. After answers, [after-briefing.md](reference/after-briefing.md) packs a Briefing card and [dispatch.md](reference/dispatch.md) attaches slot files from [load-map.md](reference/load-map.md). Use the selected execution mode's worker interface. The parent does not open composition, the Catalog, anti-slop, crit, pre-flight, product-register, ux-principles, verification, or visual-rubric, except an isolated component (pre-flight A in this window).

| Task type     | Examples                                                        | Pre-flight |
| ------------- | --------------------------------------------------------------- | ---------- |
| **Component** | Button, modal, card, form field                                 | A          |
| **App UI**    | Dashboard, CMS, CRM, admin. Recipe, not a poster.               | A + C      |
| **Marketing** | Landing, portfolio, campaign, about                             | A + B      |
