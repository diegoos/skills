# Organic

`id=organic` · `mode=light` · `font=serif`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- Look asks for wabi-sabi calm, hand-shaped forms, and forest-floor color (Himanshu Bhardwaj / UX Planet Wabi Sabi: earth, pottery, organic forms).
- Brief wants moss and clay, blob radii, and grain. Botanical arches belong on id=botanical.
- Motion is a slow lift, like picking up a river stone.
- Common jobs: tea, ceramics, and mindful products that stay humble and sunlit.

When the user did not name this id, skip if the brief wants arched greenhouse frames, safety-orange hardware, or cream-and-brass luxury the briefing did not ask for.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | fluid |
| density | airy |
| color | committed |
| surface | matte |
| type | serif editorial |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Warm earth, committed moss. Clay is the second hue. Sand and stone are quiet fields. Cream-and-brass craft only when this brief asked for it.

- Rice Paper `#FDFCF8` canvas
- Loam `#2C2C24` ink
- Moss `#5D7052` primary
- Pale Mist `#F3F4F1` on moss
- Clay `#C18C5D` secondary
- Sand `#E6DCCD`
- Stone `#F0EBE5`
- Timber `#DED8CF` hairline

**Type.** Soft old-style serif for headlines (variable "soft" axis welcome). Rounded-terminal sans for body. Prompt options: Fraunces 600-800, Nunito or Quicksand. Scale is moderate, about 1.25.
**Shape.** Water-worn. Cards `16px` to `24px`, with some corners jumping to `4rem`. Buttons and inputs `rounded-full`. Blob radii such as `60% 40% 30% 70% / 60% 30% 70% 40%` on images and washes. Curved dashed connectors join steps.
**Depth.** Moss-tinted shadow `0 4px 20px -2px rgba(93, 112, 82, 0.15)`. Clay-tinted float `0 10px 40px -10px rgba(193, 140, 93, 0.2)`. Global grain at 3-4% multiply. Blurred moss/clay blobs at low opacity.
**Motion.** `300ms` to `500ms` ease. Buttons scale `1.05` on hover and `0.95` on press. Cards lift `1px` or rotate `1deg`. Images scale over `700ms`. Reduced-motion keeps fill and opacity, drops scale and tilt.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. If occupancy is missing, stop and open [composition.md](../composition.md). Do not name a hero family here. App UI: keep the recipe in [product-register.md](../product-register.md). Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as moss pills with Pale Mist type and a moss-tinted shadow. Done when the primary is `rounded-full`, fill `#5D7052`, type `#F3F4F1`, and at least `44px` tall.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: cream-and-brass spa craft with three equal sage cards.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#2C2C24` on `#FDFCF8` for body. Moss `#5D7052` as fill with `#F3F4F1` type. Muted `#78786C` only where it clears 4.5:1.
- Focus: `2px` moss ring `#5D7052` with `2px` offset, alpha `0.3` wash allowed around the ring.
- Touch targets stay `44px`. Honor `prefers-reduced-motion`. Keep grain opacity low enough that type stays sharp.
