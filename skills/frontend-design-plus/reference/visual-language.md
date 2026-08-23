# Custom visual language

Use when Direction cannot justify a catalog `id`, when the brief names a concrete reference that is not a catalog style, or when the domain object demands a register the catalog would turn into costume. Do not use it to avoid making a design decision.

## Contract

Set `style=custom` and write one compact register with at least three of these four signals:

- **Material** — the real surface, artifact, place, or physical behavior the interface borrows from;
- **Type attitude** — how type behaves, not merely a font name;
- **Interaction behavior** — how controls respond and what motion communicates;
- **Signature** — one visible detail that belongs to this product and would be lost if the lead object changed.

Every signal must trace to the Job, an Inventory object, the user's reference, or a project token. A mood adjective alone is not a signal.

## Register

```txt
style=custom
register=<one sentence describing the visual language>
material=<source and why it belongs>
type_attitude=<role, contrast, and reading behavior>
interaction=<state or motion behavior and why>
signature=<one memorable detail and its object>
```

Leave an unused signal as `none`; do not invent four details to fill the schema. The signature is not a decorative accessory. If it can leave without weakening the Job or P0, cut it.

## Craft

Write craft at the same grain as a catalog style file, generated from the object, not from a catalog `id`. Each line traces to the Job, an Inventory object, a user reference, or a project token. Do not copy hex, typefaces, or radius from a catalog file.

```txt
material=<surface or artifact the interface borrows, and which object it is>
type_attitude=<how display and body behave; not a font shopping list>
motion=<what movement communicates; still is valid>
radius_shape=<one radius/shape rule tied to the object>
signature=<the same signature as the register>
```

A mood word, a catalog `id`, or a second palette fails this step. QA fails a register that reads as a renamed catalog style.

## Commit

Map the register onto the existing thesis, Frame, and DESIGN.md tokens. Custom language may fill type, material, motion, radius, shadow, and one signature detail; it may not rewrite occupancy, add objects, or create a second palette. Do not blend a catalog file into a custom register.

## QA

The visual rubric scores Language and Restraint. QA fails custom language when a signal is unsupported, the signature is removable, or the implementation reads as a named catalog style with a renamed label.

## Done

`style=custom` has a supported register, DESIGN.md records the chosen tokens and signature, and the rendered surface shows the register without changing the Packet's composition.
