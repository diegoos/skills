# Neumorphism

`id=neumorphism` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- Look asks for soft extruded UI, molded clay, or a single continuous surface.
- Brief wants cool grey, dual opposing shadows, and convex or concave controls (Michał Malewicz, "new skeuomorphism"; Laia Tremosa / IxDF Soft UI).
- Depth is the craft. Color stays almost monochrome aside from a spare violet accent.
- Common jobs: calm utilities, wellness tools, and tactile marketing that can afford extra type contrast.

When the user did not name this id, skip if the brief wants hard bevels, neon void, or a high-chroma product shell.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | contained |
| motion | fluid |
| density | airy |
| color | restrained |
| surface | matte |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Cool monochrome clay. Shadows do the drawing. Violet is the accent for CTA and focus. Teal is success only.

- Cool Clay `#E0E5EC` canvas and cards
- Ink `#3D4852`
- Muted `#6B7280`
- Violet `#6C63FF` accent
- Violet Light `#8B84FF` hover
- Teal `#38B2AC` success
- Light shadow `rgba(255, 255, 255, 0.5)`
- Dark shadow `rgba(163, 177, 198, 0.6)`

**Type.** Geometric sans for display, humanist sans for body. Prompt options: Plus Jakarta Sans, DM Sans. Headlines 700-800 with tight tracking. Body 400-500. Ink `#3D4852` on clay is the default pair.
**Shape.** Pillowed. Cards `32px`, buttons `16px`, inner wells `12px` or full pill. Edges come from shadows only.
**Depth.** Extruded rest `9px 9px 16px rgba(163,177,198,0.6), -9px -9px 16px rgba(255,255,255,0.5)`. Press and inputs use inset, deep wells `inset 10px 10px 20px`. Nested Extruded, then Inset, then Extruded is the signature stack. Cards share the page clay `#E0E5EC`.
**Motion.** `300ms` ease-out on shadow and `translateY`. Hover lifts `1px` and widens the pair. Active drops into inset. Ambient float keyframes pause under reduced-motion.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as same-surface extrusions that go inset on press, violet fill `#6C63FF` on the filled variant. Done when rest uses the dual rgba pair, active uses inset, and the label already passes 4.5:1 before any shadow is applied.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: low-contrast grey pills whose edges exist only as blur.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: IxDF warning is in force. Neumorphism's low contrast and dark-mode luminance are a known trap (Laia Tremosa / IxDF; Malewicz Soft UI). Body uses `#3D4852` on `#E0E5EC` (target 7.5:1). Muted `#6B7280` only at AA. Shadows add depth after those pairs pass. A dark-theme port needs a separate high-contrast clay palette before shadows return.
- Focus: `2px` violet ring `#6C63FF` with `2px` offset on `#E0E5EC`.
- Touch targets stay `44px`. Honor `prefers-reduced-motion` by snapping extruded and inset states with no float loop.
