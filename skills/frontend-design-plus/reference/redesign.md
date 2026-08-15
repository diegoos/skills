# Redesign

Load when Lock `origin=redesign`. Greenfield skips this file.

Misclassifying origin is the usual source of bad output: a rewrite of a live page, or a timid restyle of a blank file.

## Detect origin

Name `greenfield` or `redesign` before markup. Evidence, in order:

1. The user says redesign, restyle, improve, upgrade, polish, or "the current page".
2. The target path, route, or URL already has markup in the repo.
3. Neighboring screens exist and the brief is "make this match / better".
4. Otherwise `greenfield`: new surface, empty path, or the user approved a full restart.

If origin is still unclear, ask once: is this a new UI, or a redesign of a page that already exists?

Then pick the redesign **mode**:

- **Preserve:** modernise without breaking the brand. Audit first; evolve tokens and spacing; keep IA and voice.
- **Overhaul:** new visual language on existing content. Treat visuals as greenfield; preserve content, slugs, and tracking.

If preserve vs overhaul is ambiguous, ask once: keep the existing brand, or start visually from scratch?

## Sequence (redesign only)

1. **Scan.** Read the existing page and its stack: framework, styling method, tokens, neighbors. Stay on that stack. Check the lockfile before any new dependency. Tailwind: read v3 vs v4 before touching config. No framework: vanilla CSS.
2. **Diagnose.** Write the audit below as a list. Every item is a keep, a retire, or a missing state. Done when the list exists; no visual edit before that.
3. **Fix.** Patch the files that already ship the surface. Improve what is there. Preserve mode forbids a from-scratch rewrite. Overhaul may replace blocks after the audit, still on the current stack, still without breaking routes or behavior. Test the flows you touched after each cluster of changes.

## Audit before changing

Document the current state:

- Brand tokens: color, type, logo treatment, radii
- Information architecture: page tree, primary nav, conversion paths
- Content blocks: what works, what is filler
- Patterns to keep: signature interactions, recognisable hero, copy voice
- Patterns to retire: slop tells ([anti-slop.md](anti-slop.md)), broken layout, dead links (`href="#"`), missing hover/focus/loading/empty/error
- SEO baseline: ranking pages, titles, structured data, OG images
- Dial reading: infer current layout / motion / density bands as the starting point, not the marketing baseline
- Code: semantic landmarks, alt text, z-index scale, imports that exist in the lockfile

## Preservation

- Keep URL slugs, anchor IDs, and primary nav labels stable unless asked
- Extract brand colors before applying [color.md](color.md) strategies; an existing purple stays purple
- Preserve copy voice unless the user asked for a rewrite. Visual modernisation leaves the words.
- Honor existing accessibility wins (focus, alt, keyboard, contrast)
- Keep analytics event names, form field `name`s, and section IDs that tracking depends on
- Keep the styling system the project already uses

## Levers (stop when the brief is satisfied)

1. Typography refresh
2. Spacing and rhythm
3. Color recalibration (unify neutrals; keep the brand accent)
4. Hover, focus, and press states
5. Motion layer appropriate to the Lock band
6. Hero and key-section recomposition
7. Loading, empty, and error states
8. Full block replacement, only when the existing block cannot be saved

Tokens that change globally (color, type, radius, space) belong in the design-token layer, not as one-off overrides per page. One token set; themes swap values.

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
