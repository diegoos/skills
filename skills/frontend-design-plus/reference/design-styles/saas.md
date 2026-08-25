# SaaS

`id=saas` · `mode=light` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Occupancy is Packet Frame; this file vests craft. Fold vocabulary at Implement only.

## When

- The brief is a B2B or product-led web app that needs calm structure, one accent, and familiar controls.
- Craft should read as product-clean: whitespace, a single action color, soft elevation.
- Category-reflex must pass. Keep the user's layout family. If they named none, pick one from layout-patterns.md or product-register.md before hero markup.
- App UI stays on one sans and Restrained-to-Committed color; marketing may invert one band for a CTA.

Common jobs: dashboards, settings, marketing that must feel like the product, and tools whose users already know Linear or Stripe as a quality bar.

When the user did not name this id, skip if the brief wants phosphor terminal, poster type, or editorial serif as the whole voice. `you-decide` and invent-all skip this id unless the user named it.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | briefing owns |
| motion | fluid |
| density | airy |
| color | committed |
| surface | matte |
| type | one family |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Warm-neutral light, committed accent. Fallback tokens (empty color slots only): `background` `#FAFAFA`, `foreground` `#0F172A`, `muted` `#F1F5F9`, `muted-foreground` `#64748B`, `accent` `#0052FF`, `accent-secondary` `#4D7CFF`, `border` `#E2E8F0`, `card` `#FFFFFF`. Name the strategy Committed before locking hex. If the first idea is trust-blue plus orange CTA, rework per color.md category-reflex: keep neutrals, pick the briefing's real accent. One accent page-wide. Inverted bands may use `#0F172A` with light ink for a single proof or CTA band.

**Type.** One grotesque or humanist sans for headings, body, labels, and data (product-register). Sample only if the pairing procedure or the user named it; Inter is not a required brand face. A display serif (sample: Calistoga) is allowed only when the briefing names serif. Section tags may use a monospace at `xs`, uppercase, tracking about `0.15em`, and at most `ceil(sections / 3)` eyebrows. Body 16–18px, relaxed leading. Display tracking about `-0.02em`.

**Shape.** Cards and buttons `12–16px` radius. Inputs `8–12px`. Pills full-round for labels. Hairline `#E2E8F0` on cards. Featured tiles may use a 2px accent stroke.

**Depth.** Matte white cards on `#FAFAFA`. Soft stacked shadows (`0 1px 3px` up to `0 20px 25px` at low black opacity). Accent-tinted shadow only on the primary control. A faint dot grid or a low-opacity accent wash may texture an inverted band. Skip glass as the default.

**Motion.** Fluid, `200–300ms` `ease-out`. Hover lifts `2px`, deepens shadow, brightens the accent. Continuous motion (pulse, slow rotate) only if the Lock is cinematic and the brief asks. Reduced-motion: color and shadow, no loop, no float.

Primary height `48–56px`. Arrow icons may translate `4px` on hover. Outline buttons pick up an accent-tinted border. Glass and purple mesh stay off unless the scene sentence names them.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep Frame occupancy and Packet folds when task is marketing. Do not name a hero family here. Do not reopen composition.md. App UI: keep Packet `recipe=`. Do not open product-register.md from this file. Done when occupancy (marketing) or recipe (app UI) is already in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists, and category-reflex still fails to guess "SaaS landing" from palette plus layout.
3. If the user named a control language, keep it. Otherwise treat primary controls as a single committed fill (solid or a short accent-to-accent-secondary ramp) with white label and accent-tinted hover shadow. Done when one filled primary exists per view, radius matches tokens, height is at least 44px, and hover lifts without a neon outer glow.
4. Subtract this Path cliché in Commit. QA owns anti-slop and crit. Done when the common-layout check fails for this style's own cliché: centered hero, three equal feature cards, purple or electric-blue glow.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#0F172A` on `#FAFAFA` is strong. `#0052FF` on white must stay at or above 4.5:1. Inverted bands use near-white ink on `#0F172A`.
- Focus: `ring-2` in the mapped accent, `ring-offset-2` on the page background, `focus-visible` only.
- Touch targets at least 44×44px with 8px gaps. Honor `prefers-reduced-motion` on pulse, float, and entrance stagger.
- One filled primary per view. Keyboard order follows the visible work area.
