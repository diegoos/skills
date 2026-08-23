# Color

Load when [load-map.md](load-map.md) attaches this file (palette or theme in play). Unanswered blanks belong to the Packet.

Choose a strategy, build a palette, and ship the modes Lock `theme=` asks for. Dark, when shipped, is a designed palette.

## Scene sentence (temperature before hex)

Before any hex value, write one sentence describing the environment the interface lives in — a place, a time, a mood. Lock `theme=` owns light vs dark ([briefing.md](briefing.md#theme)). The scene owns temperature. It replaces reflex temperature ("cool because tools", "warm to be safe").

| Scene sentence                                          | Implies                      |
| ------------------------------------------------------- | ---------------------------- |
| "A late-night trading terminal for pros"                | Dark, cool, low-glare        |
| "A sunlit bakery menu on a Sunday morning"              | Light, warm, high key        |
| "A clinical lab dashboard read under fluorescent light" | Light, neutral-cool, calm    |
| "A backstage pass to a sold-out concert"                | Dark, saturated, high-energy |

On `theme=system`, Implies is first paint only ([System theme](#system-theme)). One visible mode for the whole page ([layout-patterns.md](layout-patterns.md#page-theme-lock)).

## Color strategies

Pick one strategy per surface and name it. These are the terms referenced in [brand-register.md](brand-register.md), [product-register.md](product-register.md), and [design-systems.md](design-systems.md).

| Strategy         | Definition                                                                                            | Fits                                          |
| ---------------- | ----------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| **Restrained**   | Near-neutral surfaces dominate; one accent ≤10% of the surface, for action/selection only             | Product UI, dashboards, dense tools — default |
| **Committed**    | One dominant brand color + neutrals; a single sharp accent, locked page-wide                          | Focused brand sites, product landings         |
| **Full palette** | Two to four coordinated hues used with clear hierarchy (primary/secondary/tertiary), not equal weight | Editorial, playful, multi-section marketing   |
| **Drenched**     | Color floods the surface — saturated background, color-on-color, neutrals are the exception           | Maximalist brand, campaigns, posters          |

Rules across all four:

- **One accent for the whole page.** Same accent in every section.
- Commit Committed and Drenched to the edges, or pick Restrained.
- Distribution beats count: dominant color + sharp accent reads richer than five hues at equal weight.
- **60-30-10** (dominant / secondary / accent) describes **Restrained** and **Committed** only. **Drenched** is an explicit Lock exemption: color floods; neutrals are the exception.

## Palette families (when the scene justifies them)

Rotate among named families instead of the category default. Skip this table when Palette is Neutrals or the strategy is Restrained on product UI; those surfaces stay charcoal / off-white. The scene sentence owns temperature. Lock `theme=` owns the mode. These are vectors, not hex recipes.

| Family                    | Character                               | Reach for when                            |
| ------------------------- | --------------------------------------- | ----------------------------------------- |
| **Cold Luxury**           | Silver, chrome, smoke                   | Premium without craft-beige               |
| **Forest**                | Deep green, bone, amber accent          | Outdoor, material, heritage without brass |
| **Black and Tan**         | True off-black + warm tan               | Sharp contrast, no cream field            |
| **Cobalt + Cream**        | Saturated blue against one neutral      | Single accent, no brass                   |
| **Terracotta + Slate**    | Warm rust on cool grey                  | Warmth without beige+oxblood              |
| **Olive + Brick + Paper** | Muted olive, brick accent               | Editorial/utilitarian warmth              |
| **Monochrome + pop**      | Off-white, off-black, one bright accent | When chroma must be scarce                |

If the previous surface you generated used beige+brass, pick a different family.

## Category-reflex (rework if this was the first idea)

**Marketing only.** Skip this check on app UI as a uniqueness bar. A CMS or admin that still looks like a product tool **passes**. The CMS row below is scaffold and sample-data tells, not a request for an original dashboard.

After occupancy is locked, matching the domain is validation when Packet *objects* occupy the lead rectangles. This table is palette *first idea* only: if the hex in your head matches the anti-reflex column, rework the palette. Do not rework occupancy so the page is unguessable from the category.

| Category                        | Anti-reflex                                                                       | Vector                                                                                                     |
| ------------------------------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| SaaS / B2B                      | Trust-blue + orange CTA, glass, three feature cards                               | Named strategy (Restrained on product, Committed on landing); a real material/reference, not "cloud blue"  |
| Fintech / bank / crypto         | Navy+gold or gold+purple OLED                                                     | Scene temperature; numbers and semantic states carry trust                                                 |
| Healthcare                      | Cyan+green pastels, soft-UI                                                       | Clinical light, high contrast, large type                                                                  |
| Restaurant / food               | Appetizing red/orange/brown, generic food hero                                    | Palette of the place and the food; real photography                                                        |
| Hotel / spa / luxury            | Navy+gold or sage/cream/brass                                                     | One family from the table above; intimate dark only if the scene is nocturnal                              |
| Legal / gov / insurance         | Navy+gold heraldry                                                                | Authority by clarity and reading hierarchy                                                                 |
| E-commerce                      | Green success + orange urgency                                                    | Brand of the product; urgency only with real data                                                          |
| Education / kids                | Clay pastels, display-as-body                                                     | Playful display, readable body                                                                             |
| Editorial / news                | Breaking-red + all-serif fashion faces                                            | Ink of the publication; alert red is not identity                                                          |
| Creative / agency               | Pink+cyan, stacked glitch/CRT                                                     | One thesis — brutalist **or** motion **or** editorial                                                      |
| Fitness                         | OLED + sports orange, game rings                                                  | Condensed type and photo; dark only if the scene is a night session                                        |
| Devtools / docs                 | Dark glass HUD, mono body                                                         | Product register: one sans; mono on code only                                                              |
| Developer portfolio             | Dark charcoal + orange + spec sheet / title block / fake git-diff / terminal hero | Scene from the work, not "tools look dark"; a metaphor that is not a drawing, a terminal, or a code editor |
| CMS / admin / product dashboard | Navy + mint SaaS clone; domain only in the logotype; four equal analytics KPIs    | Restrained neutrals; status and legend color; domain in rows, filters, and empty copy                      |

## Building a palette

1. **Anchor from the scene**, not from a generator. Name a real reference (a brand, a film still, a physical material) before opening a color tool. On `you-decide` / invent-all, park the canvas on that reference — not on the model-default triad (cream ~`#F4F1EA` + terracotta, near-black + one acid or vermilion, or broadsheet ink-on-newsprint) unless Packet *tension* names that axis ([design-styles.md](design-styles.md#pick)).
2. **Pick the dominant surface.** Restrained and product UI: near-neutral (charcoal, off-white). A named hue is the accent, not the canvas, unless Palette named a tinted field or Lock `color=drenched`.
3. **Keep the neutral ramp near chroma 0.** A 1–2% wash is optional. Recasting `--surface` as olive, forest, or navy fails Restrained. Avoid pure `#000` / `#fff`.
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

## System theme

Lock `theme=system` (briefing Both).

Done when every item holds:

1. Light tokens and dark tokens both exist in DESIGN.md and in CSS.
2. A labeled chrome control (switch, segmented control, or icon button with an accessible name) sets light or dark for the whole page. It is not the filled primary.
3. First paint may follow `prefers-color-scheme` when the user has not chosen. After the control is used, that choice wins for the session.
4. Tokens switch on `html` via `data-theme` or a class. Components read tokens. No `filter: invert()`.

Media-query-only (control count = 0) fails. Dark-only or light-only CSS fails. A toggle that does not swap tokens fails.

Set `data-theme` before first paint from the stored choice, else from `prefers-color-scheme`. Construction of the dark palette: [Dark mode](#dark-mode-construct-dont-invert).

## Dark mode (construct, don't invert)

Build the dark palette when Lock `theme=` is `dark` or `system`. Skip it when Lock is `light`. Disk already has dual tokens or a switch → follow disk; do not invent a parallel theme.

A dark theme is a designed palette, not `filter: invert()`. Do not ship dark-only because the job is "CMS", "dashboard", or "admin".

- **Canvas is charcoal.** `--surface` and `--surface-raised` sit in `#0d0e12`–`#1c1f26` with chroma near 0. The accent recasts buttons, links, and active nav, not the page field. Tinted dark (green, navy, olive walls) only when Palette named that family or Lock `color=drenched`.
- **Base off-black, not `#000`.** Pure black crushes elevation and feels cheap.
- **Elevation by lightness, not shadow.** Closer/raised surfaces get *lighter*, not a drop shadow. Shadows barely read on dark.
- **Soften text.** Don't use pure `#fff` for body — slightly dimmed off-white reduces glare. Add 0.05–0.1 to line-height for light-on-dark ([typography.md](typography.md#line-length-and-spacing)).
- **Re-tune the accent.** A mid accent that pops on light often muddies on dark — raise lightness/chroma for the dark token rather than reusing the same hex.
- **Re-check every contrast pair.** Light-mode ratios do not transfer; verify text and state colors against dark surfaces (≥4.5:1 body, ≥3:1 large).
- **Map tokens, not values.** Define `--surface`, `--surface-raised`, `--text-primary` per theme; components reference tokens and switch with the theme.

```css
:root,
[data-theme="light"] {
  --surface: #faf9f7;
  --surface-raised: #ffffff;
  --text-primary: #1a1b1e;
  --accent: #2f5fde;
}
[data-theme="dark"] {
  --surface: #121419;
  --surface-raised: #1c1f26; /* lighter = raised */
  --text-primary: #e8e9ec; /* off-white, not #fff */
  --accent: #6f93f5; /* brighter for dark */
}
```

Lock `theme=light`: ship the light block only. Lock `theme=dark`: ship the dark block as `:root`. Lock `theme=system`: ship both plus the chrome control. `@media (prefers-color-scheme: dark)` may set first paint when `html` has no `data-theme`; it is not the switch.

## Color tells (quick reference)

Cross-check:

- Purple/blue gradient glow as the default accent
- New accent color per section
- Brand accent reused as "success" / "error"
- Pure black or pure white surfaces
- Naive inverted dark mode (shadows instead of lightness elevation)
- Dark canvas recast in the accent hue (green or navy field)
- Lock `theme=system` shipped as one locked mode (no chrome switch)
- Gray text on tinted/colored backgrounds (darken to the bg hue instead)
