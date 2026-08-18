# Luxury

`id=luxury` · `mode=light` · `font=serif`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- The brief names fashion editorial, house identity, or quiet commerce (Vogue, Hermès, Aesop as a register).
- Himanshu Bhardwaj / UX Planet Luxury Typography: expressive serif, wide tracking on labels, gold as foil, monochrome field.
- Motion must feel slow. Space must feel larger than a product UI.
- Images, paper grain, and hairline rules do the tactile work. Gold stays a highlight.

Common jobs: beauty, fashion, hospitality, and editorial brands that sell restraint.

When the user did not name this id, skip if the brief needs dense tools, phosphor green, or loud poster type.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | cinematic |
| density | airy |
| color | restrained |
| surface | hairline |
| type | serif editorial |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Warm paper, restrained chroma. Fallback tokens (empty color slots only): `background` `#F9F8F6`, `foreground` `#1A1A1A`, `muted` `#EBE5DE`, `muted-foreground` `#6C6863`, `accent` `#D4AF37`, `accent-foreground` `#FFFFFF`. Gold is hover, underline, focus, and small marks. Large gold fields stay out. Dark bands invert to `#1A1A1A` with `#F9F8F6` ink. If color.md category-reflex flags hotel navy-plus-gold or cream-plus-brass as the first idea, keep this paper-and-charcoal ramp and retune the accent from the briefing.

**Type.** High-contrast display serif for headlines and quotes; humanist sans for body and UI. Optional samples: Playfair Display, Inter. Headlines `6xl-9xl`, leading near `0.9`, default or tight tracking. Labels `xs`, uppercase, tracking `0.25-0.3em`. Buttons `xs`, uppercase, tracking `0.2em`. Body 16-18px, relaxed leading, default tracking. Italic of the display face may mark one word in a headline. If the briefing named a family, keep it.

**Shape.** Radius `0`. Rules are `1px` `#1A1A1A`, often a single edge (`border-t`) rather than a full box. Dividers are `1px` lines. Inputs are underline-only. Gold `4px` top rule may mark a featured tile.

**Depth.** Soft layered shadow, low opacity: images about `0 8px 32px rgba(0,0,0,0.12)`, cards `0 2px 8px rgba(0,0,0,0.02)` deepening on hover. Inset `1px` frame on photos. Paper noise overlay at about 2% opacity. Images start grayscale and ease to color over `1500-2000ms` with a slight scale.

**Motion.** Cinematic. Buttons and color `500-700ms`, custom ease `cubic-bezier(0.25, 0.46, 0.45, 0.94)`. Primary hover may slide a gold layer from the left. Reduced-motion: keep color swaps, drop translate, scale, and the long grayscale fade.

Section padding sits near `py-24` to `py-32`. Offset columns (`col-start-2` or `col-start-6`) beat a 50/50 split. Vertical side labels (`writing-mode: vertical-rl`) may mark a photo on desktop.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as charcoal rectangles whose hover reveals gold. Done when the primary is `#1A1A1A` fill, uppercase tracked label, radius `0`, height at least 48px, and hover either fills gold or inverts through a 500ms ease with no rounded corners.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: cream-and-brass craft landing (beige field, gold ornaments, centered serif hero).

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#1A1A1A` on `#F9F8F6` is about 12.6:1 (AAA). `#6C6863` on paper about 4.8:1 (AA). `#D4AF37` on charcoal about 5.2:1 (AA for accents).
- Focus: `focus-visible` gold bottom border on inputs; `ring-1` `#1A1A1A` or gold on controls. Keep a visible indicator.
- Honor `prefers-reduced-motion` by cutting image duration to 0 and dropping scale. Touch height at least 48px (`h-12`).
- Left-align body text. Keep gold off large text blocks so contrast stays on charcoal and alabaster.
