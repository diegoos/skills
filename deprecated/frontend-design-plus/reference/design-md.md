# DESIGN.md

Visual identity lives in `DESIGN.md` at the project root (or the path the repo already uses). Tokens in YAML are normative. Spec: [DESIGN.md Format](https://github.com/google-labs-code/design.md/blob/main/docs/spec.md).

**Load before generate.** Follow the file when it exists. YAML wins on hex, type, radii, spacing. CSS custom properties map 1:1 (`--color-primary` ← `colors.primary`).

## Follow vs generate

| Repo state                          | Action                                                                                                                                                                                      |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Exists, color and type slots filled | Use them. Polish and redesign: unify CSS to those tokens. Do not rewrite DESIGN.md from CSS. Patch DESIGN.md only when the user asked or contrast fails; then patch CSS in the same change. |
| Exists, color or type empty         | Keep filled slots. Fill empty color/type from current CSS. Do not invent a second palette.                                                                                                  |
| Missing                             | Greenfield: create DESIGN.md **before** markup. Polish and redesign: extract tokens from current CSS.                                                                                       |

Do not keep a second palette in CSS comments or Tailwind config that contradicts DESIGN.md.

## Front matter (normative)

```yaml
---
version: alpha
name: "<product name>"
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

Hex is the default color format. Token references use `{path.to.token}`. Omit unused groups via `omitted` with a reason.

## Body sections (this order)

1. **Overview** — Job, enter object, Claim, Pair, Signature, audience. Mood adjectives are not Overview. Operate: Signature is how the work object reads, not a campaign beat.
2. **Colors** — each token with hex and job (ink, accent, surface)
3. **Typography** — families, roles, weights
4. **Layout** — fields from SKILL.md Layout: Job, objects, Claim, Pair, Mode, dials, ASCII of enter plus 3–5 spine folds (greenfield and redesign; polish keeps the live family), spacing rhythm. Motion `150–250ms ease-out` unless cinematic.
5. **Elevation & Depth** — shadow vs tonal vs hairline
6. **Shapes** — radius language
7. **Components** — only controls an object asked for
8. **Do's and Don'ts** — live guardrails

Unknown extra `##` headings are allowed; duplicate `## Colors` is not.

Done when DESIGN.md exists, `name` matches the Job's product, and CSS reads the same tokens. Occupancy fields: SKILL.md Layout.
