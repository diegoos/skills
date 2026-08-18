# Industrial

`id=industrial` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- Look asks for a control panel, instrument, or workshop object with honest materials.
- Brief names matte ABS, powder-coated steel, or safety orange on a cool grey chassis (Himanshu Bhardwaj / UX Planet Utilitarian mood: function-first, muted, grid-mounted).
- IxDF skeuomorphism (Laia Tremosa) applies only where it teaches the control, such as a pressable key. Materials stay ABS, steel, and safety orange.
- Common jobs: hardware, manufacturing, and tools that should feel bolted down.

When the user did not name this id, skip if the brief wants frosted glass, soft same-surface clay, a navy corporate landing, or a software-engineer work page. `you-decide` and invent-all skip this id unless the user named it.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | contained |
| motion | fluid |
| density | regular |
| color | restrained |
| surface | matte |
| type | one family |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Cool workshop light. Chassis grey dominates. Safety orange is the stop and the trigger, used sparingly. Dark charcoal panels may invert for technical strips.

- Chassis `#e0e5ec` Level 0
- Panel `#f0f2f5` raised
- Recessed `#d1d9e6` wells
- Ink `#2d3436`
- Label `#4a5568`
- Safety Orange `#ff4757`
- Shadow `#babecc`
- Highlight `#ffffff`

**Type.** Humanist sans for UI. Category first. Prompt may list Inter. Use the project sans when one already exists. Mono stamps numerals, badges, and uppercase metadata. Prompt options: JetBrains Mono, Roboto Mono. Labels track `0.05em` to `0.08em`. Headlines may take a `1px` white emboss.
**Shape.** Injection-molded radii: `8px` controls, `16px` panels, `24px` bezels, full circles for LEDs. Manufacturing marks (corner screws, vent slots) earn their place on bolted modules.
**Depth.** One light source, top-left at 45°. Dual shadows follow that vector, example `8px 8px 16px #babecc, -8px -8px 16px #ffffff`. Recessed wells invert the pair. Matte plastic noise on the chassis. Physical materials, not glass.
**Motion.** Mechanical. Press `150ms` with `translateY(2px)` and inset inversion. Hover lift `300ms`. Easing may overshoot slightly, `cubic-bezier(0.175, 0.885, 0.32, 1.275)`. Reduced-motion snaps to pressed or rest with no bounce.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as safety-orange physical keys under the 45° light, white type, uppercase tracking. Done when active inverts to inset shadow, rest uses the top-left highlight, and the DOM shows a pressable `button` at least `44px` tall.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: charcoal-and-orange developer portfolio with a fake terminal hero.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#2d3436` on `#e0e5ec` for body. White `#ffffff` on `#ff4757`. Label `#4a5568` only where it clears 4.5:1.
- Focus: `2px` orange ring `#ff4757` with `2px` offset on the chassis.
- Touch targets stay `44px` (prompt prefers `48px` on mobile). Dark panels `#2d3436` use light type `#e0e5ec` or `#ffffff`. Honor `prefers-reduced-motion`.
