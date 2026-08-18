# Maximalism

`id=maximalism` · `mode=dark` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- Look asks for dopamine color, stacked type, and joyful overload.
- Brief wants five rotating accents on a cosmic void, thick clash borders, and layered shadows.
- Density is high. Hierarchy still names one primary action.
- Common jobs: campaigns, posters, and hyperpop brand pages that can carry noise.

When the user did not name this id, skip if the brief wants a quiet product shell, restrained neutrals, or a single serif editorial voice.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | wild |
| motion | cinematic |
| density | dense |
| color | drenched |
| surface | ink |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Dark void, drenched chroma. White holds reading. Accents rotate by section (modulo 5). Body type stays white on void.

- Void `#0D0D1A`
- Ink `#FFFFFF`
- Panel `#2D1B4E`
- Magenta `#FF3AF2`
- Cyan `#00F5D4`
- Yellow `#FFE600`
- Orange `#FF6B35`
- Purple `#7B2FFF`

**Type.** Geometric grotesk display, black weight, uppercase headlines. Humanist sans for body. Optional comic display on one callout. Prompt options: Outfit or Unbounded, DM Sans, Bangers or Bungee. Headlines take stacked text-shadow in accent colors at `2px` steps. Body stays `#FFFFFF` at `lg` or `xl`.
**Shape.** Thick borders `4px` default, `8px` on featured frames. Mix solid, dashed, and double inside a section. Cards `24px`, buttons pill, one sharp corner allowed. Clip a single card corner if overlap needs a bite.
**Depth.** Combine glow `0 0 20px rgba(255, 58, 242, 0.5)` with hard stacks `8px 8px 0 #FFE600, 16px 16px 0 #FF3AF2`. Dot grids and stripes layer at low opacity. Patterns stay behind type.
**Motion.** Cinematic. Hover scales toward `1.1` on the primary and shifts shadow offset. Display type stays solid ink or a stacked shadow, not clipped gradient fills. Reduced-motion freezes keyframes and keeps `150ms` color and border changes.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as one pill CTA with a three-stop accent fill, `4px` clash border (example yellow `#FFE600`), and stacked glow plus hard shadow. Done when the view contains exactly one filled primary and that control is at least `44px` tall.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: "more decoration" as the only move (extra stickers with no new hierarchy).

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#FFFFFF` on `#0D0D1A` for body. Accents stay on labels and fills. Dark type `#0D0D1A` on yellow `#FFE600` fills.
- Focus: double ring, `ring-4` plus `ring-offset-4` in two accents that contrast both the control and the void.
- Touch targets stay `44px`. Honor `prefers-reduced-motion` by stopping float, pulse, and gradient-shift loops.
