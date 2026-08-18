# Newsprint

`id=newsprint` · `mode=light` · `font=serif`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- The brief wants a paper of record: morning edition, magazine of columns, or urgent editorial hierarchy.
- Grid lines stay visible. Density is high. Corners stay sharp.
- One editorial red appears on alerts, links, and a scarce CTA.
- Metadata, edition marks, and column rules should feel like print, including on a single-column mobile stack.

Common jobs: news, journals, civic explainers, and brands that borrow broadsheet authority.

When the user did not name this id, skip if the brief needs fashion-only monochrome, rounded product chrome, or a dark canvas.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | still |
| density | dense |
| color | restrained |
| surface | ink |
| type | serif editorial |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Warm paper, restrained ink, one red. Fallback tokens (empty color slots only): `background` `#F9F9F7`, `foreground` `#111111`, `muted` `#E5E5E0`, `accent` `#CC0000`, `border` `#111111`, `hover` `#F5F5F5`, `metadata` `#737373`. Red stays scarce (badges, hover underline, a single CTA). Permanent light. Do not invert red onto black.

**Type.** High-contrast display serif for headlines, a text serif for columns, a grotesque sans for UI chrome, monospace for dates and edition marks. Optional samples: Playfair Display, Lora, a neutral grotesque, JetBrains Mono. If the briefing named families, keep them. Hero type may reach `5xl` to `9xl` with leading near `0.9` and tight tracking. Body 14-18px, relaxed leading. Metadata `xs`, uppercase, widest tracking. Headlines stay sentence case; nav, badges, and bylines go uppercase.

**Shape.** Radius `0` everywhere. Standard rule `1px` solid `#111111`. Section breaks may use `4px`. Adjacent cells share a rule so the grid does not double. Inputs use a `2px` bottom rule and a monospace face.

**Depth.** Flat print. Hover may add a hard cutout: `4px 4px 0 #111111` plus a `2px` translate. No blur, no soft drop. Paper grain: a 4px dot screen at about 4% ink, a fine line grid, or a halftone on placeholders. Images may start grayscale; hover can add a light sepia.

**Motion.** Snappy mechanical, `200ms` `ease-out`. Inversion on buttons, red underline (`decoration-2` `#CC0000`) on links, hard-shadow lift on tiles. Reduced-motion: color and border only.

Icons sit in 48px ink squares at 1-1.5px stroke. A drop cap may open a lead paragraph. One inverted ink band is enough for a how-to or ticker. Justified text is for multi-column body only.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as ink blocks that invert to paper with a black rule. Done when the primary button is `#111111` fill, `#F9F9F7` label, radius `0`, uppercase widest tracking, min-height 44px, and hover inverts fill and ink.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: three equal cards with a red BREAKING pill on a fashion-monochrome hero.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#111111` on `#F9F9F7` exceeds 17:1 (AAA). `#CC0000` on paper must stay above 5:1 (AA). Keep red off black fields.
- Focus: `2px` ring in near-black (`neutral-950`) with `2px` offset, `focus-visible` only. Inputs fill a light well (`#F0F0F0`) instead of a glow.
- Touch targets at least 44×44px. On small screens drop vertical rules, keep horizontal rules, and keep sharp corners.
- Primary CTAs go full width below `md`. Icon-only controls get an `aria-label`.
