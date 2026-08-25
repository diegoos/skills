# Sketch

`id=sketch` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- Look asks for napkin diagrams, sticky notes, or a work-in-progress wall.
- Brief wants pencil and ink, paper tooth, and annotation (Himanshu Bhardwaj / UX Planet Conceptual Sketch: crosshatch, greyscale, sketch-paper grain).
- IxDF illustration trend applies as hand-drawn personality that still serves the task (Laia Tremosa).
- Common jobs: brainstorming tools, education, and creative journals.

When the user did not name this id, skip if the brief wants machined steel, soft clay extrusion, or a formal serif publication.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | still |
| density | regular |
| color | restrained |
| surface | ink |
| type | one family |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Paper and graphite, restrained. Marker red for correction and primary press. Ballpoint blue for focus and secondary.

- Warm Paper `#fdfbf7` canvas
- Pencil `#2d2d2d` ink and border
- Erased `#e5e0d8` muted
- Marker Red `#ff4d4d` accent
- Ballpoint `#2d5da1` focus
- Post-it `#fff9c4` callout
- Card `#ffffff` plate

**Type.** Handwritten marker for headings, handwritten body that stays legible at `16px`+. Prompt options: Kalam 700, Patrick Hand 400. Scale jumps like notes on a page. Form labels are real words in the body face, set as visible `<label>` text.
**Shape.** Wobbly radii with unequal corners, example `255px 15px 225px 15px / 15px 225px 15px 255px`. Borders `2px` to `4px` in pencil. Dashed borders on secondary frames. Small rotations `1deg` to `2deg` on cards.
**Depth.** Hard offset shadows with zero blur, example `4px 4px 0px 0px #2d2d2d`. Paper tooth via a `#e5e0d8` dot grid at `24px`. Tape bars and tacks are optional collage marks. Pencil arrows, corner ticks, and dashed callouts sit beside content as annotation.
**Motion.** `100ms` snap. Hover jiggles a degree. Active presses the offset to `0` and translates toward the shadow. Reduced-motion keeps the press-flat shadow and drops rotation.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. Do not name a hero family here. Do not reopen composition.md. App UI: keep Packet `recipe=`. Do not open product-register.md from this file. Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as wobbly pencil frames with a hard `4px 4px 0` offset that press flat. Done when shadows are hard offsets, the active state removes the offset, and every input has a visible text label in the DOM.
4. Subtract this Path cliché in Commit. QA owns anti-slop and crit. Done when the common-layout check fails for this style's own cliché: doodle-only UI where form labels are scribbles with no readable names.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#2d2d2d` on `#fdfbf7` for body. White type on `#ff4d4d` fills. Placeholder at 40% pencil only if the label stays visible beside the field.
- Focus: `2px` ballpoint ring `#2d5da1` plus a soft `ring` wash at 20% alpha. Wobbly radius stays on.
- Touch targets stay `44px` (`h-12` or larger). Honor `prefers-reduced-motion` by dropping jiggle rotation.
- Decorative arrows and tape stay `aria-hidden`. Form labels stay in the accessibility tree.
