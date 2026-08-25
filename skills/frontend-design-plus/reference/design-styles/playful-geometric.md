# Playful Geometric

`id=playful-geometric` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- Brief wants Memphis energy, a sticker book, a playground, or cleaned-up 80s geometry.
- Look names primitive shapes, squiggles, polka grids, hard offset shadows, and mixed radii.
- Copy and forms stay readable while decoration runs around them.
- UX Planet Memphis mood is youthful and quirky. Squiggles, bright primaries, grids, and block shapes. Mixed-span modules are allowed only when the briefing picks that family.

Common jobs: kids products, events, creative brands, and campaigns that should invite a tap.

When the user did not name this id, skip if the brief wants austere Swiss posters.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | fluid |
| density | regular |
| color | full |
| surface | ink |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Warm paper with a confetti of solids. Violet is the action color. Pink, amber, and mint rotate on shapes and emphasized words.

Fallback tokens (empty color slots only):

- paper `#FFFDF5`
- ink `#1E293B`
- mute field `#F1F5F9`
- mute text `#64748B`
- violet `#8B5CF6`
- pink `#F472B6`
- amber `#FBBF24`
- mint `#34D399`
- line `#E2E8F0`
- white `#FFFFFF`
- field line `#CBD5E1`

**Type.** Geometric grotesk display at 700-800. Humanist geometric body at 400-500. Scale about 1.25. Category first. Outfit and Plus Jakarta Sans stay optional.
Labels small, uppercase, wide tracking. Body ink is `#1E293B` at 16px+.
**Shape.** Chunky 2px ink borders. Radii 8 / 16 / 24px plus full pills. Mix a sharp corner with three round ones for a leaf or speech-blob.
Circles, triangles, and squiggles sit behind type with padding so copy stays clear. Primary is a 48px pill, violet fill, 2px `#1E293B` border. Field is 48px, 2px `#CBD5E1`, violet hard shadow on focus.
**Depth.** Hard offset `4px 4px 0 #1E293B` at rest, `6px 6px 0` on hover, `2px 2px 0` on press. Featured stickers may offset in `#F472B6` or `#E2E8F0`.
Dot grids and stripe fills inside shapes. Icons live inside a colored circle.
**Motion.** Bouncy overshoot `cubic-bezier(0.34, 1.56, 0.64, 1)` at 300ms. Controls lift against the shadow. Icons may wiggle a few degrees. Entrance can pop scale 0 to 1.
Reduced-motion keeps the 2px border and hard shadow at rest and drops wiggle, bounce, and pop.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. Do not name a hero family here. Do not reopen composition.md. App UI: keep Packet `recipe=`. Do not open product-register.md from this file. Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as candy stickers. Done when the primary is a pill, 2px `#1E293B` border, violet `#8B5CF6` fill, 4px zero-blur offset, and height ≥48px, with press shrinking the offset.
4. Subtract this Path cliché in Commit. QA owns anti-slop and crit. Done when the common-layout check fails for this style's own cliché: three equal sticker cards on a cream SaaS grid.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#1E293B` on `#FFFDF5` or `#FFFFFF` for body. White on `#8B5CF6` for pill labels. Mute `#64748B` only at ≥4.5:1. Pair each confetti hue with a label or shape.
- Focus: 2px violet border plus a 4px `#8B5CF6` hard shadow on the field.
- Touch and motion: Targets ≥48px. Floaters that would cover copy on small screens stay off. `prefers-reduced-motion` stills bounce and wiggle.
- Each confetti hue sits with a label or a primitive. Icons use a 2.5px stroke inside a filled circle.
