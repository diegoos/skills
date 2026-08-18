# Redesign and polish

Load after briefing when Lock `origin=redesign` or `origin=polish` ([load-map.md](load-map.md)). Polish with no blanks: after Classify. Greenfield skips this file. Do not open this file to detect origin; SKILL.md Classify is enough.

Misclassifying origin is the usual source of bad output: a rewrite of a live page, a catalog style on a determined look, or a timid restyle of a blank file.

## Detect origin

Name `greenfield`, `redesign`, or `polish` before markup. Evidence, in order:

1. The user says polish, tighten, improve craft, fix spacing, contrast, states, or a11y, and does not ask for a new look → `polish`.
2. The user says redesign, restyle, redo the layout, new IA, or "rethink this page" → `redesign`.
3. The target path, route, or URL already has markup, and the brief is "make this match / better" without a new look → `polish`.
4. The target already has markup, and the briefing names a new job, audience, success, or composition → `redesign`.
5. Otherwise `greenfield`: new surface, empty path, or the user approved a full restart.

If origin is still unclear, ask once: new UI, redesign this page from your briefing, or polish what is here?

Existing surface: follow DESIGN.md, project tokens, current CSS, stack, wordmark, and copy voice. Lock `style=none`. Leave [design-styles.md](design-styles.md) closed. A catalog `id` on redesign or polish fails this file. Do not overlay a second default system (Shadcn theme, catalog craft) on a live brand.

## Sequence

1. **Scan.** Read the existing page and its stack: framework, styling method, tokens, neighbors. Stay on that stack. Check the lockfile before any new dependency. Tailwind: read v3 vs v4 before touching config. No framework: vanilla CSS.
2. **Diagnose.** Write the audit below as a list. Every item is a keep, a retire, or a missing state. Name filler to delete. Done when the list exists; no visual edit before that.
3. **Fix.** Patch the files that already ship the surface. Improve what is there. Polish keeps the current layout family and visual language; success is deletion and craft (hierarchy, isolation, breakpoints, states), not a new look. Redesign may recompose from the user briefing, still on the current stack, still without breaking routes or behavior. Disk owns color, type, and radius unless the briefing names a token change. Test the flows you touched after each cluster of changes.

## Audit before changing

Document the current state:

- Brand tokens: color, type, logo treatment, radii. Prefer `DESIGN.md` when it exists ([design-md.md](design-md.md))
- Information architecture: page tree, primary nav, conversion paths
- Content blocks: what works, what is filler (retire filler on polish; redesign may replace a block only when it cannot be saved)
- Patterns to keep: signature interactions, recognisable hero, copy voice
- Patterns to retire: slop tells ([anti-slop.md](anti-slop.md)), broken layout, dead links (`href="#"`), missing hover/focus/loading/empty/error
- SEO baseline: ranking pages, titles, structured data, OG images
- Dial reading: infer current layout / motion / density bands as the starting point, not the marketing baseline
- Code: semantic landmarks, alt text, z-index scale, imports that exist in the lockfile

## Preservation

- Keep URL slugs, anchor IDs, and primary nav labels stable unless asked
- Extract brand colors before applying [color.md](color.md) strategies; an existing purple stays purple until the user asks to kill it
- Preserve copy voice unless the user asked for a rewrite. Visual modernisation leaves the words.
- Honor existing accessibility wins (focus, alt, keyboard, contrast)
- Keep analytics event names, form field `name`s, and section IDs that tracking depends on
- Keep the styling system the project already uses

## Levers (stop when the brief is satisfied)

**Polish** uses 1–5 only. **Redesign** may continue through 8 when the briefing asks. Polish does not re-roll the aesthetic and does not pick a catalog `id`.

1. Typography refresh (same families unless DESIGN.md already names a change)
2. Spacing and rhythm
3. Color recalibration (unify neutrals; keep the brand accent)
4. Hover, focus, and press states
5. Motion layer matching the current Lock band
6. Hero and key-section recomposition (redesign)
7. Loading, empty, and error states
8. Full block replacement, only when the existing block cannot be saved (redesign)

Tokens that change globally (color, type, radius, space) belong in the design-token layer, not as one-off overrides per page. One token set; themes swap values. Polish patches tokens only for contrast or a named DESIGN.md gap.

## Never change silently

Require explicit user approval before changing:

- URL structure / route slugs
- Primary nav labels
- Form field names or order
- Brand logo or wordmark
- Legal, consent, or cookie copy
- Framework or CSS library migration

## See also

- [brand-register.md](brand-register.md): visual language after the audit
- [product-register.md](product-register.md): app UI preservation
- [anti-slop.md](anti-slop.md): tells to retire
- [production-engineering.md](production-engineering.md): states, skip-link, forms
