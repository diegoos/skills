# Enterprise

`id=enterprise` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- Look asks for a modern SaaS or B2B product that still feels human.
- Brief wants indigo-violet trust color, colored shadows, and polished app chrome.
- Closest path to product-register. Still name a layout family. Still pass category-reflex (IxDF / Laia Tremosa minimalism as less-but-better, not an empty slate).
- Common jobs: authenticated tools, pricing, and marketing that share one product voice.

When the user did not name this id, skip if the brief wants editorial serif, workshop steel, or drenched neon. `you-decide` and invent-all skip this id unless the user named it.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | briefing owns |
| motion | fluid |
| density | regular |
| color | committed |
| surface | matte |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Cool light field, committed indigo with violet as the gradient partner. Emerald is semantic success, not brand.

- Slate Canvas `#F8FAFC`
- Card `#FFFFFF`
- Indigo `#4F46E5` primary
- Violet `#7C3AED` gradient stop
- Ink `#0F172A`
- Muted `#64748B`
- Success `#10B981`
- Hairline `#E2E8F0`

**Type.** Geometric sans with rounded terminals, one family across UI. Prompt option: Plus Jakarta Sans. Display at 700-800, tight tracking near `-0.02em` on large headlines. Body 400-500, line-height `1.6` to `1.7`. App UI keeps one sans for labels and data.
**Shape.** Cards about `12px`, inputs `8px`, primary may be pill or `8px`. Hairline `#E2E8F0`. Icon wells sit in a soft indigo wash.
**Depth.** Indigo-tinted shadows, example `0 4px 20px -2px rgba(79, 70, 229, 0.1)` at rest and a stronger pair on hover. Soft indigo/violet orbs may sit in backgrounds at low opacity. Surfaces stay matte. Glass only if the scene names it.
**Motion.** `200ms` ease-out. Cards lift `1px`. Primary lifts `0.5px` and the shadow grows. Reduced-motion keeps color and shadow, drops translate and isometric tilt.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. If occupancy is missing, stop and open [composition.md](../composition.md). Do not name a hero family here. App UI: keep the recipe in [product-register.md](../product-register.md). Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as an indigo-to-violet fill with white type and an indigo-tinted shadow. Done when the view has exactly one filled primary and that control is at least `44px` tall.
4. Run anti-slop + crit, including category-reflex. Done when the common-layout check fails for this style's own cliché: indigo-violet corporate landing with three equal feature cards and a generic navy-Inter read.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#0F172A` on `#F8FAFC` for body. White type on `#4F46E5` and on dark indigo bands. Muted `#64748B` only where it still clears 4.5:1.
- Focus: `2px` indigo ring `#4F46E5` with `2px` offset.
- Touch targets stay `44px`. Honor `prefers-reduced-motion`. Dark sections keep white type on indigo-900 class fills.
