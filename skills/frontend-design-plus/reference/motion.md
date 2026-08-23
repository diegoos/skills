# Motion

Load when [load-map.md](load-map.md) attaches this file (Behave or Lock `fluid` / `cinematic`, or task type **app UI**). Marketing with Behave `still` / `none` leaves this file closed. Unanswered blanks belong to the Packet.

Motion shows state, hierarchy, and feedback. One orchestrated entrance.

## Product micro

Always on app UI, including Lock `still`. Chrome already at rest does not play a mount entrance.

- Interactive state (hover, open/close, press): CSS **transitions**. Keyframes only for one-shot sequences (empty → data, skeleton).
- Product `:active` on buttons: `scale(0.96)`. Interruptible. Never below `0.95`. Brand island CTA stays `0.98` ([material-craft.md](material-craft.md#island-cta)).
- High-frequency rows, tabs, and filter chips: background or opacity ≤150ms. No stagger, bounce, or entrance replay on every hover.
- Motion is never the only cue. Keep color, icon, or label. `prefers-reduced-motion`: keep that cue; cut movement.

List stagger 30–50ms is for one-shot empty → data only.

## Core principles

- Animate to show change. Properties on the hot path: `transform` and `opacity`. Leave `width`, `height`, `top`, `left`, `margin`, and `padding` still.
- Honor `prefers-reduced-motion` with instant or crossfade alternatives.
- Stillness can be voice. Some brands skip entrance motion.

## Motion registers

| Register | Role of motion | Typical approach | Lock band |
| --- | --- | --- | --- |
| **Brand** | Emotion, storytelling, first impression | Orchestrated page-load; scroll choreography when `cinematic` | `still` / `fluid` / `cinematic` |
| **Product** | State change, feedback, spatial logic | 150–250ms; instant or crossfade for reduced motion | `still` or `fluid` — not cinematic chrome |

**Claimed = shown:** if the Lock says `cinematic`, the page must move (hero entrance + one reveal + CTA hover) or drop the band to `fluid`/`still`. If the Lock says `still`, do not add entrance choreography.

## Microinteraction contract

Every loop or control animation names four parts. Missing a part means cut the motion.

1. **Trigger** — user action or system state change
2. **Condition** — when it fires (and when it must not)
3. **Feedback** — visual change (`transform`/`opacity` only on the hot path)
4. **End** — how it stops (duration, interrupt on tap, pause offscreen, reduced-motion)

Authorize **one** authorial loop per surface (like, pull-to-refresh, press). Fade-up on every card fails this contract.

Auto-rotate carousels and marquees: visible pause/stop; pause on focus, hover, and `prefers-reduced-motion`; die on unmount.

## Timing and easing

| Use case | Duration | Easing |
| --- | --- | --- |
| Button hover, micro-interaction | 150–200ms | `ease-out` (decelerate) |
| Modal open/close, panel slide | 250–350ms | `cubic-bezier(0.25, 0.1, 0.25, 1)` |
| Page entrance, hero reveal | 400–800ms | `cubic-bezier(0.22, 1, 0.36, 1)` or similar expo ease-out |
| Product list stagger | 400–600ms per item | Same; stagger **30–50ms** |
| Brand hero stagger | — | 100–150ms between hero secondary items |
| Exit | ~60–70% of enter duration | Same curve family |

**Avoid**: bounce, elastic, or spring easing on product UI. Reserve expressive easing for brand surfaces when the brief demands it.

**Product budget:** 1–2 elements animating per view. **Brand:** one orchestrated idea on load; do not apply the 1–2 cap to that hero.

## Entrance choreography (brand surfaces)

A strong brand entrance has a single idea:

1. **Hero loads first** — headline and primary visual within 400ms
2. **Secondary elements follow** — subtext, CTAs with 100–150ms stagger
3. **Below-fold waits** — delay until scroll proximity, not on page load

Use intersection observers or scroll-driven triggers for below-fold content. Do not animate everything on mount.

## Scroll-driven patterns

| Pattern | Implementation approach | When to use |
| --- | --- | --- |
| **Reveal on scroll** | Intersection Observer toggles class; CSS handles transition | Default for most content |
| **Sticky scroll stack** | Pin section while next scrolls over; CSS sticky or scroll-timeline | High-motion brand briefs only |
| **Horizontal pan** | Vertical scroll drives horizontal offset via scroll-timeline or JS | Gallery transitions |
| **Parallax layers** | Different scroll speeds for background/foreground elements | Sparingly; never on product UI |

**Rules**:

- Pin/scrub: start when the section top hits the viewport top (`start: "top top"` or CSS sticky equivalent). Pin the wrapper; scrub the inner track. Cleanup on unmount.
- Justify each pin in one sentence (hierarchy, story, feedback, or state) or cut it.
- Prefer CSS `scroll-timeline` / `position: sticky` before a JS library. No canonical GSAP/React skeleton.
- Never drive animation state from scroll events that trigger layout recalculations.
- Scroll hijacking (intercepting native scroll) is a last resort.

## Brand choreography recipes (`cinematic` only)

Use at most what the Lock asked for. Sticky 64–72px nav remains the default.

- **Island nav** — floating pill, hamburger lines morph to an X, overlay with stagger mask. Blur on the pill or overlay chrome, not on the scrolling document. [layout-patterns.md](layout-patterns.md#named-patterns)
- **Press + nested icon** — `scale(0.98)` on the island CTA; the inner icon translates on hover ([material-craft.md](material-craft.md#island-cta))
- **Modal from trigger** — scale+fade or slide from the source control, not a generic center fade

## Hover and interaction states

- Buttons: `transform: translateY(-1px)` or `scale(0.96)` on product `:active` — compositor only; padding/width stay put. Brand island CTA: `scale(0.98)` ([material-craft.md](material-craft.md#island-cta)).
- Cards: `scale(1.01)` or shadow elevation — never color inversion unless it signals selection.
- Links: underline animation (`background-size` transition) or color shift — not generic opacity dim.

## Loading and skeleton states

- Skeletons animate with `pulse` or `shimmer` — never with bounce or elastic.
- Match skeleton layout to final layout; generic spinners are a fallback for unknown shapes only.

## Performance guardrails

- `will-change: transform` only on elements actively animating; remove after.
- Grain, noise, and blur overlays: use `fixed` positioning with `pointer-events: none` to avoid repaint on scroll.
- Limit simultaneous animations. Product: 1–2 moving elements per view. Brand: one load idea.

## Reduced motion

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

This is a global safety net. Per-component instant/crossfade overrides are preferred for critical state changes (modals, toasts).

## Motion tells (avoid)

- Reveal animations that gate content (content hidden until animation completes)
- Full ban list: [anti-slop.md#motion-tells](anti-slop.md#motion-tells)
