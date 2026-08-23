# Swiss Minimalist

`id=swiss-minimalist` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- The brief names International Typographic Style, objective communication, or a visible grid as law.
- Type is the interface. Negative space is structural.
- IxDF minimalism (Laia Tremosa): fewer elements, order, a single piercing signal color.
- Flush-left ragged-right blocks, uppercase display, and thick black rules should be visible at every breakpoint.

Common jobs: museums, transit, architecture, civic systems, and brands that want Helvetica-era clarity.

When the user did not name this id, skip if the brief needs serif editorial, phosphor green, or cinematic motion.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | still |
| density | airy |
| color | restrained |
| surface | ink |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Neutral canvas, restrained signal. Fallback tokens (empty color slots only): `background` `#FFFFFF`, `foreground` `#000000`, `muted` `#F2F2F2`, `accent` `#FF3000`, `border` `#000000`. Swiss red is a stop, a CTA, a hover, a real index. It does not fill decorative bands. Rhythm comes from white versus `#F2F2F2`, not from extra hues.

**Type.** Neutral grotesque sans with a high x-height. Optional sample: Inter as a Helvetica or Akzidenz stand-in, not a required brand stack. Headings uppercase, weight 700-900, tracking tight at large sizes. Labels uppercase, tracking widest. Body 400-500, flush-left, ragged-right. Display may scale from `6xl` toward `9xl` or `10rem` on wide screens. If the briefing named a family, keep it.

**Shape.** Radius `0`. Borders `2px` or `4px` black. Thickness holds on mobile. Inputs are a thick box or a bottom rule that turns `#FF3000` on focus. Icons live in squares or circles as signs, not illustrations.

**Depth.** Flat. No drop shadows. Texture from a 24px grid at ~3% ink, a 16px dot matrix at ~4%, 45° stripes at ~2%, or paper noise at ~1.5%. Apply patterns on white or `#F2F2F2`, not on red or solid black. Depth is pattern, not blur.

**Motion.** Instant and mechanical. `150-200ms` `ease-out` or `ease-linear`. Hover inverts black, white, or red. Plus marks rotate 90°. No spring. Reduced-motion: snap color only.

Primary is black fill, white ink, uppercase, wide tracking. Secondary is a white field with a black rule. Hover may snap to `#FF3000`. Numbers as prefixes are for real sequences only (anti-slop).

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. If occupancy is missing, stop and open [composition.md](../composition.md). Do not name a hero family here. App UI: keep the recipe in [product-register.md](../product-register.md). Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as black rectangles that invert or snap to Swiss red. Done when the primary is radius `0`, uppercase grotesque, black (or red) fill, `2-4px` structure, and hover is a hard color invert rather than an opacity fade.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: Inter-on-white with a red button and fake `01 / 02 / 03` section markers.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: black on white is 21:1. Red text on white must meet AA; prefer red as fill with white ink on CTAs if body-size red fails.
- Focus: `2px` ring in `#FF3000`, `2px` offset, `focus-visible` only.
- Touch targets at least 44×44px (primary height may be `h-16` on small screens). Honor `prefers-reduced-motion` on rotate and slide.
- Keep 4px rules on mobile. Scale type down; keep uppercase and contrast.
