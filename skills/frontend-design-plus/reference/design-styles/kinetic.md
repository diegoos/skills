# Kinetic

`id=kinetic` · `mode=dark` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- The brief wants type as the surface: festival poster, protest graphic, zine, or IxDF bold typography (Laia Tremosa) brought onto the page.
- Motion must guide (IxDF Animation/Motion): marquee, scroll scale, or hover flood, each with a job.
- Himanshu Bhardwaj / UX Planet Neo-Brutalism mood: large type, stark layout, purposeful asymmetry, usable boldness.
- Display type stays uppercase. Body stays readable sentence case. The scale jump between them is large (about 8-10×).

Common jobs: campaigns, music, cultural brands, and one-pagers whose headline is the image.

When the user did not name this id, skip if the brief is a dense dashboard, quiet luxury, or still product chrome.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | wild |
| motion | cinematic |
| density | airy |
| color | committed |
| surface | ink |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Rich black, committed acid yellow. Fallback tokens (empty color slots only): `background` `#09090B`, `foreground` `#FAFAFA`, `muted` `#27272A`, `muted-foreground` `#A1A1AA`, `accent` `#DFE104`, `accent-foreground` `#000000`, `border` `#3F3F46`. Yellow marks highlights, hover floods, focus, and at most one inverted band. Selection is yellow field, black ink. No extra accent hues. No background gradients.

**Type.** Geometric grotesk built for huge sizes. Optional sample: Space Grotesk. Fallback: a neutral grotesque. Display uppercase, weight 700, tracking tighter, leading `0.8` or none. At least one headline uses fluid clamp (sample: `clamp(3rem, 12vw, 14rem)`). Body stays sentence case at 18-24px. Labels uppercase, tracking wide. Numbers at `6-12rem` in `#27272A` may sit as graphic shapes with `aria-hidden="true"`. If the briefing named a family, keep it.

**Shape.** Radius `0` (rare `2px` on a micro chip). Structural borders `2px` `#3F3F46`. Hairline grids via `gap: 1px` on a muted field. Inputs: extra-tall, bottom rule only, large uppercase text. Content may push toward `95vw`. layout-patterns caps marquees at one per page.

**Depth.** Flat. No drop shadows. Layer muted numerals behind live type. A full-viewport noise overlay at about 3% opacity is enough grain. Solid section flips (black to yellow) replace gradient breaks.

**Motion.** Motion is structure. Hover floods a card to `#DFE104` with black ink in about `300ms`. Buttons scale `1.05` / `0.95`. Scroll may scale or fade a hero. One linear marquee is allowed when the brief asks. Reduced-motion: static stack, no marquee, no parallax; keep the type scale and the flood as an instant color swap.

Sticky stacked cards may overlap on scroll (`top: 8rem`). Outline buttons fill to off-white on hover. Ghost text turns yellow. Two marquees on one page fail anti-slop.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. Do not name a hero family here. Do not reopen composition.md. App UI: keep Packet `recipe=`. Do not open product-register.md from this file. Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as acid-yellow uppercase slabs. Done when the primary is `#DFE104` fill, `#000000` label, radius `0`, height at least 56px, uppercase tight tracking, and hover or active uses scale rather than a glow.
4. Subtract this Path cliché in Commit. QA owns anti-slop and crit. Done when the common-layout check fails for this style's own cliché: generic modern-dark landing with a yellow button and a still, centered hero.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#FAFAFA` on `#09090B` about 15:1. `#DFE104` on the same base about 12:1. Black on yellow about 14:1. `#A1A1AA` meets AA at large sizes; bump it for small body.
- Focus: `2px` yellow ring or bottom rule. Never remove focus to keep the poster look.
- Wrap marquees and scroll transforms in `prefers-reduced-motion: no-preference`. Touch height at least 44px (default button 56px). Decorative numerals stay `aria-hidden`.
- On small screens keep clamp() headlines and show hover-only copy at full opacity.
