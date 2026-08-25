# After briefing

Open this file when every briefing field has an owner (quoted user string, disk evidence, inferred `character=`, A/B pick, working title, Look after Style or a named `id`, you-decide on Scene when invent-all, unnamed Behave or Constraints as `none`, or invent-all), or when the form was skipped (*invent-all*). Origin `polish` on marketing or app UI: close this file and open [polish.md](polish.md). Isolated component: [Isolated component](#isolated-component). If Job, occupancy, or Style is still blank on greenfield marketing, open [briefing.md](briefing.md) instead.

The parent orchestrates. Closed files: [load-map.md](load-map.md#parent). Slot paths attach from [dispatch.md](dispatch.md) and [load-map.md](load-map.md). Open [execution-modes.md](execution-modes.md) here for capability fallbacks and to preserve `questions=serial` when briefing declared it. The parent validates the Packet against the schema in [dispatch.md](dispatch.md#valid-packet). It does not open composition to interpret the design. Origin `polish`: [polish.md](polish.md) owns the slim packet; do not validate against the Direction schema.

## Pace

- **Pack, then dispatch.** Write the Briefing card, preserve `mode=` (and `questions=serial` when declared), and open [dispatch.md](dispatch.md). Do not start markup in this file.
- **One surface per pass.** Finish QA + P0 resume on that surface before the next page or variant.
- **Pause on reflex.** Invalid Packet ([dispatch.md](dispatch.md#valid-packet)) means Direction is not done — re-dispatch Direction, do not implement.

## Isolated component

Skip [dispatch.md](dispatch.md). Open [implement.md](implement.md) and the Component rows in [load-map.md](load-map.md). Origin `polish` or `redesign`: also open [redesign.md](redesign.md#craft-audit) (polish) or [redesign.md](redesign.md) (redesign) in this window. Run [anti-slop.md](anti-slop.md) **Always** (Dashboard tells only if the component is a KPI strip or chart). Ship Tier A in [preflight-checklist.md](preflight-checklist.md); skip the *Crit* written box (no crit slot). Return the [verification.md](verification.md) block. [visual-rubric.md](visual-rubric.md) when scoring craft: skip Structural necessity and Domain specificity. Catalog, composition, and marketing folds stay closed.

Done when Tier A boxes are checked or failed and fixed, Always slop has run, and the verification block exists.

## Briefing card

Write a compact table: field → quoted owner. Every applicable field from [briefing.md](briefing.md) has a cell, including `character=`, `first-character-costume=`, and `direction=` on greenfield marketing. Skip this heading on polish ([polish.md](polish.md)). `none`, `you-decide`, inferred owners, and disk evidence count as owners. If [product-context.md](product-context.md) scored `evidence=` / `commitments=` / `anti-refs=`, copy those cells; do not reopen that file here.

Invent-all on redesign does not invent a brand or catalog `id`. Fill Aim = first viewport declares the job, Keep = wordmark + nav + tokens, Scope = this page, unless the user named others.

Invent-all name: a descriptive noun from the job (`Invoice desk`, `API uptime`), never a coined startup or handle (`Nexus`, `Cloudly`, `swe-13`). Lock will use `name=invented` with that noun.

Done when every applicable field has a quoted cell. Then open [dispatch.md](dispatch.md).

## Workflow

Isolated component: stop at [Isolated component](#isolated-component). Do not run the slots below.

1. **Direction.** Dispatch the Direction slot ([dispatch.md](dispatch.md#direction)). Attach only [load-map.md](load-map.md) Direction rows. Done when a valid Packet is in chat, `mode=` is declared, and DESIGN.md is on disk. Invalid packet: re-dispatch Direction once with the failure named. Do not dispatch Implement until the packet is valid. In `solo`, close Direction references before opening Implement paths. The Packet is the only carry.
2. **Declare.** Print the Packet Design Read and Lock in chat. No markup from the parent. Constraints that include a voice sample own the headline register; otherwise Headlines stay in the Packet voice.
3. **Implement.** Dispatch the Implement slot with the layout kit in [dispatch.md](dispatch.md#implement) (full Packet + DESIGN.md + Implement rows). Done when [implement.md](implement.md) done criterion holds and the Verification block exists. Marketing greenfield/redesign without the `See:` / `tracks=` / `scale=` / `proof=` / `distinct=` / `cta=` return: re-dispatch Implement once — not Direction. App UI without the `main=` / `proof=` return: re-dispatch Implement once — not Direction. Parent does not keep the Implement walk.
4. **QA.** Dispatch the QA slot ([dispatch.md](dispatch.md#qa)). Done when the written triad, visual rubric, verification block, and P0/P1 table exist. Praise does not ship.
5. **Fix.** If any P0 remains, the rubric threshold fails, or verification has a failed required check: resume Implement with the relevant table only (not the QA transcript). One fix cycle. Re-dispatch QA only if a P0 still remains. Done when the QA table shows Q1 holding, the rubric threshold holds, and P0 count is 0. `tracks=` or `scale=` miss: resume Implement; do not recompose `join=`. Q1 occupancy still failing after resume (wrong `See:`, missing Sketch): re-dispatch Direction. Resume does not invent Inventory nouns. Unused screenshot/browser this run on occupancy visual claims is P0 (QA verification `proof=` / `not-verified=`). Other unverified checks remain a limitation unless the user requested evidence for that check, in which case they are P1.

Product chrome stays consistent. If the Lock shape is unclear, the parent re-dispatches Direction with [design-read-examples.md](design-read-examples.md) attached — the parent does not open that file itself.

## File done

Briefing card exists. Direction Packet is valid. Design Read and Lock were printed. Implement files are on disk. Verification and rubric blocks exist. QA triad exists. P0 count is 0. Origin `polish` does not use this heading ([polish.md](polish.md#file-done)).
