# Custom visual language

Use when Lock `style=custom`, or when the user asked for a named visual register that is not a catalog `id`. On `you-decide`, default is `style=none` and craft from the enter object in DESIGN.md. Do not open this file to avoid making a design decision.

## Contract

Set `style=custom` and write one compact register with at least three of these four signals:

- **Material** — the real surface, artifact, place, or physical behavior the interface borrows from;
- **Type attitude** — how type behaves, not merely a font name;
- **Interaction behavior** — how controls respond and what motion communicates;
- **Signature** — one visible detail that belongs to this product and would be lost if the lead object changed.

Every signal must trace to the Job, an Inventory object, Packet `character=` enter, the user's reference, or a project token. A mood adjective alone is not a signal. `first-character-costume=` is not a signal.

## Register

```txt
style=custom
register=<one sentence describing the visual language>
material=<source and why it belongs>
type_attitude=<role, contrast, and reading behavior>
interaction=<state or motion behavior and why>
signature=<one memorable detail and its object>
```

Leave an unused signal as `none`; do not invent four details to fill the schema. The signature is not a decorative accessory. It is visible in the first viewport: the enter mass, or the type attitude when Packet P0 perception is type. If it can leave the first viewport without weakening the Job or P0, cut it.

## Craft

Write craft at the same grain as a catalog style file, generated from the enter object and `character=`, not from a catalog `id`. Each line traces to the Job, an Inventory object, a user reference, or a project token. Do not copy hex, typefaces, or radius from a catalog file. Do not copy the costume (navy+Playfair, phosphor HUD, indigo cards).

```txt
material=<surface or artifact the interface borrows, and which object it is>
type_attitude=<how display and body behave; not a font shopping list>
motion=<what movement communicates; still is valid>
radius_shape=<one radius/shape rule tied to the object>
signature=<the same signature as the register>
```

Fill DESIGN.md leftover slots at this grain:

**Palette.** Name surface, ink, one accent, and where the accent sits (action, not atmosphere). Accent comes from the object or a user-named hue. Trust/document defaults to light paper/ink, not navy. Demo/instrument defaults to the artifact's material, not mesh. Impact/SaaS defaults to the product chrome already implied, not indigo-on-white. Neutrals-as-fear is not a palette.

**Type.** Display vs body roles, contrast ratio of sizes, tracking on labels. Name a family only when the pairing procedure or the project already chose it. Inter, Geist, and Outfit as unexamined brand defaults fail.

**Shape.** One radius/shape rule tied to the object (document = near-square text blocks; instrument = the artifact's corner; product UI = the app's existing radius).

**Depth.** One light story or none (hairline, ink, material grain). Glass, glow, and dual neon fail unless the object is light.

**Motion.** What movement communicates. Packet Behave `none` / `still` stays still.

A mood word, a catalog `id`, `first-character-costume=`, or a second palette fails this step. QA fails a register that reads as a renamed catalog style.

## Commit

Map the register onto the existing thesis, Frame, and DESIGN.md tokens. Custom language may fill type, material, motion, radius, shadow, and one signature detail; it may not rewrite occupancy, add objects, or create a second palette. Do not blend a catalog file into a custom register.

## QA

The visual rubric scores Language and Restraint. QA fails custom language when a signal is unsupported, the signature is missing from the first viewport or removable, the implementation reads as a named catalog style with a renamed label, or the surface vests `first-character-costume=`.

## Done

`style=custom` has a supported register, DESIGN.md records the chosen tokens and signature at catalog grain, and the rendered surface shows the register and the signature in the first viewport without changing the Packet's composition or wearing the costume.
