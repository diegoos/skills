# Dispatch

Open from [after-briefing.md](after-briefing.md) after the Briefing card exists. Unanswered blanks: [briefing.md](briefing.md). Isolated component does not use the slots table below; follow [after-briefing.md](after-briefing.md#isolated-component) (Implement + Tier A in the parent window). Origin `polish` on marketing or app UI does not use this file; follow [polish.md](polish.md).

The parent builds prompts and validates returns against this schema. Closed files for the parent: [load-map.md](load-map.md#parent). Paste worker path strings into the prompt; do not open Direction, Implement, or QA bodies in the parent window except on isolated component. Each slot receives the Briefing card (or Packet) plus the exact paths below. [load-map.md](load-map.md) is the path list; this file is the prompt contract.

## Context budget

Parent keeps: Briefing card, the Packet text, DESIGN.md path, Implement file paths, QA triad / rubric / verification / P0/P1 table. Parent discards: Direction walk, Implement markup reasoning, QA scan notes. A worker transcript does not re-enter the parent except through its return block.

Implement is the builder. It needs a **layout kit** in its own window: the **full** Packet (not a slice), DESIGN.md on disk, [implement.md](implement.md), and every matching [load-map.md](load-map.md) Implement row. Occupancy for marketing is Sketch + `folds=` + DESIGN.md **Layout**. Occupancy for app UI is `recipe=` + `Pareto=` + DESIGN.md **Layout** plus [product-register.md](product-register.md) for that recipe. Do not attach [composition.md](composition.md) to Implement; Direction already committed Frame. Do not shrink the first-pass Packet. Resume after QA still sends the full Packet plus the P0/P1 table (not the QA walk), so Inventory nouns, Headlines, costume, and `style_path` stay available.

Open [execution-modes.md](execution-modes.md) with this file. In `full`, dispatch each slot to a worker when that capability exists. In `solo`, run the same slots sequentially in one window, open only the current slot's paths, and close those paths before the next slot. In `fast`, keep the slot order and apply the Fast stay-closed list in [load-map.md](load-map.md#fast). The carry into the next slot is the Packet (plus Implement file paths into QA).

Slots are sequential. Direction before markup. Implement before QA. Do not run Direction and Implement in parallel.

## Slots by origin

| Origin | Task | Direction | Implement | QA |
| --- | --- | --- | --- | --- |
| `greenfield` or `redesign` | marketing, app UI | yes | yes | yes |
| `polish` | marketing, app UI | skip this file | skip this file | skip this file |
| any | isolated component | skip this file | skip this file | skip this file |

Isolated component: [after-briefing.md](after-briefing.md#isolated-component) opens Implement in the parent. Polish marketing or app UI: [polish.md](polish.md). This table does not dispatch those tasks. Stay-closed for polish: [load-map.md](load-map.md#polish).

## Packet schema

Direction returns this block. Parent prints Design Read + Lock, then copies the Packet into the Implement prompt. A field the branch does not use is `none`. Origin `polish`: [polish.md](polish.md#slim-packet) instead.

```txt
Intent: job=<The user is here to ______>; success=<verb + object>
Layout: join=<stack|split|full-bleed|overlap|none> scan=<pyramid|Z|F|none> tracks=enter <n|none> rest <n|inset|below|none> break <n|none>   (marketing greenfield/redesign; app UI: recipe=<queue-home|list-filter|editor|accounts|none> instead of join/tracks)
Tokens: <3–7 DESIGN.md token names>
Design Read: Reading this as: <page kind> for <audience>, with a <vibe> language, leaning toward <register or design system>.
Lock: mode=<full|solo|fast>; origin=<greenfield|redesign|polish>; name=<briefing name or invented>; scene=<quoted Scene or composition sentence>; style=<id|custom|none>; theme=<light|dark|system>; color=<restrained|committed|full|drenched>; layout=<contained|offset|wild>; motion=<still|fluid|cinematic>; density=<airy|regular|dense>; stack=<detected, default html+css+js> [; questions=serial when briefing declared it].
Headlines: <H1 sentence> | <primary CTA = Success verb+object>
  (app UI: three operator questions this view answers in ten seconds, then the primary-action sentence)
job=<The user is here to ______>
character=risk=<trust|impact>; time=<document|scan|demo>; enter=<noun>; spectacle=<low|mid|high>   (marketing greenfield; else none)
first-character-costume=<category outfit this Job must not wear>   (marketing greenfield; else none)
direction=<A|B|none>
scan=<pyramid|Z|F|none>
form=<list|table|magazine|split-tasks|catalog-cards|none>
P0=perception: <object>; action: <object>
tension=<pair this product justifies, or none>
Inventory: <≤5 domain-noun + verb lines; Success on the list>
Cut: <three competing blocks named and off the page>
Sketch: <12-col ASCII, 1–3 lines> then join=<stack|split|full-bleed|overlap> tracks=enter <n> rest <n|inset|below> break <n|none> scan=<pyramid|Z|F> form=<list|table|magazine|split-tasks|catalog-cards>   (marketing greenfield/redesign occupancy; else none)
Thesis: <one experience sentence>
folds=<enter object>:<form> | <fold2 object>:<form> [| <fold3 object>:<form>|cut]   (marketing greenfield/redesign; else none)
recipe=<queue-home|list-filter|editor|accounts|none> Pareto=<1-2 screens|none>
style_path=<design-styles/<id>.md|none>
language_path=<visual-language.md|none>
Pick: <2–3 craft sentences when style=<id|custom>; none when style=none>
focus=<hierarchy|rhythm|color|states|a11y|distill|copy|none>
constraints=<quoted Constraints or none>
DESIGN.md: <path on disk>
```

Append on redesign: `aim=`, `keep=`, `scope=<first-viewport|page|flow>`. Invent-all: `name=` is a descriptive noun (`Invoice desk`, `API uptime`), never a coined startup or handle (`Nexus`, `Cloudly`, `swe-13`). Invent-all on redesign does not invent a brand or catalog `id`.

Quiet constraints (a11y-first, regulated, public-sector, kids) override Lock bands. Each dial must change spacing, motion recipe, or density. `layout=` is a containment band (center only when the Sketch already centers); it does not pick `join=`. A Lock that only labels fails Direction.

Direction writes Frame in the Direction slot. The parent does not open [composition.md](composition.md). The Packet occupancy is the Sketch footer, not a second Frame block.

### Valid packet

Parent checks the returned Packet text before Implement. Re-dispatch Direction once with the named failure if invalid. Do not open [composition.md](composition.md). Direction File done owns occupancy grammar; this list is presence and Sketch/Inventory string overlap only. Originality is not a Packet gate.

Shared (parent-only; composition does not own these):

- `Intent:` and `Tokens:` lines exist (3–7 token names). Marketing greenfield/redesign: `Layout:` has join/scan/tracks. App UI: `Layout:` is `recipe=` (or `none` on settings).
- Design Read and Lock lines exist. `scene=` quotes the briefing Scene or the composition sentence (app UI: `none` unless the briefing named occupancy).
- `mode=` matches the selected execution mode. Preserve `questions=serial` on the Lock when the briefing declared it.
- `DESIGN.md` is on disk. `name` matches the Briefing card.
- `focus=` exists. Origin `polish` does not use this schema ([polish.md](polish.md#slim-packet)). Other origins: `none`.
- `constraints=` exists (`none` is valid).
- Lock `motion=still` when Behave is `none`. Lock `density=` from briefing `time=` (document → regular or dense; scan → airy; demo → regular) or from named Use (hours → dense; minutes → airy; `none` → regular).
- Lock `theme=` from user or disk; else Direction craft after Frame (default `light`). Not navy-for-law or dark-HUD-for-tech.
- Headlines primary CTA is the Success verb+object.

Marketing **greenfield** or **redesign:** fail unless every line below exists on the Packet:

- `Inventory:` line present
- `Sketch:` with 1–3 ASCII lines and a footer that includes `join=` and `tracks=`
- `folds=` present; each remaining fold has `:<form>`
- greenfield: `first-character-costume=` is not empty

Then fail if:

- Sketch ASCII above the `join=` footer contains `hero`, `card`, `section`, `CTA`, `feature`, or `benefit` as a whole word, unless that word also appears on the `Inventory:` line
- Sketch ASCII above the footer shares no token of 3+ letters with `Inventory:` (split that line on spaces and punctuation; ignore `know`, `do`, `compare`, `discover`, `monitor`, `decide`)
- `style=` is the domain cliché (`professional` for a firm, `saas`/`enterprise` for “my SaaS”, `terminal`/`cyberpunk` for “tech”) **and** briefing Look did not name that id (prompt, Style pick, or Item)
- `style=custom`: `language_path=` missing
- `style=none`: `Pick:` is `none`. `style=<id>`: `Pick:` is 2–3 craft sentences. `style=custom`: `Pick:` names the signature

**App UI:** `style=none` unless Look is a named catalog `id` or the user explicitly requested a custom visual language. `job=` and `P0=` present. Headlines are three operator questions plus the persist verb. CMS, CRM, admin home, list, editor, or accounts: `recipe=` and `Pareto=` set. Settings and other tools: `recipe=none` is valid. Occupancy numbers, `character=`, `first-character-costume=`, `direction=`, `scan=`, `form=`, `tension=`, and Sketch are `none`. Greeting as the `h1` job fails.

**Polish:** skip this file. Slim packet: [polish.md](polish.md#slim-packet). Stay-closed: [load-map.md](load-map.md#polish).

## Direction

Before any markup. Parent prompt:

```txt
Run the Direction slot for this surface. Do not write page markup.

Briefing card:
[field → quoted owner table from after-briefing.md]

Read ONLY these paths, then write DESIGN.md and return a Packet:
- [paths from load-map.md Direction rows for this origin + task + briefing signals]

Work: follow the done criteria in the attached files. Use only the bullet that matches this origin and task.
- Marketing greenfield/redesign only: composition.md through File done (Frame + Sketch) before brand-register.md. A/B pick owns `join=`; invent-all writes one Sketch. Look `you-decide` → `style=none` and object craft. A named catalog `id` vests craft via design-styles.md after Frame. Do not match catalog **When** to invent an id. Open visual-language.md only for an explicit custom register. `layout=` does not pick `join=`.
- App UI only: product-register.md. Catalog closed. `style=none` unless Look is a named id (attach that one style file, not design-styles.md) or the user explicitly requested a custom register. `character=none`.
- Redesign (not polish): scan and audit first (redesign.md). Marketing still runs composition after the audit when that path is attached.
- Polish: do not run this slot ([polish.md](polish.md)).

Map briefing onto Lock: Mode → mode=, Name → name=, Stack → stack= (disk or html+css+js), character time → density=, Behave → motion= (none/still → still; hover/scroll → fluid; cinematic → cinematic), Theme → theme= (user/disk or craft after Frame, default light), Look → style=, Scene / A/B occupancy → scene=, Constraints → constraints=. `focus=none` on this slot. Color from the object or named Palette, not from the costume ([color.md](color.md#color-strategies) when attached).

Return the Packet schema only. Do not copy `Frame:` into the Packet. Do not open anti-slop.md, crit.md, preflight-checklist.md, or implement.md.
Do not open other files under reference/ than the paths listed.
```

Done when a valid Packet is in chat and DESIGN.md is on disk. Headlines H1 names an Inventory or Success object, and H1 and the primary CTA *divide* (each does one job). Headlines that could sit on a CRM, a bank, and a dentist fail; rewrite before returning.

## Implement

Clean window. Parent prompt (first pass):

```txt
Run the Implement slot. Compose from the layout kit. Do not reopen the briefing form. Do not reopen composition.md.

Layout kit:
[full Packet from Direction — every field, including Inventory, Headlines, Sketch, folds/recipe, Pick, style_path, language_path, constraints, DESIGN.md path]

Read ONLY these paths, then write or patch the surface:
- [implement.md](implement.md)
- DESIGN.md (path in Packet)
- [paths from load-map.md Implement rows]
- Packet style_path when not none
- Packet language_path when not none

Done criterion is in implement.md. Marketing greenfield/redesign: return the `See:` / `tracks=` / `scale=` / `proof=` / `distinct=` / `cta=` block from that file before folds. App UI: return the `main=` / `proof=` block from that file. Do not change Packet `recipe=` or `join=`. Return the [verification](verification.md) block after viewport proof. Do not open anti-slop.md, crit.md, preflight-checklist.md, composition.md, design-styles.md, visual-rubric.md, or briefing.md.
Do not open other files under reference/ than the paths listed.
```

Resume (after QA) — full Packet plus the P0/P1 table, not the QA transcript:

```txt
Resume Implement. Apply this P0/P1 table. Do not re-compose the *frame* or change `join=` or `recipe=`. Correct `tracks=` CSS or enter type scale when the miss is occupancy or `scale=`.

Layout kit: [full Packet from Direction]
P0/P1:
[table from QA]

Read ONLY: implement.md, DESIGN.md, the files you already wrote, and load-map Implement paths already attached.
Do not open anti-slop.md, crit.md, or composition.md.
```

Done when [implement.md](implement.md) done criterion holds. Marketing greenfield/redesign: the `See:` / `tracks=` / `scale=` / `proof=` / `distinct=` / `cta=` block is in the child return. App UI: the `main=` / `proof=` block is in the child return. The verification block exists. Missing block: re-dispatch Implement once — not Direction. One resume cycle per QA pass.

## QA

After markup exists on disk. Parent prompt:

```txt
Run the QA slot. Do not edit markup, CSS, or JS.

Packet:
[full Packet including Sketch]

Implement return:
[See / tracks / scale / proof / distinct / cta on marketing greenfield/redesign; main / proof on app UI; none on polish]

Files on disk: [paths Implement wrote]

Read ONLY these paths, then return a written triad, rubric, verification block, and a P0/P1 table:
- [anti-slop.md](anti-slop.md)
- [crit.md](crit.md)
- [visual-rubric.md](visual-rubric.md)
- [quality-cases.md](quality-cases.md)
- [verification.md](verification.md)
- [performance.md](performance.md) when origin is marketing greenfield or redesign
- [preflight-checklist.md](preflight-checklist.md) (tier from SKILL.md task routing)

Walk the primary task. Walk the render when the harness has a screenshot or browser this run. Occupancy visual claims on marketing greenfield/redesign (costume off screen, logo-swap, `See:` visible in enter) are P0 if that tool existed and was unused ([verification.md](verification.md#ship-rule)). Other unverified visual tells are not a fail — do not invent them. Occupancy on marketing greenfield/redesign is [crit.md](crit.md) Q1. App UI Q1 is `main=` / `proof=` against `recipe=`. Do not restate Q1 grammar here.

Return two blocks in one table (one slot; no second worker):
A occupancy — Q1, Sketch/`tracks=`/`See:` (marketing) or `main=`/`proof=` (app UI), costume, CTA.
B production — pre-flight tier counts, contrast, overflow, states.
Then:
(a) What works
(b) User-goal failures
(c) One alternative (map / recipe / in-place craft — not a pixel tweak)
(d) The [visual-rubric.md](visual-rubric.md) return block
(e) The [verification.md](verification.md) return block
P0/P1 table: #, question, fail-if, finding, suggested fix; `rule=` when an [anti-slop.md](anti-slop.md#rule-ids) id matches
Pre-flight: each applicable box pass or fail, and what was not verified.

Do not edit. Do not open composition.md, design-styles.md, implement.md, or briefing.md.
Do not open other files under reference/ than the paths listed.
```

Done when the triad, rubric, verification block, and P0/P1 table exist. Empty "no issues" without the scan in [crit.md](crit.md) fails. Parent keeps the triad, rubric, verification, and P0/P1 table; it does not keep the QA walk. Parent resumes Implement when any P0 remains; re-dispatch QA only if a P0 still remains after that resume. Ship when Q1 holds, the rubric threshold holds, and P0 count is 0.

## Completion criterion

Every required slot for this origin and task has returned. Origin `polish`: [polish.md](polish.md#file-done). Direction Packet is valid. Implement files are on disk. Marketing greenfield/redesign: Implement returned `See:` / `tracks=` / `scale=` / `proof=` / `distinct=` / `cta=`. App UI: Implement returned `main=` / `proof=`. Implement and QA returned the verification block. QA triad and rubric exist. P0 count is 0, or the parent named why a remaining P0 is out of scope.
