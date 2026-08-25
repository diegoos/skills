# Minimal Dark

`id=minimal-dark` · `mode=dark` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- Scene is a quiet night tool, a dim studio, or long-session software with warm embers.
- Brief wants layered slate, one amber accent, and lots of dark space.
- Product is a focused app, a premium utility, or a nocturnal marketing surface for that app.
- IxDF Dark Mode (Laia Tremosa) uses dark gray fields and off-white type. Material-style dark gray, high contrast, long-session calm.

Common jobs: people who will stare at the screen for hours and still need calm hierarchy.

When the user did not name this id, skip if the brief wants neon dystopia.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | contained |
| motion | still |
| density | airy |
| color | restrained |
| surface | hairline |
| type | one family |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Cool stacked slates, one warm amber ≤10% of the surface. Amber is action and ember.

Fallback tokens (empty color slots only):

- void `#0A0A0F`
- raised `#12121A`
- plate `#1A1A24`
- ink `#FAFAFA`
- secondary `#71717A`
- amber `#F59E0B`
- amber-ink `#0A0A0F`
- hairline white at 8%
- hover hairline at 15%
- amber wash at 15%

**Type.** One geometric sans for UI. Optional display grotesk and a quiet body sans. Space Grotesk and Inter stay optional. Mono only on metadata.
Headlines tight tracking. Body 16-18px. Labels slightly wide. Weight and size carry rank. One accent hue for the page.
**Shape.** Soft but small. 8px default, 12px cards, 16px large plates, pills for chips. 1px hairlines at 8-15% white.
Primary is 44px, 12px radius, solid `#F59E0B` with `#0A0A0F` label. Field is 44px, 8% hairline, amber ring on focus.
**Depth.** Lightness steps (`#0A0A0F` → `#12121A` → `#1A1A24`) plus a short dark shadow (`0 4px 6px` at 30% black). Amber ambient glow only on the accent control or one hero ember (`0 0 20px` at 15-40% amber).
Matte plates. Grain near 2%. Optional 40px grid at 2% white.
**Motion.** 200ms controls, 300ms plates, ease-out. Hover raises hairline opacity and a 2% scale at most. Press to 0.98.
Reduced-motion keeps amber fill and hairline and drops scale, pulse, and drifting orbs.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. Do not name a hero family here. Do not reopen composition.md. App UI: keep Packet `recipe=`. Do not open product-register.md from this file. Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as amber embers. Done when the primary is solid `#F59E0B` with `#0A0A0F` label, radius 12px, height ≥44px, and hover glow lives on that control only.
4. Subtract this Path cliché in Commit. QA owns anti-slop and crit. Done when the common-layout check fails for this style's own cliché: charcoal-plus-orange developer-tool landing.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#FAFAFA` on `#0A0A0F` for body. `#71717A` only at ≥4.5:1. `#F59E0B` as large type or as a solid fill with dark ink.
- Focus: 2px `#F59E0B` ring, 2px offset on `#0A0A0F`.
- Dark luminance and touch: Keep the three slate steps visible. Void is `#0A0A0F`. Body is `#FAFAFA`. Targets ≥44px. Extra line-height on long light-on-dark copy.
- Ambient orbs, if present, stay `aria-hidden="true"` at 2-4% amber. The UI still reads if those orbs are gone.
