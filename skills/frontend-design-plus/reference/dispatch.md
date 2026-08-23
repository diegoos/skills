# Dispatch

Open from [after-briefing.md](after-briefing.md) after the Briefing card exists. Unanswered blanks: [briefing.md](briefing.md). Isolated component: skip this file ([after-briefing.md](after-briefing.md#isolated-component)).

The parent builds prompts and validates returns. It does not open composition, the Catalog, anti-slop, crit, pre-flight, implement, product-register, or ux-principles. Each slot receives the Briefing card (or Packet) plus the exact paths below. [load-map.md](load-map.md) is the path list; this file is the prompt contract.

If the harness can start a child agent (`Task` or equivalent), dispatch that slot as a child. That is the default. In-process only when that tool does not exist. Loading Direction, Implement, and QA into one window fails this file. In-process: open only that slot's paths. The carry into the next slot is the Packet (plus Implement file paths into QA). The child's transcript does not re-enter the parent except the return block.

Slots are sequential. Direction before markup. Implement before QA. Do not run Direction and Implement in parallel.

## Slots by origin

| Origin | Task | Direction | Implement | QA |
| --- | --- | --- | --- | --- |
| `greenfield` or `redesign` | marketing, app UI | yes | yes | yes |
| `polish` | marketing, app UI | yes (audit only; Catalog closed) | yes | yes |
| any | isolated component | skip | skip | skip |

Polish Direction opens [redesign.md](redesign.md) craft audit only. It does not open [composition.md](composition.md) or [design-styles.md](design-styles.md).

## Packet schema

Direction returns this block. Parent prints Design Read + Lock, then copies the Packet into the Implement prompt. A field the branch does not use is `none`.

```txt
Design Read: Reading this as: <page kind> for <audience>, with a <vibe> language, leaning toward <register or design system>.
Lock: origin=<greenfield|redesign|polish>; name=<briefing name or invented>; scene=<quoted Scene or composition sentence>; style=<id|none>; theme=<light|dark|system>; color=<restrained|committed|full|drenched>; layout=<contained|offset|wild>; motion=<still|fluid|cinematic>; density=<airy|regular|dense>; stack=<detected, asked, or html+css+js>.
Headlines: <H1 sentence> | <primary CTA>
  (app UI: three operator questions this view answers in ten seconds, then the primary-action sentence)
job=<The user is here to ______>
P0=perception: <object>; action: <object>
pattern=<named pattern>; fails here because <audience filter>
tension=<pair this product justifies>
discarded=<two occupancy cards: join token + job/P0/audience reason>
object-swap=<foreign P0> in enter does not read because <this job's kinship> | n/a | none
fallback=<yes|no>   (yes requires the words “fallback, not thesis”)
Inventory: <≤5 domain-noun + verb lines; Success on the list>
Cut: <three competing blocks named and off the page>
Frame:
  enter: <object> <occupancy>
  rest: <Success control> <occupancy>
  break: <object> <occupancy> | none — <why two masses>
Sketch: <12-col ASCII, 1–3 lines> then join=<stack|split|full-bleed|overlap> tracks=enter <n> rest <n|inset|below> break <n|none>   (marketing greenfield/redesign; else none)
Thesis: <experience of this product>. <enter / rest / break with occupancy, or two masses>
folds=<enter object> | <fold2 object> [| <fold3 object>|cut]   (marketing greenfield/redesign; polish: current family / none)
recipe=<queue-home|list-filter|editor|accounts|none> Pareto=<1-2 screens|none>
style_path=<design-styles/<id>.md|none>
Pick: <2–3 sentences, or none>
DESIGN.md: <path on disk>
```

Append on redesign: `aim=`, `keep=`, `scope=<first-viewport|page|flow>`. Invent-all: `name=` is a descriptive noun (`Invoice desk`, `API uptime`), never a coined startup or handle (`Nexus`, `Cloudly`, `swe-13`). Invent-all on redesign does not invent a brand or catalog `id`.

Quiet constraints (a11y-first, regulated, public-sector, kids) override Lock bands. Each dial must change spacing, layout family, or motion recipe. A Lock that only labels fails Direction.

### Valid packet

Parent checks before Implement. Re-dispatch Direction once with the named failure if invalid. Object-swap grammar: [composition.md](composition.md#frame) (do not reopen that file to recount; use the Packet Inventory lines).

Shared:

- Design Read and Lock lines exist. `scene=` quotes the briefing Scene or the composition sentence (app UI: `none` unless the briefing named occupancy).
- `DESIGN.md` is on disk. `name` matches the Briefing card.
- Lock `motion=still` when Behave is `none`. Lock `density=`: hours → dense; minutes → airy; Use `none` → regular.

Marketing **greenfield** or **redesign** — fail if any:

- `job=` uses a component name (hero, card, sidebar) or is not a do-phrase
- Inventory missing, >5 lines, Success absent, or a line is only `hero` / `card` / `section` / `CTA` / `feature` / `benefit` (unless that word is the product's object)
- `P0=` missing perception or action; Cut missing three competitors
- `pattern=` missing a name plus “fails here because”; `tension=` is a style id
- `discarded=` missing two cards, or the three *joins* are not three distinct tokens from `stack | split | full-bleed | overlap`
- Frame occupancy missing (two-mass page needs `break=none` plus why)
- Sketch absent, first-row cells not summing to 12, labels not ⊂ Inventory, footer `join=` not the surviving token, or `tracks=` mismatch Frame
- Thesis missing experience or occupancy; DESIGN.md **Layout** missing the Sketch
- `object-swap=` fails the Frame Object-swap check (`n/a` on ≥2 domain nouns; a `because` line on <2; omitted; foreign noun on Inventory; `because` cites no Inventory noun; swap still reads when the line is not `n/a`)
- `fallback=yes` without “fallback, not thesis”; `folds=` not from Inventory
- Look `you-decide` / invent-all: Pick sentences missing and `style=` not `none`

**App UI:** `style=none` unless Look is a named catalog `id`. `job=` and `P0=` present. Headlines are three operator questions plus the persist verb. CMS, CRM, admin home, list, editor, or accounts: `recipe=` and `Pareto=` set. Settings and other tools: `recipe=none` is valid. Occupancy numbers, `tension=`, `discarded=`, `object-swap=`, `fallback=`, Frame tracks, and Sketch are `none`. Greeting as the `h1` job fails.

**Polish:** `style=none`; Catalog closed; `Sketch=none`; `object-swap=none`; craft-audit P0/P1 named in Pick or Headlines; occupancy not required.

## Direction

Before any markup. Parent prompt:

```txt
Run the Direction slot for this surface. Do not write page markup.

Briefing card:
[field → quoted owner table from after-briefing.md]

Read ONLY these paths, then write DESIGN.md and return a Packet:
- [paths from load-map.md Direction rows for this origin + task + briefing signals]

Work: follow the done criteria in the attached files.
- Marketing greenfield/redesign: [composition.md](composition.md). Style as a craft path ([design-styles.md](design-styles.md)) only if *tension* requires a named look.
- App UI: [product-register.md](product-register.md). Catalog closed. `style=none` unless Look is a named id.
- Redesign: scan and audit first ([redesign.md](redesign.md)).
- Polish: craft audit only ([redesign.md](redesign.md#craft-audit)).

Map briefing onto Lock: Name → name=, Stack → stack=, Use → density= (hours → dense; minutes → airy; `none` → regular), Behave → motion= (none/still → still; hover/scroll → fluid; cinematic → cinematic), Theme → theme=, Look → style=, Scene → scene=. Color strategy when palette or theme is in play ([color.md](color.md#color-strategies)).

Return the Packet schema only. Do not open anti-slop.md, crit.md, preflight-checklist.md, or implement.md.
Do not open other files under reference/ than the paths listed.
```

Done when a valid Packet is in chat and DESIGN.md is on disk. Headlines that could sit on a CRM, a bank, and a dentist fail; rewrite before returning.

## Implement

Clean window. Parent prompt (first pass):

```txt
Run the Implement slot. Compose from the Packet. Do not reopen the briefing form.

Packet:
[full Packet from Direction]

Read ONLY these paths, then write or patch the surface:
- [implement.md](implement.md)
- DESIGN.md (path in Packet)
- [paths from load-map.md Implement rows]
- Packet style_path when not none

Done criterion is in implement.md. Marketing greenfield/redesign: return the `See:` / `tracks=` / `proof=` block from that file before folds. App UI: return the `main=` / `proof=` block from that file. Do not open anti-slop.md, crit.md, preflight-checklist.md, composition.md, design-styles.md, or briefing.md.
Do not open other files under reference/ than the paths listed.
```

Resume (after QA) — Packet plus the P0/P1 table only, not the QA transcript:

```txt
Resume Implement. Apply this P0/P1 table. Do not re-compose the *frame* or change `join=`. Correct `tracks=` CSS when the miss is occupancy.

Packet: [Lock + Thesis + Sketch + folds/recipe only]
P0/P1:
[table from QA]

Read ONLY: implement.md, DESIGN.md, the files you already wrote, and load-map Implement paths already attached.
Do not open anti-slop.md or crit.md.
```

Done when [implement.md](implement.md) done criterion holds. Marketing greenfield/redesign: the `See:` / `tracks=` / `proof=` block is in the child return. App UI: the `main=` / `proof=` block is in the child return. Missing block: re-dispatch Implement once — not Direction. One resume cycle per QA pass.

## QA

After markup exists on disk. Parent prompt:

```txt
Run the QA slot. Do not edit markup, CSS, or JS.

Packet:
[full Packet including Sketch]

Implement return:
[See / tracks / proof on marketing greenfield/redesign; main / proof on app UI; none on polish]

Files on disk: [paths Implement wrote]

Read ONLY these paths, then return a written triad and a P0/P1 table:
- [anti-slop.md](anti-slop.md)
- [crit.md](crit.md)
- [preflight-checklist.md](preflight-checklist.md) (tier from SKILL.md task routing)

Walk the primary task. Walk the render when the harness has a screenshot or browser this run; unverified visual tells are not a fail — do not invent them. Occupancy is not unverified: marketing greenfield/redesign Q1 needs Sketch, Implement `tracks=`, and `data-mass` ([crit.md](crit.md)). Question 1: marketing greenfield/redesign — `|measured − Sketch| ≤ 1` column; `See:` is the enter *object*; skip the object-swap fail when Packet `object-swap=n/a` ([composition.md](composition.md#frame)); when the line is not `n/a`, still-reads or a missing swap fails. Missing Sketch or `tracks=` fails. App UI: greeting in `main`, four equal KPI cards + donut, missing `main=` / `proof=`, or missing `recipe=` on a CMS/CRM/list/editor/accounts view. Settings: `recipe=none` is valid.

Return:
(a) What works
(b) User-goal failures
(c) One alternative (map / recipe / in-place craft — not a pixel tweak)
P0/P1 table: #, question, fail-if, finding, suggested fix
Pre-flight: each applicable box pass or fail, and what was not verified.

Do not edit. Do not open composition.md, design-styles.md, implement.md, or briefing.md.
Do not open other files under reference/ than the paths listed.
```

Done when the triad and P0/P1 table exist. Empty "no issues" without the scan in [crit.md](crit.md) fails. Parent keeps the triad and the P0/P1 table; it does not keep the QA walk. Parent resumes Implement when any P0 remains; re-dispatch QA only if a P0 still remains after that resume. Ship when Q1 holds and P0 count is 0.

## Completion criterion

Every required slot for this origin and task has returned. Direction Packet is valid. Implement files are on disk. Marketing greenfield/redesign: Implement returned `See:` / `tracks=` / `proof=`. App UI: Implement returned `main=` / `proof=`. QA triad exists. P0 count is 0, or the parent named why a remaining P0 is out of scope.
