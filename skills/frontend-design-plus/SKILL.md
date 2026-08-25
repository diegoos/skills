---
name: frontend-design-plus
description: >-
  Build, redesign, or polish web UI (page, landing, dashboard, component, HTML/CSS). Review or fix layout, spacing, type, and a11y on existing markup. Loose marketing starts with one occupancy question, not an industry palette. Skip backend, SQL, CI, docs-only, and native mobile/desktop (SwiftUI, Flutter).
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

The first user-facing output on an unanswered greenfield marketing run is one structured question: two layout directions, Job if the prompt named none, or Style yes/no once occupancy exists and Look is still unnamed. The host's question interface may be `AskQuestion` or an equivalent structured tool. A numbered list of questions in the chat message fails this turn. An eight-field briefing dump fails this turn.

## Words

| Term | Meaning |
| --- | --- |
| **Job** | What the person came to *do*. One line. |
| **Success** | Primary action: verb + object. |
| **Origin** | `greenfield` \| `redesign` \| `polish`. |
| **Mode** | `full` \| `solo` \| `fast` — orchestration, not quality. |
| **Lock** | Closed decisions for this run. |
| **Packet** | Card the next slot receives. |
| **Occupancy** | What occupies the first viewport (masses, not “hero”). |
| **Sketch** | 12-column ASCII of those masses; `none` on app UI and polish. |
| **Token** | Named visual in DESIGN.md, not a raw value. |
| **Slot** | Direction \| Implement \| QA. |
| **Recipe** | Product layout (`queue-home`, `list-filter`, `editor`, `accounts`). |
| **Verification** | Evidence block (`proof=`, viewports). Not a user study. |

## Execution mode

Choose the mode from these three lines. Do not open [execution-modes.md](reference/execution-modes.md) here.

- `full` — default for marketing and app UI when the harness can hand off slots.
- `solo` — same slot order in one window when no child-agent tool exists.
- `fast` — isolated component, `origin=polish`, or a complete low-risk prompt. Extra stay-closed: [load-map.md](reference/load-map.md#fast). Does not skip Direction on greenfield or redesign marketing or app UI.

`origin=polish` sets `mode=fast` and skips Direction ([polish.md](reference/polish.md)). The mode changes orchestration, not the quality gates. Declare `mode=` in the Lock. Question-interface fallbacks live in [execution-modes.md](reference/execution-modes.md); open that file at dispatch, or in `solo` when closing slot files.

## Pace

- **Classify from disk.** Name only task type and origin from the prompt plus a repo glance (`package.json`, existing markup, `DESIGN.md`). No `reference/` files. Classify does not fill briefing fields. If origin is unclear, ask once through the host's question interface and end the turn. Do not mix origin with briefing fields.
- **Polish.** Origin `polish` on marketing or app UI: this turn's file is [polish.md](reference/polish.md). Do not open briefing.md. Isolated component: [after-briefing.md](reference/after-briefing.md#isolated-component).
- **Else this turn's file is [briefing.md](reference/briefing.md).** Open it once. Greenfield marketing with a named Job: infer the domain's layout behavior and the category cliché to refuse, then send **one** A/B occupancy question. After occupancy exists, if Look is still unnamed, send **one** Style yes/no. If yes, next turn print [catalog.md](reference/catalog.md) and ask one id. No Job: ask Job only. invent-all or an isolated component skip it (then [after-briefing.md](reference/after-briefing.md)).
- **Unanswered.** A greenfield marketing run missing Job, the A/B pick (when occupancy is unnamed), or the Style answer (when Look is unnamed): that one structured question is the user-facing output, then end the turn. Markup, Design Read, Lock, and a multi-field dump fail this turn. Mute polish: the Focus question in polish.md is the output, then end the turn.
- **After answers.** Polish: stay on [polish.md](reference/polish.md). Otherwise, when every applicable owner exists (including inferred domain behavior, the A/B pick, and Look on marketing), or briefing.md skipped the form, open [after-briefing.md](reference/after-briefing.md). That file orchestrates Direction, Implement, and QA ([dispatch.md](reference/dispatch.md)). If Job, occupancy, or Style is still blank, stay on briefing.md.

## Workflow

0. **Mode.** Choose `full`, `solo`, or `fast` from the three lines above. Done when the mode is named. Do not open `reference/` this step.
1. **Classify.** Pick component, app UI, or marketing ([task routing](#task-routing)). Glance at `package.json` for whether a stack exists. Name **origin**: `greenfield` (new UI), `redesign` (existing UI, new composition from the user briefing), or `polish` (existing UI, improve craft, keep the look). If origin is unclear, ask once and end the turn. Polish: set `mode=fast` and open [polish.md](reference/polish.md); skip step 2. Redesign with no `DESIGN.md` on disk: Direction extracts tokens from current CSS; do not invent a palette here. Done when task type and origin are named, no briefing field was filled, and no `reference/` file was opened this step except polish.md after origin is named.
2. **Briefing.** Skip on polish. Open [briefing.md](reference/briefing.md) and follow it. Done when that file's done criterion holds for the selected mode.

## Task routing

Name the type at Classify. Do not open `reference/` this step except polish.md or the briefing file named in Pace. After answers, [after-briefing.md](reference/after-briefing.md) packs a Briefing card and [dispatch.md](reference/dispatch.md) attaches slot files from [load-map.md](reference/load-map.md). Use the selected execution mode's worker interface. Parent closed-file list lives in load-map Parent; open that heading only after the card exists. Isolated component: after-briefing Isolated (Implement + Tier A in this window; skip Direction and crit). Polish marketing or app UI: [polish.md](reference/polish.md) (same window; skip Direction and crit).

| Task type     | Examples                                                        | Pre-flight |
| ------------- | --------------------------------------------------------------- | ---------- |
| **Component** | Button, modal, card, form field                                 | A          |
| **App UI**    | Dashboard, CMS, CRM, admin. Recipe, not a poster.               | A + C      |
| **Marketing** | Landing, portfolio, campaign, about                             | A + B      |
