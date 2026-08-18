# Web3

`id=web3` · `mode=dark` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- Brief names Bitcoin, DeFi, a ledger, or digital gold in a deep void.
- Look asks for orange heat, thin grid structure, and mono data next to geometric titles.
- Product must signal value and precision (wallet, protocol, market, on-chain status).
- Orange heat is the brand. Glow lives on the control that is live.

Common jobs: operators who read prices and still want a branded night surface.

When the user did not name this id, skip if the brief wants a light consumer bank.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | briefing owns |
| motion | fluid |
| density | regular |
| color | committed |
| surface | hairline |
| type | mono accent |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** True void with Bitcoin fire. One orange locked page-wide. Gold `#FFD600` is a value highlight on stats and success.

Fallback tokens (empty color slots only):

- void `#030304`
- surface `#0F1115`
- display `#FFFFFF`
- muted `#94A3B8`
- border `#1E293B`
- bitcoin `#F7931A`
- burnt `#EA580C`
- gold `#FFD600`

**Type.** Geometric sans for titles (category first). Body sans at 16-18px, relaxed leading. Mono on prices, hashes, badges, and nav ticks (optional JetBrains Mono), uppercase with wide tracking.
Tight leading on display. Inter and Space Grotesk stay optional. Display may use `#FFFFFF`. Long copy prefers `#94A3B8` when the pair clears AA, otherwise `#FFFFFF`.
**Shape.** Cards 12-16px. Buttons pill. Inputs 8px or underline-only. 1px hairlines at rest (`#1E293B` or white at 10%). Hover hairline shifts to `#F7931A` at 50%. Focus hairline full `#F7931A`.
Primary is a 44px pill in `#F7931A` or `#EA580C` to `#F7931A`, uppercase tracking. Field is 48px, bottom border 2px, orange on focus.
**Depth.** Matte `#0F1115` plates on `#030304`. Orange glow only on the live control or a selected node (`0 0 20px` at about 50% burnt). Optional faint 50px grid that fades at the edges.
Hairline enclosures. Colored shadow uses orange or gold tints.
**Motion.** Precise terminal speed. 200-300ms on hover lift (`1px`) and border. Slow float only if the Lock is cinematic and the brief named an orb.
Reduced-motion keeps the orange fill and hairline and drops float, spin, ping, and scale.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as orange-ink pills. Done when the primary is `#F7931A` (or `#EA580C` to `#F7931A`), pill radius, height ≥44px, and any glow is on that button, while cards stay matte `#0F1115` with a 1px hairline.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: navy-gold crypto glass HUD.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#FFFFFF` for large display on `#030304`. Body and captions prefer `#94A3B8` only where the pair still clears 4.5:1. Recheck `#F7931A` on void at small sizes and use it at large or on a solid fill with dark ink.
- Focus: 2px `#F7931A` ring on the control. Fields use a 2px `#F7931A` underline plus a short orange wash.
- Touch and dark luminance: Targets ≥44px. Prefer surface `#0F1115` for plates. Honor reduced-motion on orbital spin and ping badges.
- Prices and status use mono plus a word. Icon wells may tint `#EA580C` at 20% fill with a 50% orange hairline.
