# Color

Choose a strategy, build a palette, and ship a dark theme that is a designed palette. Tells: [anti-slop.md](anti-slop.md).

## Scene sentence (decide theme before picking colors)

Before any hex value, write one sentence describing the environment the interface lives in — a place, a time, a mood. The scene decides light vs dark and temperature. It replaces reflex choices ("dark because tools look cool", "light to be safe").

| Scene sentence | Implies |
| --- | --- |
| "A late-night trading terminal for pros" | Dark, cool, low-glare |
| "A sunlit bakery menu on a Sunday morning" | Light, warm, high key |
| "A clinical lab dashboard read under fluorescent light" | Light, neutral-cool, calm |
| "A backstage pass to a sold-out concert" | Dark, saturated, high-energy |

If the scene does not point clearly to light or dark, the brief is missing an anchor — ask one question or default to the register (product → light/system; brand → whatever the scene supports). One theme per page ([layout-patterns.md](layout-patterns.md#page-theme-lock)).

## Color strategies

Pick one strategy per surface and name it. These are the terms referenced in [brand-register.md](brand-register.md), [product-register.md](product-register.md), and [design-systems.md](design-systems.md).

| Strategy | Definition | Fits |
| --- | --- | --- |
| **Restrained** | Tinted neutrals dominate; one accent ≤10% of the surface, for action/selection only | Product UI, dashboards, dense tools — default |
| **Committed** | One dominant brand color + neutrals; a single sharp accent, locked page-wide | Focused brand sites, product landings |
| **Full palette** | Two to four coordinated hues used with clear hierarchy (primary/secondary/tertiary), not equal weight | Editorial, playful, multi-section marketing |
| **Drenched** | Color floods the surface — saturated background, color-on-color, neutrals are the exception | Maximalist brand, campaigns, posters |

Rules across all four:

- **One accent for the whole page.** Same accent in every section.
- Commit Committed and Drenched to the edges, or pick Restrained.
- Distribution beats count: dominant color + sharp accent reads richer than five hues at equal weight.
- **60-30-10** (dominant / secondary / accent) describes **Restrained** and **Committed** only. **Drenched** is an explicit Lock exemption: color floods; neutrals are the exception.

## Palette families (when the scene justifies them)

Rotate among named families instead of the category default. The scene sentence still owns light vs dark and temperature. These are vectors, not hex recipes.

| Family | Character | Reach for when |
| --- | --- | --- |
| **Cold Luxury** | Silver, chrome, smoke | Premium without craft-beige |
| **Forest** | Deep green, bone, amber accent | Outdoor, material, heritage without brass |
| **Black and Tan** | True off-black + warm tan | Sharp contrast, no cream field |
| **Cobalt + Cream** | Saturated blue against one neutral | Single accent, no brass |
| **Terracotta + Slate** | Warm rust on cool grey | Warmth without beige+oxblood |
| **Olive + Brick + Paper** | Muted olive, brick accent | Editorial/utilitarian warmth |
| **Monochrome + pop** | Off-white, off-black, one bright accent | When chroma must be scarce |

If the previous surface you generated used beige+brass, pick a different family.

## Category-reflex (rework if this was the first idea)

After the scene sentence, check the category. If the palette in your head matches the anti-reflex column, rework. The positive column is a **vector**, not a swatch — never treat industry as a hex lookup.

| Category | Anti-reflex | Vector |
| --- | --- | --- |
| SaaS / B2B | Trust-blue + orange CTA, glass, three feature cards | Named strategy (Restrained on product, Committed on landing); a real material/reference, not "cloud blue" |
| Fintech / bank / crypto | Navy+gold or gold+purple OLED | Scene temperature; numbers and semantic states carry trust |
| Healthcare | Cyan+green pastels, soft-UI | Clinical light, high contrast, large type |
| Restaurant / food | Appetizing red/orange/brown, generic food hero | Palette of the place and the food; real photography |
| Hotel / spa / luxury | Navy+gold or sage/cream/brass | One family from the table above; intimate dark only if the scene is nocturnal |
| Legal / gov / insurance | Navy+gold heraldry | Authority by clarity and reading hierarchy |
| E-commerce | Green success + orange urgency | Brand of the product; urgency only with real data |
| Education / kids | Clay pastels, display-as-body | Playful display, readable body |
| Editorial / news | Breaking-red + all-serif fashion faces | Ink of the publication; alert red is not identity |
| Creative / agency | Pink+cyan, stacked glitch/CRT | One thesis — brutalist **or** motion **or** editorial |
| Fitness | OLED + sports orange, game rings | Condensed type and photo; dark only if the scene is a night session |
| Devtools / docs | Dark glass HUD, mono body | Product register: one sans; mono on code only |

## Building a palette

1. **Anchor from the scene**, not from a generator. Name a real reference (a brand, a film still, a physical material) before opening a color tool.
2. **Pick the dominant** surface family — the color the eye sees most. In Restrained this is a tinted neutral; in Drenched it is the saturated field.
3. **Derive a neutral ramp** from the dominant hue, not pure gray. Mix a few percent of the dominant into grays so surfaces feel intentional, not stock. Avoid pure `#000` / `#fff` (see [anti-slop.md](anti-slop.md#visual-tells)).
4. **Choose one accent** with enough chroma to carry action and selection. Verify it clears contrast on its own background (buttons, links).
5. **Add semantic states** (below) as a separate, functional layer — not the brand accent reused for "success".
6. **Lock as tokens** ([design-systems.md](design-systems.md)) with semantic names (`--surface`, `--text-primary`, `--accent`), never raw hex in components.

## Semantic state colors

States communicate meaning, so they answer to recognition first and brand second. Keep them distinct from the brand accent.

| State   | Convention          | Note                                      |
| ------- | ------------------- | ----------------------------------------- |
| Success | Green family        | Pair with icon/label — never color alone  |
| Warning | Amber/orange family | Reserve for recoverable, attention-needed |
| Error   | Red family          | High contrast; must read at small sizes   |
| Info    | Blue/neutral family | Lowest urgency                            |

Never rely on hue alone to carry meaning — pair with icon, label, or weight for color-blind users ([ux-principles.md](ux-principles.md)). Each state needs a foreground/background pair that clears WCAG AA.

## Dark mode (construct, don't invert)

**Dark mode is not mandatory.** Decide whether to build it before how to build it:

- **Project already has dark mode** (tokens, theme switch, `prefers-color-scheme` handling, or design-system instructions) → follow the project's existing approach; do not invent a parallel theme.
- **Brief or scene clearly calls for it** (e.g. a night-time tool) → build it with the rules below.
- **Unclear whether the project wants dark mode** → ask the user one question before adding it. Don't ship a dark theme by reflex.

When you do build it, a dark theme is a designed palette, not `filter: invert()`.

- **Base off-black, not `#000`.** Start around `#0d0e12`–`#16181d`; pure black crushes elevation and feels cheap.
- **Elevation by lightness, not shadow.** Closer/raised surfaces get _lighter_, not a drop shadow. Shadows barely read on dark.
- **Soften text.** Don't use pure `#fff` for body — slightly dimmed off-white reduces glare. Add 0.05–0.1 to line-height for light-on-dark ([typography.md](typography.md#line-length-and-spacing)).
- **Re-tune the accent.** A mid accent that pops on light often muddies on dark — raise lightness/chroma for the dark token rather than reusing the same hex.
- **Re-check every contrast pair.** Light-mode ratios do not transfer; verify text and state colors against dark surfaces (≥4.5:1 body, ≥3:1 large).
- **Map tokens, not values.** Define `--surface`, `--surface-raised`, `--text-primary` per theme; components reference tokens and switch with the theme.

```css
:root {
  --surface: #faf9f7;
  --surface-raised: #ffffff;
  --text-primary: #1a1b1e;
  --accent: #2f5fde;
}
@media (prefers-color-scheme: dark) {
  :root {
    --surface: #121419;
    --surface-raised: #1c1f26; /* lighter = raised */
    --text-primary: #e8e9ec; /* off-white, not #fff */
    --accent: #6f93f5; /* brighter for dark */
  }
}
```

## Color tells (quick reference)

Cross-check against [anti-slop.md](anti-slop.md#color-strategy-anti-patterns):

- Purple/blue gradient glow as the default accent
- New accent color per section
- Brand accent reused as "success" / "error"
- Pure black or pure white surfaces
- Naive inverted dark mode (shadows instead of lightness elevation)
- Gray text on tinted/colored backgrounds (darken to the bg hue instead)
