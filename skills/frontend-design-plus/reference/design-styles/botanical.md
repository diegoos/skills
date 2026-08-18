# Botanical

`id=botanical` · `mode=light` · `font=serif`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- Look names a garden, greenhouse, apothecary, or plant-led catalog.
- Brief wants earthbound color, arched frames, and slow plant-like motion.
- Mood overlaps Art Nouveau (Himanshu Bhardwaj / UX Planet): curving lines, floral motifs, earthy palettes.
- Common jobs: wellness, horticulture, and artisan food surfaces that stay sunlit.

When the user did not name this id, skip if the brief wants wabi-sabi clay blobs, or a dark neon canvas.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | fluid |
| density | airy |
| color | committed |
| surface | matte |
| type | serif editorial |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Nature temperature, muted chroma. Forest ink on rice-paper field, sage as the committed hue, terracotta as the action pop. Cream-and-brass craft only when this brief asked for it.

- Warm Alabaster `#F9F8F4` canvas
- Deep Forest `#2D3A31` ink and primary fill
- Sage `#8C9A84` highlights and rings
- Soft Clay `#DCCFC2` secondary wash
- Stone `#E6E2DA` hairline
- Terracotta `#C27B66` action hover
- Card White `#FFFFFF`
- Clay Card `#F2F0EB`

**Type.** High-contrast serif headlines with italic stress on a single word. Humanist sans for body. Prompt options: Playfair Display, Source Sans 3. Scale is large and airy. Buttons use small uppercase with wide tracking.
**Shape.** Soft geometry. Cards near `24px`. Buttons `rounded-full`. Images may use an arch (`rounded-t-full` or a tall radius) or a water-smoothed blob. Vine-like `1px` SVG curves may connect sections.
**Depth.** Forest-tinted shadows at `0.05` alpha, example `0 10px 15px -3px rgba(45, 58, 49, 0.05)`. Fixed paper-grain overlay near `0.015` opacity. Overlay cards may use light backdrop blur.
**Motion.** Honeyed ease-out. Hovers `300ms`, lifts `500ms`, image scale `700ms`. Cards lift `1px` to `2px`. Reduced-motion keeps color and opacity, drops scale and translate.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as forest-green pills with white type, uppercase, and widest tracking. Done when the primary is `rounded-full`, fill `#2D3A31`, and at least `44px` tall.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: cream wellness landing with sage pills and three equal arch cards.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#2D3A31` on `#F9F8F4` for body. Sage `#8C9A84` is for borders and icons. Body-size sage type only after 4.5:1. Terracotta `#C27B66` as hover fill only when the label still clears 4.5:1.
- Focus: `2px` sage ring `#8C9A84` with `2px` offset.
- Touch targets stay `44px`. Honor `prefers-reduced-motion` with color-only feedback.
