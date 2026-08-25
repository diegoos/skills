# Academia

`id=academia` · `mode=dark` · `font=serif`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- Scene is a library at night, a college archive, a leather study, or a manuscript desk.
- Brief wants scholarly gravitas, brass hardware, crimson seals, and serif reading type.
- Look names drop caps, Roman volume marks, arch-top portraits, or engraved metal.
- This path is Dark Magic Academia (mahogany, brass, crimson). Light Academia cream-and-sunlight is a different id.

Common jobs: publishers, universities, rare-book shops, and research products that should feel like rooms of paper.

When the user did not name this id, skip if the brief wants a sunlit cream campus (Light Academia).

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | contained |
| motion | fluid |
| density | airy |
| color | committed |
| surface | hairline |
| type | serif editorial |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Warm dark wood, parchment ink, one brass metal, crimson used as a seal. Brass is the interactive language. Crimson is a wax seal and a rare hover.

Fallback tokens (empty color slots only):

- mahogany `#1C1714`
- oak `#251E19`
- parchment `#E8DFD4`
- leather `#3D332B`
- faded ink `#9C8B7A`
- wood grain `#4A3F35`
- brass `#C9A962`
- crimson `#8B2635`
- brass highlight `#D4B872`
- brass shade `#B8953F`

**Type.** Serif editorial throughout. Display old-style for titles (optional Cormorant Garamond). Book serif for body at 16-18px, leading 1.625 (optional Crimson Pro).
Small-caps engraved labels with tracking `0.2em`-`0.3em` (optional Cinzel). Italic for emphasis. Drop cap on the opening paragraph of a major fold, brass, Cinzel-scale.
**Shape.** Radius `4px` on controls and cards. Arch-top on featured images (`40% 40% 0 0 / 20% 20% 0 0`). Brass corner brackets on major frames.
Ornate divider as a short brass-centered hairline. Primary is a 48px brass plate, small-caps tracking `0.15em`. Field is 48px oak fill, 1px wood-grain border, brass on focus.
**Depth.** Oak `#251E19` on mahogany `#1C1714`. Soft warm shadow `0 8px 24px` at 30% black on hover. Inset highlight on brass (`1px` light over `1px` dark).
Paper grain near 3% and a mild vignette. Images may start at `sepia(0.6)` and warm to full color over 700ms. Engraved text-shadow on brass labels.
**Motion.** Weighted and slow. 150ms press, 300ms border, 500-700ms image. Ease-out. Hover brightens brass to 110%.
Reduced-motion keeps brass fill and full-color images, and drops scale and long filters.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. Do not name a hero family here. Do not reopen composition.md. App UI: keep Packet `recipe=`. Do not open product-register.md from this file. Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as brass plates. Done when the primary uses the brass fill (or the three-stop brass gradient), dark ink `#1C1714` on brass, radius `4px`, height ≥48px, and small-caps tracking.
4. Subtract this Path cliché in Commit. QA owns anti-slop and crit. Done when the common-layout check fails for this style's own cliché: generic dark-serif luxury with cream-and-brass craft.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: Parchment `#E8DFD4` on `#1C1714` at ≥4.5:1 (this pair is near 8.5:1). Faded ink `#9C8B7A` only when it still clears AA. Dark mahogany on brass for button labels.
- Focus: 2px `#C9A962` ring, 2px offset, offset color `#1C1714`.
- Touch and dark luminance: Targets ≥48px on primary actions. Keep warm off-black wood `#1C1714`. Body stays parchment `#E8DFD4`. Honor reduced-motion on sepia and shimmer.
- Flourishes, dividers, and wax seals are `aria-hidden="true"`. Form labels stay visible Cinzel small-caps above the field.
