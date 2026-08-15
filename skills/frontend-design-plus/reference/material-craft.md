# Material craft

Recipes for brand surfaces that should feel machined or physical. Load when the Lock names a nested enclosure, hairline surface, or island CTA.

Product UI skips this file. Nested cards stay wrong in [product-register.md](product-register.md).

## Gates

- Brand register only
- At most **one** nested enclosure per section
- Island CTA on the **primary** action only
- Translate the structure to the project's tokens and syntax; the CSS below is the contract, not a Tailwind lock

## Nested enclosure (double-bezel)

Use when a hero asset, featured product, or one focal card should read as a plate sitting in a tray.

```html
<div class="enclosure">
  <div class="enclosure__core">
    <!-- focal content -->
  </div>
</div>
```

```css
.enclosure {
  padding: 0.375rem;
  border-radius: var(--radius-enclosure, 2rem);
  border: 1px solid color-mix(in srgb, var(--text-primary) 8%, transparent);
  background: color-mix(in srgb, var(--text-primary) 4%, var(--surface));
}

.enclosure__core {
  border-radius: calc(var(--radius-enclosure, 2rem) - 0.375rem);
  background: var(--surface-raised, var(--surface));
  box-shadow: inset 0 1px 0 color-mix(in srgb, #fff 18%, transparent);
  overflow: hidden;
}
```

**When:** one focal object per section that needs physical depth. **Not for:** every card, metric tiles, form groups, app chrome.

**Performance:** no `backdrop-filter` on this recipe. If a later glass variant is justified by the scene, apply blur only on `position: fixed` or `sticky` chrome — never on a scrolling card.

## Concentric radius

Inner radius = outer radius − padding. Never reuse the outer radius on the inner plate (the gap reads as a sliver, not a tray).

```css
--radius-enclosure: 2rem;
--enclosure-pad: 0.375rem;
/* inner: calc(var(--radius-enclosure) - var(--enclosure-pad)) */
```

## Inset highlight

One light source: a 1px inset highlight on the inner plate only (`inset 0 1px 0` mixed from white or `--text-primary`). Do not add a second highlight on the outer tray.

## Tinted hairline

Use instead of a generic gray `1px solid` when a region needs an edge.

```css
.hairline {
  border: 1px solid color-mix(in srgb, var(--text-primary) 10%, transparent);
}
```

On dark surfaces, mix from `#fff` at 10–14% instead of `--text-primary`. One light source: keep the mix consistent across the page.

**When:** same-plane separation (inputs at rest, image frames, dividers). **Not for:** side-stripe accent borders ([anti-slop.md](anti-slop.md)).

## Island CTA

Primary marketing button as a pill with a nested trailing icon — never a naked arrow beside the label.

```html
<a class="island-cta" href="…">
  <span>Start a project</span>
  <span class="island-cta__icon" aria-hidden="true">↗</span>
</a>
```

```css
.island-cta {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 0.75rem 0.75rem 1.5rem;
  border-radius: 999px;
  text-decoration: none;
}

.island-cta__icon {
  display: grid;
  place-items: center;
  width: 2rem;
  height: 2rem;
  border-radius: 999px;
  background: color-mix(in srgb, var(--text-primary) 8%, transparent);
  transition: transform 150ms ease-out;
}

.island-cta:hover .island-cta__icon {
  transform: translate(2px, -1px) scale(1.05);
}

.island-cta:active {
  transform: scale(0.98);
}
```

Press uses `transform` only. Padding and width stay put ([production-engineering.md](production-engineering.md)).

**When:** the one primary marketing CTA. **Not for:** secondary links, nav items, product toolbars.

## Grain overlay

Atmosphere lives on a fixed, non-interactive layer.

```css
.grain {
  position: fixed;
  inset: 0;
  z-index: var(--z-grain, 50);
  pointer-events: none;
  opacity: 0.03;
  /* noise image or SVG filter */
}
```

**When:** brand surfaces that need paper or film. **Not for:** scrolling containers (repaint cost). Honor `prefers-reduced-transparency` by dropping the overlay.

## See also

- [brand-register.md](brand-register.md) — when craft is in scope
- [motion.md](motion.md) — press and hover timing
- [performance.md](performance.md) — blur and grain constraints
