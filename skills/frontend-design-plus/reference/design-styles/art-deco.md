# Art Deco

`id=art-deco` · `mode=dark` · `font=serif`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- Brief names 1920s glamour, Gatsby, Metropolis, a cinema palace, or a brass elevator grille.
- Product is luxury, hospitality, jewelry, cultural institution, or an heirloom service.
- Look asks for sunbursts, chevrons, stepped ziggurats, or bilateral symmetry.
- UX Planet Art Deco mood is glamorous, upscale, jazzy. Gold, symmetry, and angular jewelry-box geometry.

Common jobs: a visitor who expects ceremony and metallic precision.

When the user did not name this id, skip if the brief wants soft consumer SaaS curves.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | contained |
| motion | fluid |
| density | airy |
| color | committed |
| surface | hairline |
| type | serif editorial |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Cool void with one warm metal. Dominant surface is obsidian. Champagne cream carries body. Gold is the locked accent. Midnight blue is inactive depth.

Fallback tokens (empty color slots only):

- background `#0A0A0A`
- raised `#141414`
- foreground `#F2F0E4`
- gold `#D4AF37`
- midnight `#1E3D59`
- pewter `#888888`
- bright gold `#F2E8C4`

**Type.** Serif display owns the voice. All-caps headings with tracking near `0.2em`. H1 sits in the 60-72px band.
Body is a geometric sans at `1.125rem` with relaxed leading. Optional faces: Marcellus or Italiana for display, Josefin Sans for body. Paragraph ink stays `#F2F0E4`. Gold stays on titles, rules, and controls.
**Shape.** Radius `0` to `2px`. Double frames (outer gold hairline, inner dark inset). Stepped corner cuts and 45° diamond holders for icons.
Vertical rules and short measured gold bars (`h-px w-24`) as section marks. Primary button is a sharp 48px plate, 2px gold stroke, all-caps tracking. Field is underline-only, 2px gold, 48px tall.
**Depth.** Metallic sheen on gold fills (`#F2E8C4` to `#D4AF37`). Gold halo `0 0 15px` at about 20% gold on metal only. Fine grain on the void.
Raised charcoal `#141414` against `#0A0A0A` for panels. Images sit in a double frame. Hover raises gold border from 30% to 100% opacity.
**Motion.** Theatrical and mechanical. 300ms feedback, 500ms reveals, ease-out. Hover lifts a framed panel `2px` and raises gold border opacity.
Reduced-motion keeps the border and fill swap and drops lift, pulse, and sunburst expansion.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. Do not name a hero family here. Do not reopen composition.md. App UI: keep Packet `recipe=`. Do not open product-register.md from this file. Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as sharp gold instruments. Done when the primary CTA is all-caps, radius ≤2px, gold border ≥2px, height ≥48px, and hover fills gold with dark ink.
4. Subtract this Path cliché in Commit. QA owns anti-slop and crit. Done when the common-layout check fails for this style's own cliché: cream-and-brass hotel lobby with three equal cards.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: Body uses `#F2F0E4` on `#0A0A0A`. Keep `#D4AF37` for large titles, borders, and controls. Pewter `#888888` only on secondary copy that still clears 4.5:1.
- Focus: 2px gold ring, 2px offset, offset color `#0A0A0A`.
- Touch and dark luminance: Targets ≥44px with ≥8px gap. Surfaces stay off-black `#0A0A0A` / `#141414`. Body stays cream `#F2F0E4`.
- Decorative diamonds, sunbursts, and corner brackets are `aria-hidden="true"`. Keyboard order follows the ceremonial axis top to bottom.
