# Retro

`id=retro` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- Look asks for early-web nostalgia, Windows 95 chrome, or GeoCities energy.
- Brief wants beveled controls, system primaries, and tiled grey (overlapping Himanshu Bhardwaj / UX Planet Mid-Century optimism, Memphis chroma, and Y2K throwback mood, executed as 1995-1999 system UI).
- Radius stays zero. Depth is a four-edge bevel.
- Common jobs: throwback tools, archival exhibits, and playful docs that still have real forms.

When the user did not name this id, skip if the brief wants Y2K chrome gloss, Memphis squiggles as the whole language, or a quiet editorial serif.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | contained |
| motion | still |
| density | dense |
| color | full |
| surface | ink |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Full-saturation system colors on button-face grey. Black ink. Classic link blue, visit purple, hover red.

- Face `#C0C0C0` canvas
- Ink `#000000`
- Mid `#808080`
- Link `#0000FF`
- Alert `#FF0000`
- Highlight `#FFFF00`
- Title `#000080`
- Bevel Light `#FFFFFF`

**Type.** System grotesk for body. Heavy display (black grotesk or impact) for headlines, often uppercase. Mono for counters, dates, and stats. Prompt options: Tahoma or Verdana body, Arial Black or Impact display, Courier New mono. Comic Sans only on one decorative chip if the brief asks. Headlines may take a hard `2px 2px 0 #808080` shadow.
**Shape.** `border-radius: 0` on every control and window. Borders `2px`, `4px` on heavy frames. Window title bars use `#000080` (optional gradient to `#1084D0`).
**Depth.** Outset bevel, top and left `#FFFFFF`, bottom and right `#808080`, plus inset `1px` edges `#dfdfdf` / `#404040`. Inset reverses the pair for fields and pressed keys. Tiled 4px hatch on the face grey. Yellow/black 45° stripes only on warning bands.
**Motion.** Still by default. Active translates `1px 1px` and becomes inset. Optional marquee or rainbow type. Reduced-motion freezes marquee and rainbow (solid `#FF0000` is an allowed fallback) and keeps the press bevel.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as 0-radius outset bevels that go inset and translate `1px` when pressed. Done when top/left edges are `#FFFFFF`, bottom/right edges are `#808080`, and every field has a visible text label.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: parody GeoCities page where controls are pictures and labels are missing.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#000000` on `#C0C0C0` for body. White type on `#000080` and on `#0000FF`. Lime `#00FF00` is decoration unless the pair is rechecked.
- Focus: `2px` dotted black outline, `2px` offset (Windows 95 pattern).
- Touch targets stay `44px`. Marquee needs a static accessible name. Honor `prefers-reduced-motion` by stopping rainbow and marquee loops.
