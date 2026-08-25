# DESIGN.md

Load when [load-map.md](load-map.md) attaches this file to the current slot. Unanswered blanks belong to the Packet.

Visual identity for this product lives in `DESIGN.md` at the project root (or the path the repo already uses). Tokens in YAML are normative. Prose tells the agent why those values exist. Spec: [DESIGN.md Format](https://github.com/google-labs-code/design.md/blob/main/docs/spec.md).

## UX-context framing

`DESIGN.md` is the visual slice of product context: exact values plus how to apply them. It lives next to the code and is read on every UI pass. Success is whether generation matches this product, not whether a stakeholder finds the file persuasive.

**Load before generate.** Follow the file when it exists. Training-data averages (generic SaaS landing, default dashboard) are what you get without this context.

**Tokens vs prose.** YAML wins on hex, type, radii, spacing, and component refs (`{colors.primary}`). Prose covers *why*, *when*, *for whom*, and the case no token covers (`## Overview`, `## Do's and Don'ts`). Evocative names in prose ("Boston Clay") map to token ids (`tertiary`).

**Constraints, not theater.** Write research as rules the model can apply: "Users abandon setup when asked for data they do not have." Skip named personas, stock photos, and journey-map decoration. Invent no users, expertise level, compliance, or glossary.

**Glossary and mental model.** UI copy and control names use how users speak (`reset password`, `case`), not internal jargon (`credential-recovery workflow`). The briefing owns that vocabulary; DESIGN.md does not invent it.

**Context of use steers density.** Hours of expert work → more on screen. Minutes per month → fewer choices per view. Interruption, stress, and audit trails belong in the briefing Lock (`density=`), not as extra YAML groups.

**Do not overload the file.** Visual identity only. Interaction policy, research synthesis, and world-of-use stay in the briefing (and any UX notes the repo already has). Point at real components in code; tokens do not replace the library.

**Curate.** More context is not better. Current approved tokens beat leftover comments. `## Do's and Don'ts` names live guardrails only.

## Follow vs generate

| Repo state         | Action                                                                                                                                                                                                                                                                                                                          |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `DESIGN.md` exists | Read it before the Lock. Use its `name`, colors, type, spacing, rounded, components. Change tokens only when the user asked, or when a11y contrast fails; then patch DESIGN.md in the same change and say what moved.                                                                                                           |
| Missing            | Greenfield: create `DESIGN.md` after briefing *answers* (or invent-all Lock), **before** markup. Values must match the Lock and the CSS you will write. Unanswered blanks: no DESIGN.md this turn. Redesign and polish: extract tokens from the current CSS; do not invent a palette from [design-styles.md](design-styles.md). |

Do not keep a second palette in CSS comments or Tailwind config that contradicts DESIGN.md. CSS custom properties map 1:1 to token names (`--color-primary` ← `colors.primary`). When the file exists, map new UI onto existing token names; do not add colors, fonts, or radii to look complete. Missing `primary` or typography is a gap to fill from the current palette or to ask about, not a license to freestyle. A component kit is a code floor; wrap it with these tokens. Lock `theme=system`: DESIGN.md names surface tokens for light and dark; CSS maps both ([color.md](color.md#system-theme)).

## Front matter (normative)

```yaml
---
version: alpha
name: "<product name from briefing>"
description: "<one-line job of the surface>"
colors:
  primary: "#..."
  secondary: "#..."
  tertiary: "#..."
  neutral: "#..."
  surface: "#..."
  on-surface: "#..."
typography:
  headline-lg:
    fontFamily: "..."
    fontSize: 48px
    fontWeight: 600
    lineHeight: 1.1
    letterSpacing: -0.02em
  body-md:
    fontFamily: "..."
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.6
rounded:
  sm: 4px
  md: 8px
spacing:
  sm: 8px
  md: 16px
  lg: 32px
components:
  button-primary:
    backgroundColor: "{colors.tertiary}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.sm}"
    padding: 12px
---
```

`name` is the briefing name. Hex is the default color format. Token references use `{path.to.token}`. Omit unused groups via `omitted` with a reason rather than inventing a fake scale.

Valid component properties in the spec: `backgroundColor`, `textColor`, `typography`, `rounded`, `padding`, `size`, `height`, `width`. Hover as a sibling key (`button-primary-hover`).

## Body sections (this order)

Present sections stay in spec order. Skip a section only via `omitted`.

1. **Overview** (alias Brand & Style): the enter object, the signature, audience. Mood adjectives (`bold`, `warm`, `premium`) are not Overview.
2. **Colors**: each token with the hex and the job (ink, accent, surface)
3. **Typography**: families, roles, weights
4. **Layout** (alias Layout & Spacing): on marketing greenfield/redesign when [composition.md](composition.md) is already attached — the *thesis* (one experience sentence) plus the Sketch from Frame (the drawing does not reopen occupancy); grid, gutter, type-scale jump, spacing rhythm, motion recipe (`150–250ms ease-out` unless the Lock is `cinematic`). A style id as the *thesis* fails. Sketch absent on that origin fails. Occupancy numbers live in the Sketch footer. App UI and polish: no Sketch. Do not attach composition from this file.
5. **Elevation & Depth** (alias Elevation): shadow vs tonal layers vs hairline
6. **Shapes**: radius language
7. **Components**: buttons, inputs, cards as used on this surface
8. **Do's and Don'ts**: guardrails the *crit* can cite

Unknown extra `##` headings are allowed; duplicate `## Colors` is not.

## Custom language

When Lock uses `style=custom`, `Overview` records the supported register and `Do's and Don'ts` records the signature detail and its reason. Tokens still come from the briefing, project, or [visual-language.md](visual-language.md); a custom label does not authorize a second palette or a new layout family.

## Agent behavior

- Tokens win over adjectives in chat. Prefer `{colors.primary}` over duplicated hex.
- After edits, if `npx` can reach the public npm registry, `npx -y @google/design.md lint DESIGN.md` is optional proof. Lint errors (`broken-ref`) block ship. Warnings (contrast, missing `primary`, missing type) get fixed when they apply to this surface.

Done when DESIGN.md exists, `name` matches the Lock, and the CSS theme reads the same tokens. On generate (file was missing): if palette + type pairing would pass on any similar page, retune **one** role (display, accent, or the *break*) — that retune is the signature, not a fourth token — and say what changed.

**Polish and redesign:** if shipped CSS tokens drift from DESIGN.md, patch DESIGN.md in the same change (extract from CSS; do not invent a palette). Greenfield still writes DESIGN.md **before** markup.
