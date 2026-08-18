# Bauhaus

`id=bauhaus` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- The brief names constructivist modernism, 1920s poster geometry, or "form follows function."
- Circles, squares, and triangles compose sections, overlaps, and marks.
- Primary color blocking (red, blue, yellow) plus stark black and white is welcome.
- The page should read as a poster brought into the browser: asymmetric, architectural, graphic.

Common jobs: architecture, product-design, education, and brand systems that want rational structure (Himanshu Bhardwaj / UX Planet: grid, primaries, basic shapes).

When the user did not name this id, skip if the brief needs soft radii, gradients, or a single muted accent.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | still |
| density | regular |
| color | full |
| surface | ink |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Cool-neutral canvas, full primaries. Fallback tokens (empty color slots only): `background` `#F0F0F0`, `foreground` `#121212`, `primary-red` `#D02020`, `primary-blue` `#1040C0`, `primary-yellow` `#F0C020`, `border` `#121212`, `muted` `#E0E0E0`. One hue owns a whole band of surface; the three primaries do not share equal weight on one component. IxDF (Laia Tremosa) and Melanie Daveid: remove noise so line, shape, and color do the work.

**Type.** Geometric sans with circular counters. Optional sample: Outfit. Headlines uppercase, weight 700-900, tracking tight, leading near `0.9`, scaling toward 6xl-8xl on large screens. Body medium weight, relaxed leading. Labels uppercase with widest tracking. If the briefing named a family, keep it and apply this scale and case.

**Shape.** Binary radius: `0` for rectangles, `9999px` for circles. No in-between. Borders `2px` on small screens, `4px` on desktop, always `#121212`. Decorative marks are circle, square, or triangle only. A 45° rotation may appear on a repeating mark, not on body text.

**Depth.** Hard offset shadows with zero blur: `4px 4px 0 #121212` up to `8px 8px 0`. Active press translates `2px` toward the shadow and drops the shadow. A static dot grid or a large geometric plane at 10-20% opacity may texture a section. No gradients, no soft blur.

**Motion.** Mechanical and snappy. `200-300ms` `ease-out`. Button press, card lift of `4-8px`, chevron rotate. Reduced-motion: color and border change only, no translate or scale.

Primary variants rotate the three primaries plus an outline on white. Each major band may take one solid primary as its field. Images may start grayscale and gain color on hover.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as hard-shadow color blocks (square or pill). Done when a primary control uses a primary fill, `2-4px` black border, a 0-blur offset shadow, uppercase geometric sans, and an `:active` press that removes the shadow.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: rounded Tailwind cards with a red-blue-yellow badge strip and a centered hero.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#121212` on `#F0F0F0` is high. White text on `#D02020` and `#1040C0` must stay at or above 4.5:1. Black text on `#F0C020`. Recheck every blocked section.
- Focus: `2px` offset ring in `#121212` (or the section inverse) on `focus-visible`.
- Touch targets at least 44×44px. Shrink shadow and border on small screens (`3px` shadow, `2px` border); keep the geometry and primaries.
- Pair every primary fill with a label or icon so hue is never the only state cue.
