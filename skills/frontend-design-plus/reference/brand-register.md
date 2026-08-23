# Brand register

Load when [load-map.md](load-map.md) attaches this file to the current slot. Unanswered blanks belong to the Packet.

When design is the product: landing pages, marketing sites, campaigns, portfolios, long-form content, about pages.

The visitor's impression is the deliverable. Stance: communicate. A luxury hotel, a devtools landing, and a restaurant each get their own lane.

## Brand slop test

The visitor should ask how this was made. Name a reference before committing: Stripe-minimal, Klim specimen, Liquid Death maximalism, Condé Nast editorial.

Describe the page the way a competitor would. If it fits the modal category landing, restart.

Full tells: [anti-slop.md](anti-slop.md). Category-reflex palettes: [color.md](color.md#category-reflex-rework-if-this-was-the-first-idea).

## Lock bands

Declare with the Design Read. Quiet constraints override.

| Band | Values | Mutates |
| --- | --- | --- |
| **layout** | `contained` / `offset` / `wild` | Centered OK only on contained (manifesto/launch). Offset and wild prefer split, magazine, or container-free. |
| **motion** | `still` / `fluid` / `cinematic` | Still: hover/focus only. Fluid: CSS transitions. Cinematic: claimed motion must show. |
| **density** | `airy` / `regular` / `dense` | Spacing tokens in [design-systems.md](design-systems.md#density-bands) |

Brand visual axes (pick one each; they are the Read, not a silent roll):

- **enclosure:** flat / nested / overlap (nested → [material-craft.md](material-craft.md), one per section)
- **rhythm:** macro-sparse / editorial / modular
- **surface:** matte / hairline / ink (glass only if the scene sentence asks)
- **type:** grotesk display / serif editorial / mono accent / one family

Product UI skips these axes. Chrome stays consistent. Brand may break external consistency once; that break is the memorable detail named in the Lock.

## Voice

Display + body when voice needs two families. Procedure: [typography.md](typography.md).

Brand may use Committed, Full palette, or Drenched ([color.md](color.md#color-strategies)). Name a real reference before picking. Commit to the edges or pick Restrained.

Marketing needs real photography ([assets.md](assets.md)). Hero, bento, magazine, container-free: [layout-patterns.md](layout-patterns.md). Nested enclosure or island CTA: [material-craft.md](material-craft.md).

One orchestrated page load, or stillness as voice. Scroll choreography when the brief supports high motion. Honor reduced motion. Timing: [motion.md](motion.md).

## Brand permissions

Things product UI often cannot afford:

- Ambitious first-load motion and typographic choreography
- Single-purpose viewports (one idea per fold)
- Unexpected color strategies
- Art direction varying per section when narrative demands

Consistency of **voice** beats consistency of **treatment**.

## AIDA structure (long-form marketing)

Optional scaffold:

1. **Attention:** cinematic hero
2. **Interest:** features, bento, proof
3. **Desire:** scroll media, storytelling, social proof
4. **Action:** CTA, pricing, footer

On **airy** / macro-sparse brand layouts, section padding is `6rem`–`10rem` (`py-24`–`py-40`) **between** sections. Hero top cap stays `6rem`. Name one spatial irregularity per page (overlap, scale jump, full-bleed). Product screens inherit this floor only on the 1–2 Pareto views named in the Lock.
