# Bold Typography

`id=bold-typography` · `mode=dark` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- Brief says the headline is the picture, a poster, a manifesto, or a Huge Inc-scale statement.
- Look asks for extreme scale contrast, tight display tracking, and almost no chrome.
- Type may split words across lines on purpose, with a reason named in the Lock.
- IxDF Bold Typography (Laia Tremosa) treats type as the surface. Bend tracking, size, and line breaks only when that break has a job.

Common jobs: campaigns, studios, and editorials where letterforms carry the brand.

When the user did not name this id, skip if the brief needs dense app chrome.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | wild |
| motion | still |
| density | airy |
| color | restrained |
| surface | hairline |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Near-black field, warm white ink, one vermillion accent. Accent sits on headlines, underlines, and one CTA.

Fallback tokens (empty color slots only):

- background `#0A0A0A`
- card `#0F0F0F`
- muted surface `#1A1A1A`
- foreground `#FAFAFA`
- muted text `#737373`
- accent `#FF3D00`
- accent-ink `#0A0A0A`
- border `#262626`

**Type.** Display is the surface. Aim for about 6:1 between H1 and body (desktop H1 near 96px, body 16-18px). Display tracking `-0.04em` to `-0.06em`. Labels `0.1em`-`0.2em`. Body leading 1.6.
Optional grotesk: Inter Tight. Optional serif only on pull quotes. Body stays 16px+ while display may break a word to make a shape. Headline leading 1.0-1.1.
**Shape.** Radius `0`. 1px dividers. 2px accent underlines as the main affordance. Wide H1 container (`64rem`+) so a poster line holds two lines or fewer on desktop unless the Lock named a deliberate split.
Primary is text plus underline, uppercase, tracking `0.1em`. Outline secondary inverts to `#FAFAFA` fill on hover. Field is 48-56px, radius 0, 1px `#262626`, accent border on focus.
**Depth.** Layer a large muted word behind bright ink. Thin accent bars (`4px` tall, short width) as anchors. Optional 1.5% grain on the field.
Rank comes from scale, tracking, and rules. Hover on a panel lightens the 1px border.
**Motion.** Fast and linear. 150ms on underlines and color. 200ms on disclosure height. Easing `cubic-bezier(0.25, 0, 0, 1)`. Underline scales on hover. Press shifts `1px` down.
Reduced-motion keeps the underline visible at rest and drops scale and slide-up entrance.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as typographic underlines. Done when the primary is text plus a ≥2px `#FF3D00` underline, radius `0`, height ≥44px, and the H1 to body size ratio is ≥6:1 on desktop.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: six-line wrapped H1 in a narrow cage.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#FAFAFA` on `#0A0A0A` for body. `#737373` only where it still clears 4.5:1. `#FF3D00` on the field is for large type and underlines. Pair small accent with weight or an underline.
- Focus: 2px `#FF3D00` ring, 2px offset, no glow fill.
- Touch and dark luminance: Targets ≥44px. Field is `#0A0A0A`. Body is `#FAFAFA`. Keep body at 16px+ and leading ≥1.5 when display type shouts.
- Underlines stay ≥2px so the affordance reads without hue. Decorative overflow numbers hide on small screens if they cause horizontal scroll.
