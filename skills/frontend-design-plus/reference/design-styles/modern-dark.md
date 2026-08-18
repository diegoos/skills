# Modern Dark

`id=modern-dark` · `mode=dark` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- The brief wants premium developer-tool or night-session product chrome (Linear, Vercel, Raycast as a register).
- Users stay on-screen for long stretches. IxDF dark mode (Laia Tremosa): dark gray bases, bright off-white text.
- Depth comes from layered translucency and one indigo accent.
- Hover and focus must feel like desktop software: small moves, fast easing, visible rings.

Common jobs: tools, dashboards, and marketing that must feel like software at night.

When the user did not name this id, skip if the scene is daylight, phosphor-green terminal, or poster-scale type. `you-decide` and invent-all skip this id unless the user named it.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | fluid |
| density | regular |
| color | committed |
| surface | hairline |
| type | one family |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Cool near-black, committed indigo. Fallback tokens (empty color slots only): `background-deep` `#020203`, `background-base` `#050506`, `background-elevated` `#0a0a0c`, `foreground` `#EDEDEF`, `foreground-muted` `#8A8F98`, `accent` `#5E6AD2`, `accent-bright` `#6872D9`, `border-default` `rgba(255,255,255,0.06)`. Surfaces sit at `rgba(255,255,255,0.05)` and rise to `0.08` on hover. Accent is for action, links, and a restrained glow. Most of the UI stays monochrome. If category-reflex fires on indigo-as-SaaS, keep the near-black ramp and retune the accent from the briefing.

**Type.** One humanist or geometric sans for display and body. Optional sample: Inter or Geist Sans. Display semibold with tracking about `-0.03em`. Body regular, relaxed leading. Labels may use a monospace at `xs` with widest tracking. Headlines may use a vertical fade from `#EDEDEF` toward 70% white as a fill. Skip gradient-clip rainbow text.

**Shape.** Large shells `16px` radius, buttons and inputs `8px`, pills full-round. Hairline borders at 6-10% white. Inputs use a darker well (`#0F0F12`) and an accent border on focus.

**Depth.** Elevation by stacked light, not a single drop. Combine a 1px light edge, a soft dark diffuse, and an optional accent glow at low opacity. A faint noise (`~0.015`) and a 64px grid at `0.02` may sit behind chrome. Ambient pools of accent at 10-25% opacity are material, not a hero illustration. Raised surfaces go lighter (`#0a0a0c` over `#050506`), per the skill dark-mode rule.

**Motion.** Precise software: `200-300ms`, expo-out `[0.16, 1, 0.3, 1]`. Hover moves `4-8px` or scales `0.98-1.02`. Reduced-motion: opacity and border only; freeze parallax and floating light.

Secondary controls use `rgba(255,255,255,0.05)` fill and brighten to `0.08`. Ghost controls stay transparent until hover. Cards may track a 300px accent spotlight at 15% opacity when the brief asks for cinematic light.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as accent fills with a multi-layer glow and a 1px inset highlight. Done when the primary button uses `#5E6AD2` (or the mapped accent), off-white label, `8px` radius, hover to `#6872D9`, and `:active` at `scale(0.98)`.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: centered hero on a dark mesh with purple or indigo glow and three equal glass cards.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#EDEDEF` on `#050506` is about 15:1. `#8A8F98` on the same base is about 6:1. Interactive accent on dark must stay at or above 4.5:1.
- Focus: `ring-2` at `accent/50`, `ring-offset-2` on `#050506`.
- Long-session luminance: keep bases near `#050506` / `#020203`. Soften body text off pure white. Honor `prefers-reduced-motion` on blobs, parallax, and shine sweeps.
- Raised surfaces go lighter than the canvas. Recheck every text pair after the theme tokens land.
