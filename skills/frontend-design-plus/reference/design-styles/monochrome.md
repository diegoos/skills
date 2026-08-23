# Monochrome

`id=monochrome` · `mode=light` · `font=serif`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- The brief asks for austere editorial, fashion catalog, gallery, or museum-catalog authority with no chroma.
- Type, scale, and negative space must carry drama.
- Black and white inversion is the only emphasis tool.
- The look matches a fashion cover, an architectural monograph, or a gallery wall: stark, timed, and still.

Common jobs: a reader who expects a publication of record or a luxury house identity.

When the user did not name this id, skip if the brief needs a brand hue, friendly rounding, or playful motion.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | still |
| density | airy |
| color | restrained |
| surface | hairline |
| type | serif editorial |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Neutral, high-key, restrained. Black is the accent. Fallback tokens (empty color slots only): `background` `#FFFFFF`, `foreground` `#000000`, `muted` `#F5F5F5`, `mutedForeground` `#525252`, `accent` `#000000`, `accentForeground` `#FFFFFF`, `border` `#000000`, `borderLight` `#E5E5E5`. Gray only on secondary text and light dividers. IxDF minimalism (Laia Tremosa) backs this with fewer elements and active negative space.

**Type.** Display serif is the surface (IxDF bold typography). Body stays a readable text serif. Optional examples from the sample system: Playfair Display for display, Source Serif 4 for body. If the briefing already named a family, keep it. Headlines track tight (`-0.025em` to `-0.05em`) and can reach 8xl-9xl on desktop. Body at 16-18px with relaxed leading. Labels use small caps or widest tracking. A monospace face may mark dates and metadata only.

**Shape.** Radius `0` on every control, card, and input. Structure comes from rules: hairline `1px` `#E5E5E5`, thin `1px` black, medium `2px`, thick `4px`, ultra `8px`. Icons stay outlined at 1-1.5px stroke.

**Depth.** Flat plane. No drop shadows. Hierarchy from inversion (black field, white ink), rule weight, type scale, and space. A near-invisible paper grain or hairline stripe (opacity about `0.015`) may sit on the canvas so the field does not read as empty CSS.

**Motion.** Instant state change. Transitions `0-100ms`. Hover inverts fill and ink or thickens a rule. Reduced-motion: the same inversion and border change with `transition: none`.

Primary buttons stay rectangular, uppercase, wide-tracked. Ghost actions underline on hover. Thick `4px` or `8px` black rules separate major bands.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. If occupancy is missing, stop and open [composition.md](../composition.md). Do not name a hero family here. App UI: keep the recipe in [product-register.md](../product-register.md). Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as sharp ink rectangles that invert on hover. Done when every primary button has `border-radius: 0`, black fill with white label (or the inverse), uppercase wide tracking, and hover swaps fill and ink within 100ms.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: grayscale SaaS landing (centered hero, three equal cards, sans-on-slate with chroma stripped).

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: black on white is 21:1 (AAA). Keep secondary gray at or above 4.5:1 on its surface.
- Focus: `3px` solid black outline, `2-3px` offset, `focus-visible` only. Inputs thicken the ink border to `3-4px` instead of a colored ring.
- Touch targets stay at least 44×44px. Oversized headlines scale down on small viewports; the sharp corners and inversion stay.
- Skip links render as a visible black rectangle at the top of the document.
