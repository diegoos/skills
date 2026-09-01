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

You invoked this skill to ship a layout like a senior frontend engineer. The run is Classify → Origin → Layout → markup from DESIGN.md → Floor → Critique once. Do not write markup before Layout is done. Mute polish may stop after the Focus question. Isolated component skips [app-ui.md](reference/app-ui.md).

Quality is the same chain the whole way: object's rectangles, then tokens, then the live page matching that spine, then every Fail-if in scope. Critique does not invent a second look.

Occupancy first. Hex from the object's materials. One risk on the enter fragment; the rest stays quiet.

## Words

| Term          | Meaning                                            |
| ------------- | -------------------------------------------------- |
| **Job**       | What the person came to do. One line.              |
| **Origin**    | `greenfield` \| `redesign` \| `polish`.            |
| **Mode**      | `Persuade` \| `Operate` \| `Read` \| `Experience`. |
| **Signature** | The one risk: a treatment of the enter fragment.   |
| **Claim**     | One line of using this product. Not a style name.  |
| **Pair**      | Two traits this object justifies.                  |

## Classify

Name Origin and Mode from the prompt plus a repo glance (`package.json`, existing markup, `DESIGN.md`). Done when both are named.

**Origin.** Polish, tighten, craft, spacing, contrast, states, or a11y, and no new look → `polish`. Redesign, restyle, new IA, or rethink → `redesign`. Existing markup plus a new job or composition → `redesign`. Else `greenfield`. Unclear: ask once and end the turn.

**Mode.** Landing, campaign, pricing → `Persuade`. Dashboard, admin, editor, settings → `Operate`. Docs, article, help → `Read`. Portfolio, gallery, the work itself → `Experience`. Choose from the surface, not the company. A tool's marketing page is still `Persuade`.

**Idea.** If the prompt names no concrete subject and Job, ask **one** Job question and end the turn. If the idea is in the prompt, continue. Done when Job is named in the prompt or that question was the only user-facing output.

Isolated component: Classify, then Origin on that control.

## Origin

- **greenfield** — Name the costume you would reach for first. Invent occupancy and hex from the object's materials (ink, newsprint, kiln). Invent-the-look is this path.
- **redesign** — Disk owns color, type, radius. Keep / retire / missing against the Aim in the prompt. Blocks that still serve Aim stay (news, list, catalog stay that form). Unify CSS to filled DESIGN.md; patch DESIGN.md only when the user asked or contrast fails.
- **polish** — Keep the live palette. Mute ("improve this"): ask **one** Focus question, Finish the path first, end the turn. Named focus or finish: audit (P0 contrast, overflow, hidden action; P1 rhythm, states), then close those rows. Filled DESIGN.md wins. Ask before changing routes, nav labels, form names, wordmark, legal copy, or the CSS library.

Done when this Origin's work for the turn is finished (mute polish: the Focus question; otherwise DESIGN.md is ready for Layout or already law on disk).

## Layout

This step **is** the layout. Write `DESIGN.md` **before** markup. Spec: [design-md.md](reference/design-md.md). Occupancy first, then type and color.

1. Job in one line. Claim. Pair. Objects: ≤7 domain nouns (opinion letter, kiln, queue), not hero / card / sidebar.
2. ASCII of the first viewport, then 3–5 fold names down the page. Enter is the object's mass. Chrome is one row; a drawer is closed. The enter rectangle must fit at 375 below that row; otherwise the plan is already wrong. Squint: what leads, what supports, the groups. Proximity before a container. A real sequence is the object's control, not `01`/`02`/`03` cards. If the second fold is named how-it-works, benefits, or three gestures, or is a second layout of the same enter object, the plan is already wrong.
3. Mode. `Persuade`: enter is the object plus the act. The next fold is another object (price, archive, sources) or the create control — not a paraphrase of enter. `Operate`: open [app-ui.md](reference/app-ui.md); `main` is the work. `Read`: structure for comprehension. `Experience`: the artifact leads; chrome recedes.
4. Dials, one line: `variance` / `motion` / `density` on 1–10. Operate: density high, motion low. Persuade/Experience may go asymmetric. Trust-first: low variance.
5. Signature on the enter mass. Disk-filled DESIGN.md: those hex, type, and radius; Signature is still a treatment of the live fragment (mark, crop, stamp). Greenfield: hex from the object's materials. Then 4–6 named hex values and 2+ type roles. A component exists only if an object asked for it.

If the ASCII would fit another product in the same Mode, retune **one** role and say what changed. If the user named a look in the prompt, follow those words. Free axis: hex from the object. Brief wins when it names a default look.

Spend boldness on Signature. Cut one fold before shipping.

Copy: name what people control. Same action, same label. Fail-ifs: [anti-slop.md](reference/anti-slop.md#copy).

Done when DESIGN.md exists, Layout names Job, objects, Mode, ASCII plus spine folds (polish: live family), Claim, Pair, and Signature, and color/type slots are filled. Then write the code from that file. CSS tokens match 1:1. Markup that is not this spine already failed.

## Floor

The live page is the Layout. Viewport zoomable (`width=device-width, initial-scale=1`, no `user-scalable=no`). Body and inputs ≥16px. One `h1`. Page shell: skip link → `#main`. Contrast ≥4.5:1 body, ≥3:1 icons. Visible focus. Keyboard reaches every action. Targets ≥44px with ≥8px gap. `prefers-reduced-motion` when motion exists. No overflow at 375. One filled primary per view (`Operate`) or per fold (`Persuade`). Hover is enhancement.

Browser or screenshot tool: open [anti-slop.md](reference/anti-slop.md#walk). Unused tool fails. No browser tool: skip Walk.

Done when every row that applies holds.

## Critique

After markup, open [critique.md](reference/critique.md) once. That file opens [anti-slop.md](reference/anti-slop.md) when Design or Copy is in scope. Confirm the spine held. Done when critique.md's done criterion holds.
