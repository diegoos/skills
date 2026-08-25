# Material Design

`id=material-design` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- Brief asks for a Google-like system, Material You, or tonal surfaces from a seed color.
- Product UI needs ink-on-paper roles, elevation, and pill actions that feel tactile.
- Look names adaptive color, filled text fields, or a FAB as the primary create action.
- IxDF places Material with the 2012 flat wave (Windows 8, iOS 7, Material) and Flat 2.0 affordances (subtle elevation so controls read as pressable).

Common jobs: teams shipping app chrome, forms, and sheets that must stay consistent across screens.

When the user did not name this id, skip if the brief wants sharp ink posters. `you-decide` and invent-all skip this id unless the user named it.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | briefing owns |
| motion | fluid |
| density | regular |
| color | committed |
| surface | matte |
| type | one family |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Tonal light, seed-driven. Surfaces step by lightness. One primary plus a quieter secondary container and a dusty tertiary. Map roles as surface, on-surface, primary, on-primary.

Fallback tokens (empty color slots only; violet seed):

- surface `#FFFBFE`
- on-surface `#1C1B1F`
- primary `#6750A4`
- on-primary `#FFFFFF`
- secondary-container `#E8DEF8`
- on-secondary-container `#1D192B`
- tertiary `#7D5260`
- surface-container `#F3EDF7`
- surface-container-low `#E7E0EC`
- outline `#79747E`
- on-surface-variant `#49454F`

**Type.** One humanist sans for the whole UI. Optional face: Roboto at 400 / 500 / 700. Display around 56px, headlines 32-48px, body 16-20px, labels 12-14px with slight positive tracking.
Medium weight on titles. Regular on body. Label tracking about `0.01em`. This is a system path. Keep one family even when the layout family changes.
**Shape.** Pills on buttons, chips, and badges (`9999px`). Cards 24px. Sheets and dialogs 28px. Hero enclosures up to 48px.
Filled inputs round 12px on top and square on the bottom with a 2px underline. FAB is 56×56px at 28px radius (square) or full (round). Padding on pills is generous (`24px`-`32px` inline).
**Depth.** Elevation tokens 0-3. Resting cards at a small soft shadow. Hover steps one elevation. Modals sit highest. Surface-container on surface does the separation work.
State layers are opacity on the same ink (90% hover, 80% pressed on fills; 10% / 5% on ghosts). Outline `#79747E` at 1px when a stroke is required.
**Motion.** `cubic-bezier(0.2, 0, 0, 1)`, 200ms micro, 300ms surfaces, 400-500ms sheets. Press scale about 0.95. Ripple is optional motion on press.
Reduced-motion keeps color/opacity state layers and drops scale, translate, and ripple.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. Do not name a hero family here. Do not reopen composition.md. App UI: keep Packet `recipe=`. Do not open product-register.md from this file. Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as pill filled actions with state-layer ink. Done when every primary `<button>` is `border-radius: 9999px` (FAB may be 28px), hover changes fill opacity not hue, and a filled field uses a 2px primary underline on focus.
4. Subtract this Path cliché in Commit. QA owns anti-slop and crit. Done when the common-layout check fails for this style's own cliché: purple mesh glow with three equal cards.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: On-surface `#1C1B1F` on `#FFFBFE` at ≥4.5:1. White on `#6750A4` for filled labels. Outline `#79747E` at ≥3:1 against neighboring surfaces.
- Focus: 2px primary ring, 2px offset, on the surface token.
- Touch and motion: Targets ≥44px (default button 40-48px, FAB 56px). Honor `prefers-reduced-motion` by keeping state-layer color and removing scale.
- Decorative blur blobs, if used, stay `aria-hidden="true"` and sit behind content. Tonal steps remain visible without those blobs.
