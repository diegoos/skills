---
name: frontend-design-plus
description: >-
  Build or restyle web UI: components, pages, landings, dashboards, posters, HTML/CSS layouts. Use when the work is visual frontend (layout, type, color, motion, a11y) and the output must pass anti-slop craft. Classify each task as greenfield (new UI) or redesign (existing page). Skip backend-only, SQL, CI, or docs-only tasks.
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

Ship working frontend. The user names a component, page, app, or surface, and may add audience, constraints, or an existing system.

## Pace

Read routed references before the first markup.

- **Routed refs only.** Load the files [task routing](#task-routing) assigns.
- **Inspect the repo.** Tokens, components, neighboring screens. Detect stack from `package.json`, CSS, framework files. If stack matters and nothing is detectable, ask once. Decide **origin** (greenfield vs redesign) before markup; existing page files mean redesign until the user says otherwise.
- **One intent per lookup.** Open the one owning file; retry once narrower; if still empty, follow the [priority table](#priority-order) and say the fallback is the table.
- **Design Read + Lock before markup** on app UI and marketing. Name color strategy before any hex ([color.md](reference/color.md#color-strategies)).
- **One surface per pass.** Finish that surface's pre-flight before the next page or variant.
- **Pause on reflex.** Centered hero, three equal cards, or purple gradient means return to direction.
- **Slop test.** Run [anti-slop.md](reference/anti-slop.md) before calling the surface done.

## Workflow

1. **Classify.** Pick component, app UI, or marketing. Detect stack. Name **origin**: `greenfield` (new UI) or `redesign` (the page or component already exists). If origin is unclear, ask once. `redesign`: read [redesign.md](reference/redesign.md) before step 3. Done when the Task routing row **and** origin are named.
2. **Prioritize.** Walk the [priority table](#priority-order) top-down; skip rows that do not apply. Done when each applicable row has an owner file.
3. **Read.** Routed refs plus project tokens/CSS. Done when those files are in context.
4. **Declare.** Design Read + Lock on app UI and marketing. Color strategy when palette or theme is in play. Done when both lines exist. No markup before that.
5. **Direction.** Pick one aesthetic that fits the brief (brutalist, editorial, industrial, luxury, organic, maximalist, art deco, playful). Marketing Lock names one material or spatial break. App UI Lock names the 1–2 Pareto screens. Done when those names are in the Lock.
6. **Implement.** Greenfield: write the new surface. Redesign: patch the existing files on the current stack (scan → diagnose → fix in [redesign.md](reference/redesign.md)); keep functionality. Reuse the project design system when it exists.
7. **Pre-flight.** Run the matching tier in [preflight-checklist.md](reference/preflight-checklist.md). Tiers B and C pass as DOM counts. Tab interactive elements. State what was not verified. Done when every applicable box is checked or failed and fixed.

**Design Read** (one sentence):

> Reading this as: \<page kind> for \<audience>, with a \<vibe> language, leaning toward \<register or design system>.

**Lock** (next line):

> Lock: origin=\<greenfield|redesign>; scene=\<place/time/mood>; color=\<restrained|committed|full|drenched>; layout=\<contained|offset|wild>; motion=\<still|fluid|cinematic>; density=\<airy|regular|dense>; stack=\<detected or asked>.

Quiet constraints (a11y-first, regulated, public-sector, kids) override Lock bands. Each dial must change spacing, layout family, or motion recipe ([design-systems.md](reference/design-systems.md#density-bands), [brand-register.md](reference/brand-register.md#lock-bands)). A Lock that only labels fails step 4. Redesign Lock also names `mode=preserve|overhaul`.

Product chrome stays consistent. Ask one clarifying question when the read diverges from the brief. Worked examples: [design-read-examples.md](reference/design-read-examples.md).

## Priority order

Work top-down. Pre-flight is the ship gate; this table is work order.

| #   | Focus      | Check                                      | Anti-pattern                              | Read                                                                                                      |
| --- | ---------- | ------------------------------------------ | ----------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| 1   | A11y       | Contrast 4.5:1, visible focus, keyboard    | Removing focus rings                      | [preflight A](reference/preflight-checklist.md)                                                           |
| 2   | Touch      | Targets ≥44px, 8px gap, press feedback     | Hover-only actions                        | [production-engineering.md](reference/production-engineering.md)                                          |
| 3   | Perf       | LCP/CLS, reserved space                    | Layout shift                              | [performance.md](reference/performance.md)                                                                |
| 4   | Direction  | Design Read + Lock with origin             | Markup without Lock or origin             | this file                                                                                                 |
| 5   | Layout     | Mobile-first, no horizontal scroll         | Fixed-px cages on every surface           | [layout-patterns.md](reference/layout-patterns.md) / [product-register.md](reference/product-register.md) |
| 6   | Type/color | Named strategy, tokens                     | Raw hex, gray-on-gray                     | [color.md](reference/color.md), [typography.md](reference/typography.md)                                  |
| 7   | Motion     | Recipe matches the Lock band               | One duration for everything               | [motion.md](reference/motion.md)                                                                          |
| 8   | Forms      | Visible labels, blur+submit, error summary | Placeholder-as-label; error per keystroke | [production-engineering.md](reference/production-engineering.md#forms)                                    |
| 9   | Nav        | Predictable back, one primary per view     | Overloaded chrome                         | [ux-principles.md](reference/ux-principles.md)                                                            |
| 10  | Data       | Chart matches the question                 | Chart gallery, color-only encoding        | [ux-principles.md](reference/ux-principles.md#dashboards-and-data-ui)                                     |

## Task routing

Read only what the task needs.

| Task type     | Examples                            | Read                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Pre-flight |
| ------------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| **Component** | Button, modal, card, form field     | [production-engineering.md](reference/production-engineering.md)                                                                                                                                                                                                                                                                                                                                                                                             | A          |
| **App UI**    | Dashboard, settings, admin, tool    | [product-register.md](reference/product-register.md), [ux-principles.md](reference/ux-principles.md), [production-engineering.md](reference/production-engineering.md)                                                                                                                                                                                                                                                                                       | A + C      |
| **Marketing** | Landing, portfolio, campaign, about | [brand-register.md](reference/brand-register.md), [layout-patterns.md](reference/layout-patterns.md), [assets.md](reference/assets.md). Add [color.md](reference/color.md) when the Lock is committed, full, or drenched, or the scene is dark. Add [motion.md](reference/motion.md) when entrance or scroll choreography is in scope. Add [material-craft.md](reference/material-craft.md) when the Lock names a nested enclosure, hairline, or island CTA. | A + B      |

**Redesign** (`origin=redesign`): also [redesign.md](reference/redesign.md) before changing tokens, IA, or copy. Skip that file on greenfield.

**On demand:** [typography.md](reference/typography.md), [performance.md](reference/performance.md), [design-systems.md](reference/design-systems.md).

## Production baseline

| Requirement       | Minimum                                                                                                |
| ----------------- | ------------------------------------------------------------------------------------------------------ |
| **States**        | Default, hover, focus, active, disabled; loading, error, empty when async                              |
| **Accessibility** | Semantic HTML, labels, keyboard nav, visible focus, WCAG 2.2 AA contrast                               |
| **Responsive**    | Mobile-first; touch targets ≥44px with ≥8px gap; no horizontal overflow on 320px; viewport allows zoom |
| **Design system** | Reuse project tokens and components                                                                    |

Patterns: [production-engineering.md](reference/production-engineering.md).
