# Claymorphism

`id=claymorphism` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- Brief wants inflated vinyl, marshmallow UI, or a candy-shop object you could pinch.
- Look names plump radii, pastel canvas, and stacked soft shadows (outer plus inset).
- Product is playful, kids, lifestyle, or a campaign that should feel safe and tactile.
- IxDF warns that soft extruded UI (neumorphism) needs extra type, space, and contrast. Clay is inflated volume. Same a11y bar.

Common jobs: visitors who should read the label as clearly as they feel the bulge.

When the user did not name this id, skip if the brief wants flat ink posters.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | briefing owns |
| motion | fluid |
| density | regular |
| color | full |
| surface | matte |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Cool lavender paper with candy solids. Violet is the action. Pink, sky, emerald, and amber support orbs and states.

Fallback tokens (empty color slots only):

- canvas `#F4F1FA`
- charcoal `#332F3A`
- muted `#635F69`
- violet `#7C3AED`
- light violet `#A78BFA`
- pink `#DB2777`
- sky `#0EA5E9`
- emerald `#10B981`
- amber `#F59E0B`
- pressed well `#EFEBF5`

**Type.** Rounded grotesk display at 700-900, tight tracking on large titles. Humanist sans body at 16-18px, medium weight, leading 1.625. Optional display face: Nunito. DM Sans stays optional.
Small labels wide tracking. Body floor is `#635F69`. Display uses `#332F3A`.
**Shape.** Plump radii. Buttons and fields ≥20px. Cards ~32px. Large shells 48-60px. Nested image 8px tighter than its card. Circles for stat orbs.
Primary is 56px, radius ≥20px, violet fill (`#A78BFA` to `#7C3AED`). Field is 64px, `#EFEBF5`, inset clay stack, white raise on focus.
**Depth.** Inflated clay via four-layer stacks (soft colored drop, top-left white highlight, faint inner tint, inner rim). Pressed wells use inset `#d9d4e3` / white.
Volume is the material. Matte paint. A 1px edge or darker fill marks the control even if the shadow stack is faint.
**Motion.** Squish physics. Hover lifts 4-8px and thickens the outer shadow. `:active` scales near 0.92 and swaps to the inset stack. Blobs may drift 8-12s if motion is cinematic.
Reduced-motion keeps the resting clay stack and drops lift, squish, breathe, and drift.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. If occupancy is missing, stop and open [composition.md](../composition.md). Do not name a hero family here. App UI: keep the recipe in [product-register.md](../product-register.md). Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as plump clay. Done when the primary uses the violet fill (or `#A78BFA` to `#7C3AED`), radius ≥20px, height ≥44px, a four-layer outer stack at rest, and an inset stack on `:active`.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: three equal plump cards on a gray soft-UI field.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: Body `#332F3A` or `#635F69` on `#F4F1FA` at ≥4.5:1. Secondary text stays at `#635F69` or darker. White on `#7C3AED` for pill labels. Recheck every pastel pair. Soft UI needs extra contrast because shadows alone do not mark a control.
- Focus: 4px violet ring at 30% `#7C3AED`, 2px offset, plus a darker fill or 1px edge so the target reads without the shadow stack.
- Touch and motion: Targets ≥44px (prefer 56px on primary). Honor `prefers-reduced-motion` on blob drift and squish. Pair hue with an icon or label on emerald and amber states.
