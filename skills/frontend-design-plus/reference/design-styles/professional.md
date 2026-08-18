# Professional

`id=professional` · `mode=light` · `font=serif`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- Look asks for editorial trust, literary warmth, or classical restraint on a light canvas.
- Brief names a publication, studio, counsel, or heritage product that should read like a well-set book.
- Accent budget is one warm metal used on actions and hairline rules.
- Common jobs: readers who stay for long copy and quiet authority.

When the user did not name this id, skip if the brief wants neon, bevel chrome, or a dense app shell with no serif voice. `you-decide` and invent-all skip this id unless the user named it.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | contained |
| motion | still |
| density | airy |
| color | restrained |
| surface | hairline |
| type | serif editorial |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Warm near-monochrome. Ivory field, rich ink, one burnished gold. Strategy is Restrained. Gold stays on actions, rules, and focus.

- Ivory `#FAFAF8` canvas
- Rich Black `#1A1A1A` ink
- Warm Gray `#6B6B6B` secondary
- Burnished Gold `#B8860B` accent
- Light Gold `#D4A84B` hover
- Rule `#E8E4DF` hairline
- Muted `#F5F3F0` secondary surface
- Card `#FFFFFF` lift plate

**Type.** Transitional serif carries headlines and display figures. Humanist sans carries body. Mono stamps tracked uppercase labels. Prompt options: Playfair Display, Source Sans 3, IBM Plex Mono. Headlines track slightly tight. Body tracks `0.01em` with line-height near `1.75`.
**Shape.** Modest radii, about `6px` on controls and `8px` on cards. Structure comes from `1px` warm rules.
**Depth.** Paper grain at low opacity. Shadows stay faint, example `0 4px 12px rgba(26,26,26,0.06)`. Featured plates may take a `2px` gold hairline on the top edge.
**Motion.** `200ms` ease-out on color, border, and underline. Primary hover may shift fill to `#D4A84B`. Reduced-motion keeps the color change and drops translate.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md (magazine or editorial manifesto on marketing, top bar + side nav or split on app UI). Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as a gold fill with white label, `6px` radius, and tracked medium weight. Done when the primary measures at least `44px` tall and uses `#B8860B` behind `#FFFFFF` type.
4. Run anti-slop + crit, including category-reflex. Done when the common-layout check fails for this style's own cliché: ivory-and-gold Playfair landing with three equal feature cards.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#1A1A1A` on `#FAFAF8` for body. Gold `#B8860B` is for fills and rules. Body-size gold type only after it clears 4.5:1 on its actual background.
- Focus: `2px` gold ring, `2px` offset, matching `#B8860B`.
- Touch targets stay `44px`. Honor `prefers-reduced-motion` with color-only feedback.
