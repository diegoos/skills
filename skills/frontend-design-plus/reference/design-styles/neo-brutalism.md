# Neo Brutalism

`id=neo-brutalism` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- Brief wants raw honesty, zine energy, sticker collage, or a loud anti-smooth brand.
- Look names thick black strokes, highlighter blocks, hard offset shadows, or slight sticker rotation.
- Product can stay usable while it shouts (agency, magazine, campaign, playful tool).
- UX Planet Neo-Brutalism keeps raw honesty and adds usable UI (bold yet functional).

Common jobs: a visitor who wants punch and still needs to tap, read, and submit.

When the user did not name this id, skip if the brief wants quiet tonal product chrome.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | still |
| density | dense |
| color | full |
| surface | ink |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Paper canvas with unmixed paint. Black is structure. Cream is the field for this path (newsprint, not generic warmth). Red, yellow, and violet take turns as solid blocks.

Fallback tokens (empty color slots only):

- canvas `#FFFDF5`
- ink `#000000`
- hot red `#FF6B6B`
- vivid yellow `#FFD93D`
- soft violet `#C4B5FD`
- white `#FFFFFF`

**Type.** Grotesk display, heavy weights (700-900). Headlines tight tracking and often uppercase. Labels wide tracking. Body stays bold and readable at 18px+.
Optional face: Space Grotesk. Hollow stroke display (`text-stroke` 2px ink with transparent fill) is a signature on one hero word. Body stays solid ink.
**Shape.** Radius `0` on frames. Full pills only on stickers and badges. Default border `4px` solid ink. `2px` for ghosts. `8px` for a hero frame.
Small rotations (`1deg`-`3deg`) on a few stickers. Primary is a sharp 44-56px plate, uppercase, 4px ink border. Field is 56px+ with a 4px ink border.
**Depth.** Hard offset shadows with zero blur: `4px 4px 0 #000`, `8px 8px 0 #000`, `12px 12px 0 #000`. On black bands, a white offset is allowed.
Halftone dots, graph-paper lines, or grain on the canvas. Overlap a badge like a sticker. Color-block sections (cream, yellow, violet, black) for rhythm.
**Motion.** Snappy mechanical press. 100ms on buttons, 200ms on cards. `:active` translates the control onto its shadow. Hover lifts a card and grows the offset.
Reduced-motion keeps the press color and the hard shadow at rest and drops bounce, spin, and translate.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. If occupancy is missing, stop and open [composition.md](../composition.md). Do not name a hero family here. App UI: keep the recipe in [product-register.md](../product-register.md). Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as ink-framed push plates. Done when the primary has a 4px black border, a 4-8px zero-blur offset shadow, height ≥44px, uppercase label, and `:active` covers the shadow.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: three equal bordered feature cards.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: Ink `#000000` on `#FFFDF5`, `#FFD93D`, and `#C4B5FD` at ≥4.5:1. White on `#000000` or `#FF6B6B` for inverted labels. Recheck red-on-cream at small sizes.
- Focus: 2px black ring with 2px offset, or a yellow `#FFD93D` fill plus the same ring on fields.
- Touch: Every control ≥44px with ≥8px gap. Keep the loud craft and the hit area. Reduced-motion holds color blocking and stills the sticker wiggle.
- Icons use a 3-4px stroke inside an ink box. Icon-only controls get a visible name.
