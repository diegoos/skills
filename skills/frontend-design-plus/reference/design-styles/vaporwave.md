# Vaporwave

`id=vaporwave` · `mode=dark` · `font=sans`

Agent style guide. Keep the user's briefing, Look, DESIGN.md, and project tokens. Fill blanks only: type attitude, material, motion, density, and the cliché to refuse. The user's palette, typeface, radius, and layout stay as chosen. Layout families still come from the briefing and from layout-patterns.md (marketing) or product-register.md (app UI).

## When

- Look asks for 1980s retro-futurism, outrun grids, CRT noise, or ironic digital nostalgia.
- Brief wants pastel pink and purple energy, glitch, and terminal chrome on a dark void (Himanshu Bhardwaj / UX Planet Vaporwave mood, prompt tokens at full neon chroma).
- Motion may include scanlines and chromatic aberration that still honor reduced-motion.
- Common jobs: music, zines, arcade tools, and portfolio scenes that can carry satire.

When the user did not name this id, skip if the brief wants a quiet product shell or physical workshop materials.

Lock table: fill a dial only when the briefing, Look, DESIGN.md, and the current screen left it blank.

## Lock

| Dial | Fill if blank |
| --- | --- |
| layout | wild |
| motion | cinematic |
| density | dense |
| color | drenched |
| surface | ink |
| type | grotesk display |

Quiet constraints still override.

## Craft

Hex and sample typefaces in this section are fallbacks for empty slots. Keep any color, typeface, radius, or control the user, DESIGN.md, or project CSS already named, and map this file's attitude onto those tokens.

**Palette.** Cool void, drenched neon. Magenta is the hero, cyan the link and glow, orange the sunset stop. Body stays chrome on void.

- Void `#090014` canvas
- Chrome `#E0E0E0` body
- Panel `#1a103c` cards
- Hot Magenta `#FF00FF` primary
- Electric Cyan `#00FFFF` links and glow
- Sunset Orange `#FF9900` tertiary
- Quiet Border `#2D1B4E`
- Glass Panel `rgba(26, 16, 60, 0.8)`

**Type.** Geometric wide sans for display, often uppercase and heavy. Mono for UI labels, buttons, and inputs. Prompt options: Orbitron, Share Tech Mono. Headlines may take a three-stop fill `#FF9900` to `#FF00FF` to `#00FFFF`. Body stays `#E0E0E0`.
**Shape.** Square geometry. `border-radius: 0` on controls and cards. `2px` neon tubes, `4px` on outer frames. Occasional full-circle dots on window chrome. Buttons may skew `-12deg` at rest. Title bars may use three dots in magenta, cyan, and orange.
**Depth.** Colored glows, example `0 0 20px #FF00FF`. Receding grid, CRT scanlines, and a large blurred sun are textures. Cards may use a cyan top bar plus magenta side edges. Irony lives in terminal chrome and glitch. Body type stays `#E0E0E0` on `#090014`.
**Motion.** `200ms` linear. Hover un-skews, fills, and doubles glow. Glitch and pulse are optional. Reduced-motion freezes glitch, scanline animation, and skew morph. Static neon borders may remain.

## Path

Done criteria that name a hex apply only when that fallback token is in use. Prefer the user's mapped token.

1. Keep the layout family the user named. If none, name one from layout-patterns.md or product-register.md. Done when that name is in the Lock.
2. Keep the user's tokens. Fill empty DESIGN.md slots from Craft. Done when CSS uses the named user palette when one exists.
3. If the user named a control language, keep it. Otherwise treat primary controls as square neon frames (cyan or magenta, `2px`), mono uppercase labels, optional `-12deg` skew. Done when radius is `0`, hover glow is visible, and label contrast against the filled state clears 4.5:1.
4. Run anti-slop + crit. Done when the common-layout check fails for this style's own cliché: centered magenta-grid hero with three equal glowing feature cards.

## A11y

If the surface uses the user's palette, recheck contrast on those pairs. Hex values here describe the fallback tokens only.

- Contrast: `#E0E0E0` on `#090014` for body (keep this pair). Magenta and cyan stay on labels, borders, and fills. Body-size neon type only after 4.5:1 on its actual background.
- Focus: `2px` cyan ring `#00FFFF` plus a visible glow, offset from the void.
- Reduced-motion must stop glitch, RGB shift, and looping scanline animation. Touch targets stay `44px`.
