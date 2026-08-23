# After briefing

Open this file when every briefing field has an owner (quoted user string, disk evidence, you-decide on Look or Scene — including unnamed greenfield marketing Look — unnamed Behave or Constraints as `none`, or invent-all), or when the form was skipped (*invent-all*, or polish with no blanks). If a blank remains, open [briefing.md](briefing.md) instead.

The parent orchestrates. It does not open [composition.md](composition.md), [design-styles.md](design-styles.md), `design-styles/*.md`, [anti-slop.md](anti-slop.md), [crit.md](crit.md), [preflight-checklist.md](preflight-checklist.md), [product-register.md](product-register.md), or [ux-principles.md](ux-principles.md). Slot paths attach from [dispatch.md](dispatch.md) and [load-map.md](load-map.md).

## Pace

- **Pack, then dispatch.** Write the Briefing card. Open [dispatch.md](dispatch.md). Do not start markup in this file.
- **One surface per pass.** Finish QA + P0 resume on that surface before the next page or variant.
- **Pause on reflex.** A missing Packet *thesis*, missing Sketch on marketing greenfield/redesign, Inventory lines that are only `hero` / `card` / `CTA`, `object-swap=` that fails the Frame check ([composition.md](composition.md#frame): `n/a` illegal on a rich Inventory; a `because` line illegal on a thin one; still-reads when the line is not `n/a`), four equal KPI cards with Welcome back, or a CMS/CRM/list/editor/accounts view with `recipe=` missing, means Direction is not done — re-dispatch Direction, do not implement.

## Isolated component

Skip [dispatch.md](dispatch.md). Open [implement.md](implement.md) and the Component rows in [load-map.md](load-map.md). Ship Tier A in [preflight-checklist.md](preflight-checklist.md) in this window. Catalog, composition, and marketing folds stay closed.

Done when that surface's pre-flight A boxes are checked or failed and fixed.

## Briefing card

Write a compact table: field → quoted owner. Every applicable field from [briefing.md](briefing.md) has a cell. `none`, `you-decide`, and disk evidence count as owners.

Invent-all on redesign does not invent a brand or catalog `id`. Fill Aim = first viewport declares the job, Keep = wordmark + nav + tokens, Scope = this page, unless the user named others.

Invent-all name: a descriptive noun from the job (`Invoice desk`, `API uptime`), never a coined startup or handle (`Nexus`, `Cloudly`, `swe-13`). Lock will use `name=invented` with that noun.

Done when every applicable field has a quoted cell. Then open [dispatch.md](dispatch.md).

## Workflow

1. **Direction.** Dispatch the Direction slot ([dispatch.md](dispatch.md#direction)). Attach only [load-map.md](load-map.md) Direction rows. Done when a valid Packet is in chat and DESIGN.md is on disk. Invalid packet: re-dispatch Direction once with the failure named. Do not dispatch Implement until the packet is valid.
2. **Declare.** Print the Packet Design Read and Lock in chat. No markup from the parent. Constraints that include a voice sample own the headline register; otherwise Headlines stay in the Packet voice.
3. **Implement.** Dispatch the Implement slot with the full Packet and [load-map.md](load-map.md) Implement rows. Done when [implement.md](implement.md) done criterion holds. Marketing greenfield/redesign without the `See:` / `tracks=` / `proof=` return: re-dispatch Implement once — not Direction. App UI without the `main=` / `proof=` return: re-dispatch Implement once — not Direction.
4. **QA.** Dispatch the QA slot ([dispatch.md](dispatch.md#qa)). Done when the written triad and the P0/P1 table exist. Praise does not ship.
5. **Fix.** If any P0 remains: resume Implement with that table only (not the QA transcript). One fix cycle. Re-dispatch QA only if a P0 still remains. Done when question 1 holds (first viewport matches the Sketch and measured `tracks=`, or polish kept the current family) and P0 count is 0. `tracks=` off Sketch by more than ±1 column: resume Implement; do not recompose `join=`. `See:` names an object that is not Sketch enter, or Sketch missing: re-dispatch Direction. `object-swap=` still reading against measured enter: re-dispatch Direction only when the Packet line is not `n/a`. Resume does not invent Inventory nouns to turn `n/a` into a swap. App UI: greeting in `main`, missing `main=` / `proof=`, or a missing `recipe=` on a CMS/CRM/list/editor/accounts view fails Q1. Settings `recipe=none` does not fail Q1.

Product chrome stays consistent. If the Lock shape is unclear, the parent re-dispatches Direction with [design-read-examples.md](design-read-examples.md) attached — the parent does not open that file itself.

## File done

Briefing card exists. Direction Packet is valid. Design Read and Lock were printed. Implement files are on disk. QA triad exists. P0 count is 0.
