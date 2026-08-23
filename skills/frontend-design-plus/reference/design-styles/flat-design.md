# Flat Design

`id=flat-design` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- The brief wants schematic, digital-native UI: solid color, type, and geometry, with no fake 3D.
- IxDF Flat Design (Laia Tremosa): bright color, even-stroke type, no decorative shadow. Flat 2.0 affordance comes from color shift and scale.
- Sections read as poster blocks: white, muted gray, or a full primary field.
- Interactive targets must stay obvious through fill change and size, including on touch devices.

Common jobs: consumer apps, campaigns, and marketing that need speed and graphic clarity.

When the user did not name this id, skip if the brief needs skeuomorphic depth, phosphor terminal, or cinematic blur. `you-decide` and invent-all skip this id unless the user named it.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | contained |
| motion | still |
| density | regular |
| color | full |
| surface | matte |
| type | one family |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** High-key, full hierarchy of hues. Fallback tokens (empty color slots only): `background` `#FFFFFF`, `foreground` `#111827`, `primary` `#3B82F6`, `secondary` `#10B981`, `accent` `#F59E0B`, `muted` `#F3F4F6`, `border` `#E5E7EB`. Primary owns action. Secondary and amber support, never equal weight on one control. Color blocks define sections. Edges are fill, not line, except where an input or FAQ needs a `2px` rule.

**Type.** Geometric sans that matches the rectangles and circles. Optional sample: Outfit. Headings 700-800, tracking about `-0.02em`. Body 400. Labels and buttons 500-600, often uppercase with wider tracking. If the briefing named a family, keep it. Hierarchy is size and weight, not shadow.

**Shape.** Radius `6-8px` on controls and cards, consistent. Pills only on tags. Circles hold icons (`56-64px`). Outline buttons may use a `4px` solid rule. Large background circles or rotated squares at low opacity may decorate a band.

**Depth.** Z-axis off. `shadow-none` on components. Flat 2.0: hover darkens or lightens the fill, scales a button to `1.05`, a card to about `1.02`, an icon to `1.10`. A muted-to-transparent wash may tint a background only, never a button. No backdrop blur.

**Motion.** Digital and snappy. `200ms` for most, `300ms` for larger scale. Fill on outline hover. Reduced-motion: color change only, scale `1`.

Secondary sits on `#F3F4F6` and darkens on hover. Outline buttons use a thick solid rule and fill on hover. Icons live in solid circles. Alternate section fields (white, muted, primary, emerald, amber) without hairline dividers.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. If occupancy is missing, stop and open [composition.md](../composition.md). Do not name a hero family here. App UI: keep the recipe in [product-register.md](../product-register.md). Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as solid primary rectangles with white labels. Done when the primary uses `#3B82F6` (or the mapped primary), radius `6-8px`, height at least 56px, no box-shadow, and hover is a darker fill plus scale (or color only under reduced-motion).
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: Material floating cards or a Bootstrap three-column icon grid with drop shadows.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#111827` on white is strong. White on `#3B82F6` must meet AA. Recheck white on `#10B981` and `#F59E0B`; darken those fills or switch to dark ink if a pair fails.
- Focus: `ring-2 ring-offset-2` in primary (sample `ring-blue-500`). The ring replaces shadow as the affordance for keyboard users.
- Touch height `h-14` to `h-16` on primaries. Pair hue with icon or label so color is never the only state cue.
- Recheck white-on-amber and white-on-emerald at button size. Darken the fill or switch to `#111827` ink when a pair fails AA.
