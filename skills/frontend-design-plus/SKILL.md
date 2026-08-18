---
name: frontend-design-plus
description: >-
  Ask unanswered briefing fields with AskQuestion, one field per turn, when greenfield app UI or marketing is missing audience or look, unless invent-all. Then build web UI: components, pages, landings, dashboards, posters, HTML/CSS. Classify from disk as greenfield (new UI), redesign (existing page from the user briefing), or polish (improve existing UI). Skip backend-only, SQL, CI, or docs-only tasks.
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
- **Unanswered.** Greenfield app UI or marketing, no invent-all, and the prompt named neither Audience nor Look (no group, no catalog `id`, no refs, no `you-decide`): call `AskQuestion` for the first blank. End the turn. Markup, Design Read, Lock, and a numbered list of questions in chat fail this turn. Look may print the Catalog table before its `AskQuestion` call.
- **After answers.** When every field has an owner, or briefing.md skipped the form, open [after-briefing.md](reference/after-briefing.md). If blanks remain, stay on briefing.md and ask the next one.

## Workflow

1. **Classify.** Pick component, app UI, or marketing ([task routing](#task-routing)). Glance at `package.json` for whether a stack exists. Name **origin**: `greenfield` (new UI), `redesign` (existing UI, new composition from the user briefing), or `polish` (existing UI, improve craft, keep the look). If origin is unclear, ask once and end the turn. Done when task type and origin are named, no briefing field was filled, and no `reference/` file was opened this step.
2. **Briefing.** Open [briefing.md](reference/briefing.md) and follow it. Do not score Name, Job, Audience, Success, Use, Look, Behave, Constraints, or Stack until that file is in context. invent-all and isolated component skip this file (Pace). Done when that file's done criterion holds. A first-person bio plus "showcase" / "unique", with Audience and Look unnamed, is unanswered: that file's Worked example is the first `AskQuestion` call.

## Task routing

Name the type at Classify. File lists open from [after-briefing.md](reference/after-briefing.md) after answers.

| Task type     | Examples                            | Pre-flight |
| ------------- | ----------------------------------- | ---------- |
| **Component** | Button, modal, card, form field     | A          |
| **App UI**    | Dashboard, settings, admin, tool    | A + C      |
| **Marketing** | Landing, portfolio, campaign, about | A + B      |
