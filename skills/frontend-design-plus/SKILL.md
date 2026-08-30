---
name: frontend-design-plus
description: >-
  Web UI: build, redesign, or polish a landing, dashboard, or component (HTML/CSS). Fix layout, spacing, type, or a11y on existing markup. Skip backend, SQL, CI, docs-only, and native mobile/desktop (SwiftUI, Flutter).
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

Work as the design lead at a small studio. This client rejected templated proposals. Make opinionated choices about palette, type, and layout that belong to this brief. Take one aesthetic risk you can justify.

Occupancy first: rectangles of the Job's objects, then tokens.

## Words

| Term | Meaning |
| --- | --- |
| **Job** | What the person came to do. One line. |
| **Origin** | `greenfield` \| `redesign` \| `polish`. |
| **Mode** | `Persuade` \| `Operate` \| `Read` \| `Experience`. |
| **Signature** | The one memorable risk. Everything else stays quiet. |

## Classify

Name Origin and Mode from the prompt plus a repo glance (`package.json`, existing markup, `DESIGN.md`). Done when both are named.

**Origin.** Polish, tighten, craft, spacing, contrast, states, or a11y, and no new look → `polish`. Redesign, restyle, new IA, or rethink → `redesign`. Existing markup plus a new job or composition → `redesign`. Else `greenfield`. Unclear: ask once and end the turn.

**Mode.** Landing, campaign, pricing → `Persuade`. Dashboard, admin, editor, settings → `Operate`. Docs, article, help → `Read`. Portfolio, gallery, the work itself → `Experience`. Choose from the surface, not the company. A tool's marketing page is still `Persuade`.

**Idea.** If the prompt names no concrete subject and Job, ask **one** Job question and end the turn. If the idea is in the prompt, continue. Done when Job is named in the prompt or that question was the only user-facing output.

Isolated component: Classify, then Origin on that control. Leave [app-ui.md](reference/app-ui.md) closed.

## Origin

- **greenfield** — Infer the first costume (navy+justice, indigo+three cards, cream+serif). Invent hex and occupancy from the object. Invent-the-look is this path.
- **redesign** — Disk owns color, type, radius. Keep / retire / missing against the Aim in the prompt. Blocks that still serve Aim stay (news, list, catalog stay that form). Unify CSS to filled DESIGN.md; patch DESIGN.md only when the user asked or contrast fails.
- **polish** — Keep the live palette. Mute ("improve this"): ask **one** Focus question, Finish the path first, end the turn. Named focus or finish: audit (P0 contrast, overflow, hidden action; P1 rhythm, states), then close those rows. Filled DESIGN.md wins. Ask before changing routes, nav labels, form names, wordmark, legal copy, or the CSS library.

Done when this Origin's work for the turn is finished (mute polish: the Focus question; otherwise DESIGN.md is ready for Layout or already law on disk).

## Layout

Write `DESIGN.md` **before** markup. Spec: [design-md.md](reference/design-md.md). Occupancy first, then type and color.

1. Job in one line. Objects: ≤7 domain nouns (opinion letter, kiln, queue), not hero / card / sidebar.
2. ASCII of the first viewport. Enter is the object's mass. Squint: what leads, what supports, the groups. Proximity before a container. Numbered markers only on a real sequence.
3. Mode. `Persuade`: occupy what / why / how / trust / act. `Operate`: open [app-ui.md](reference/app-ui.md); `main` is the work. `Read`: structure for comprehension. `Experience`: the artifact leads; chrome recedes.
4. Dials, one line: `variance` / `motion` / `density` on 1–10. Operate: density high, motion low. Persuade/Experience may go asymmetric. Trust-first: low variance.
5. Signature on the enter mass. Then 4–6 named hex values and 2+ type roles. A component exists only if an object asked for it.

If the plan would pass on any similar page, retune **one** role and say what changed. If the user named a look in the prompt, follow those words. Free axis: hex from the object. Brief wins when it names a default look.

Spend boldness on Signature. Remove one accessory before shipping.

Copy is material. Name what people control. Active voice. Same action, same label. Error and empty: what happened + the next step. Sentence case.

Done when DESIGN.md exists, Layout names Job, objects, Mode, ASCII (polish: live family), and Signature, and color/type slots are filled. Then write the code from that file. CSS tokens match 1:1.

## Floor

Viewport zoomable (`width=device-width, initial-scale=1`, no `user-scalable=no`). Body and inputs ≥16px. One `h1`. Page shell: skip link → `#main`. Contrast ≥4.5:1 body, ≥3:1 icons. Visible focus. Keyboard reaches every action. Targets ≥44px with ≥8px gap. `prefers-reduced-motion` when motion exists. No overflow at 375. One filled primary per view (`Operate`) or per fold (`Persuade`). Hover is enhancement.

Browser or screenshot tool: Walk 1440 and 375, hit the primary CTA. Unused tool fails. No browser tool: skip Walk.

Done when every row that applies holds.

## Critique

After markup, open [critique.md](reference/critique.md) once. Done when that file's done criterion holds.
