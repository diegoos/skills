# Design styles

Named styles are agent guides. They describe how a look behaves: type attitude, material, motion, density, and the cliché to refuse. The design the user already chose stays in charge.

Keep, in this order: briefing answers, Scene occupancy, Look, DESIGN.md, project tokens. Then use this folder to fill leftover blanks. Packet `folds=` already lists leftover *objects* with `:<form>`. Packet `recipe=` owns app UI layout. A named style vests craft after occupancy exists. Do not reopen [composition.md](composition.md) or [product-register.md](product-register.md) from this file.

## Load

Open this file in the Direction slot when Look is a catalog `id` or 1–3 sites with a craft *why* ([load-map.md](load-map.md)). Hex and typefaces in the matching style file are fallbacks for empty color and type slots. Do not open this folder at Classify. Briefing opens [catalog.md](catalog.md) only on Style pick after yes ([briefing.md](briefing.md#look)). Do not open this folder on Look `you-decide` / invent-all: Lock `style=none`. The parent orchestrator does not open this file.

On app UI, leave this folder closed and Lock `style=none`, unless Look is a named catalog `id` (craft blanks only; layout stays [product-register.md](product-register.md)). On `redesign` or `polish`, follow DESIGN.md, project tokens, and the current CSS. Leave this folder closed. Lock `style=none`. Origin detection: SKILL.md Classify; existing-surface rules: [redesign.md](redesign.md).

## Pick

Greenfield **marketing** only, after briefing answers (or invent-all). Skip this section on app UI except a named catalog `id` (step 1 only). Unnamed greenfield marketing Look that survived Style **no** is `you-decide` ([briefing.md](briefing.md#look)).

**Domain-cliché cluster** (`professional` on a law/consulting Job, `saas` / `enterprise` on "my SaaS", `terminal` / `cyberpunk` / `web3` on "tech"): not a Pick because the Job named that industry. Authorship (user named the id in the prompt or Style pick) still takes step 1. Packet `first-character-costume=` is this cluster in outfit form — refuse the matching `id` unless the user named it.

**Quiet-chrome cluster**, **Second-hop cluster**, and **Model-default triad**: refuse as a default on `you-decide` / invent-all. Do not match a catalog **When** to invent an `id`. Brief names it, brief wins.

1. If Look or the prompt names an `id` from the catalog, use that id. If it names an Item number, map it from the briefing table or open [catalog.md](catalog.md). Authorship wins. QA still runs the slop test. If that id *is* `first-character-costume=` and the user did not name it, treat as unnamed and continue at step 2.
2. Else if Look is `you-decide` or `none` (Style **no**, unnamed after they declined, or invent-all): set `style=none` and fill craft from the enter object in DESIGN.md. Open [visual-language.md](visual-language.md) only when writing an explicit custom register (`style=custom`). Do not pick a catalog `id` by matching **When** or *tension*. Scene occupancy is not a license for `newsprint`, `botanical`, or `cyberpunk`.
3. Else if Look names sites or a metaphor without an id: open [catalog.md](catalog.md). Map one clause of *why* onto one row **Description** (or `id`). Attach that one style file. Do not open the rest of `design-styles/` to hunt **When**. Do not blend two files. Cap 1–3 refs. A *why* that only restates the industry maps to `style=none` plus object craft, or to `style=custom` if writing a register, not to the domain-cliché `id`.
4. Write `style=<id>`, `style=custom`, or `style=none` on the Lock. Done when that value is in the Lock, the matching file or custom register is in context when not `none`, `style=none` needs no Pick paragraph, and `style=` does not vest `first-character-costume=` unless the user named that id.

Skip this folder when the user named a live component library to follow as-is (Polaris, Carbon, USWDS, Fluent 2, Spectrum). `style=none`. Quiet constraints still override Lock bands.

## Commit

After the one catalog file or custom register is in context, map Craft onto the *thesis* already in DESIGN.md **Layout**. Extract type, material, motion, radius, and shadow from that file's Craft and Path, or from [visual-language.md](visual-language.md). Do not invent a second id. Do not choose a hero family here. Craft does not rewrite Frame occupancy. A Path that names a hero family loses to the Sketch. Do not reopen [composition.md](composition.md); occupancy is already in the Packet.

- **Spatial** — confirm occupancy numbers and type-scale jump from the Sketch; fill gutters, radius set, shadow recipe, motion `150–250ms ease-out` only where DESIGN.md left them blank (cinematic Lock may exceed that band).
- **One loud thing** — numeric contrast that serves the *break* mass when one exists: display type ≥3× body, or one block spanning most of the first viewport, or radius `0` against `4px` controls. Two-mass page: enter/rest contrast is the loud thing. Marketing Lock already names this break.
- **Folds** — confirm `folds=` from the Packet. A missing `:<form>` or a family that rewrites occupancy fails Direction, not this Path.
- **Subtraction** — the Path cliché to delete until Job + Success still hold.
- **Forbids** — that Path cliché. Pair it with the do-instead already in this file's Path.

A second style's tokens in CSS fail this step.

## Catalog

Ids and Item numbers live in [catalog.md](catalog.md). Briefing prints that table only after Style **yes**. Direction opens [catalog.md](catalog.md) when Look is an Item number and the table is not already in chat. On `you-decide` / invent-all, keep [catalog.md](catalog.md) closed. A named `id` attaches that one style file ([load-map.md](load-map.md)). Lock names an id. Occupancy and recipe stay in the Packet.
