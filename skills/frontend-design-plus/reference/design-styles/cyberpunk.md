# Cyberpunk

`id=cyberpunk` · `mode=dark` · `font=mono`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- Scene is a wet megacity night, a rogue terminal, or high-tech low-life fiction.
- Look names chamfered HUD plates, scanlines, chromatic split, or acid-green signal.
- Product is a game, a festival, a story world, or a voltage-heavy tool.
- UX Planet Cybercore mood is futuristic and dystopian. Neon, glitch, and tech marks stay on the craft layer.

Common jobs: audiences who expect voltage and still need to read alerts and press controls.

When the user did not name this id, skip if the brief wants a quiet developer portfolio.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | offset |
| motion | cinematic |
| density | regular |
| color | full |
| surface | ink |
| type | one family |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Blue-black void with three signal neons. Green is the primary current. Magenta and cyan are split accents for chromatic edges.

Fallback tokens (empty color slots only):

- void `#0a0a0f`
- card `#12121a`
- chrome `#1c1c2e`
- ink `#e0e0e0`
- muted `#6b7280`
- green `#00ff88`
- magenta `#ff00ff`
- cyan `#00d4ff`
- border `#2a2a3a`
- danger `#ff3366`

**Type.** One mono family for UI. Geometric mono for display (optional Orbitron). Readable mono for body (optional JetBrains Mono). Headings uppercase with wide tracking.
Body `1rem`, relaxed leading, slightly wide tracking. Labels small, uppercase, tracking near `0.2em`. Body ink is `#e0e0e0`. Green is for titles, prefixes, and live states.
**Shape.** Radius `0`-`2px`. Chamfered corners via clip-path (about 10px cuts). 1-2px borders. Technical plates.
Primary is a 44px+ chamfered outline in `#00ff88`, uppercase mono. Hover fills green and flips label to the void. Field uses a `>` prefix, 1px `#2a2a3a`, green border plus glow on focus.
**Depth.** Neon glow only on the live signal (accent border, focused field, display title). Stacked green glow `0 0 5px #00ff88` plus a softer 10px wash.
Scanline overlay and a faint 50px circuit grid at about 3% green. RGB split (`#ff00ff` left, `#00d4ff` right) on the hero word. Body copy stays unsplit.
**Motion.** Sharp digital snaps. 100-150ms, stepped or `cubic-bezier(0.4, 0, 0.2, 1)`. Occasional glitch on the display word. Blink cursor as a local motif.
Reduced-motion freezes glitch and scanline travel and keeps a static chromatic offset plus the green border.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as chamfered signal plates. Done when the primary has a 2px `#00ff88` border, a chamfer clip, height ≥44px, uppercase mono label, and glow attached to that control only.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: developer-portfolio git-diff or fake terminal hero.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#e0e0e0` on `#0a0a0f` for body. `#00ff88` on the void for large labels and borders (this pair is near 7.5:1). Muted `#6b7280` only at AA. Pair hue with a prefix, icon, or weight.
- Focus: 2px `#00ff88` ring, 2px offset on `#0a0a0f`, plus the small neon stack on that control.
- Dark luminance and motion: Void stays `#0a0a0f`. Body stays `#e0e0e0`. Targets ≥44px. `prefers-reduced-motion` stills glitch, blink, and scanline scroll.
- Scanlines and circuit grids are `aria-hidden="true"` and pointer-events none. Live status uses a word plus the green mark.
