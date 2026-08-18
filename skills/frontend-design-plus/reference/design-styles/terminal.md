# Terminal

`id=terminal` · `mode=dark` · `font=mono`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- The brief wants a usable shell (ZSH or BASH), server console, or cyber-industrial tool.
- Every string, including headlines, sits in one monospace.
- IxDF dark mode (Laia Tremosa): near-black phosphor field, high contrast, long-session friendly.
- Prompt characters, status codes, and pane chrome are the interface language.

Common jobs: CLI products, infra docs, hacker-adjacent tools, and brands that live inside a prompt.

When the user did not name this id, skip if the brief needs a humanist product UI, fashion serif, or a decorative terminal widget on a marketing hero.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | contained |
| motion | still |
| density | dense |
| color | committed |
| surface | ink |
| type | one family |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Phosphor on near-black, committed green. Fallback tokens (empty color slots only): `background` `#0a0a0a`, `primary` `#33ff00`, `secondary` `#ffb000`, `muted` `#1f521f`, `accent` `#33ff00`, `error` `#ff3333`, `border` `#1f521f`. Amber marks warnings. Red marks errors. Dim green marks idle chrome. The whole surface is the shell. A fake git-diff card as decoration stays out (anti-slop developer-portfolio tell).

**Type.** One monospace for display, body, and UI. Optional samples: JetBrains Mono, Fira Code, VT323. Headings uppercase on a modular snap scale. Body may stay lowercase for command text. Prompt glyphs (`>`, `$`, `~`), flags (`--help`), and status (`[OK]`, `[ERR]`) are the voice. If the briefing named a family, keep it and force mono metrics.

**Shape.** Radius `0`. Panes use `1px` solid or dashed `#1f521f`. Title bars read as `+--- LABEL ---+` or an inverted strip. ASCII rules (`----`, `====`) divide regions. Buttons are `[ LABEL ]` or inverted video blocks.

**Depth.** No drop shadow. Phosphor persistence: `text-shadow: 0 0 5px rgba(51, 255, 0, 0.5)` on primary ink. A faint CRT scanline overlay (`pointer-events: none`) may sit above the canvas. Stats render as bar strings (`[||||||||||.....]`), not pie charts.

**Motion.** Still, with a blinking block or underscore cursor as the pulse. Optional typewriter on a single headline. Hover fills primary and sets ink to `#0a0a0a` (inverted video). A 1px text jitter on hover is enough glitch. Reduced-motion: steady cursor, no typewriter, no jitter.

Inputs follow a prompt (`user@host:~$`) with a block caret. Panes stack on small screens. Long lines wrap with a `\` marker. ASCII art may mark a wordmark.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as bracketed or inverted-video mono commands. Done when the primary control is radius `0`, monospace, `#33ff00` (or mapped primary) on `#0a0a0a`, and hover inverts to a solid primary fill with dark ink.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: charcoal developer portfolio with one orange accent and a fake terminal window in the hero.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#33ff00` on `#0a0a0a` exceeds AA. Recheck amber and dim green (`#1f521f`) for small text; bump luminance if a pair fails 4.5:1.
- Focus: inverted video or a 2px primary outline. The blinking caret is extra, not a replacement for focus on buttons and links.
- Base stays `#0a0a0a` so scanlines and elevation can read. Wrap long mono lines. Honor `prefers-reduced-motion` on blink rate and typing.
- Keep the blinking caret as extra feedback. Buttons and links still show inverted video or a 2px outline on `focus-visible`.
