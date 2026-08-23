# Design Read examples

Load from the Direction slot ([dispatch.md](dispatch.md)) if the Lock shape is unclear. If Name, Audience, Success, Use, Scene, Theme, Palette, or Stack is still blank: close this file; the parent opens [briefing.md](briefing.md). Unnamed greenfield marketing Look is `you-decide` and does not block. Unnamed Behave and Constraints are `none` and do not block. Origin `redesign` with Aim, Keep, or Scope blank: same. App UI Scene is skipped (`none`) and does not block.

One sentence plus one Lock line before markup. These examples are **after** briefing answers (or invent-all). The personal-work-page prompt is [briefing.md](briefing.md#worked-example), not a Lock in this file.

## Format

```txt
Reading this as: <page kind> for <audience>, with a <vibe> language, leaning toward <register or design system>.
Lock: mode=<full|solo|fast>; origin=<greenfield|redesign|polish>; name=<briefing name or invented>; scene=<place/time/mood>; style=<id|custom|none>; theme=<light|dark|system>; color=<restrained|committed|full|drenched>; layout=<contained|offset|wild>; motion=<still|fluid|cinematic>; density=<airy|regular|dense>; stack=<detected, asked, or html+css+js>.
```

Product Locks also name the 1–2 Pareto screens. CMS/admin/CRM/list/editor/accounts also name `recipe=`. Settings outside those four: `recipe=none`. Marketing Locks name the one memorable break (or `break=none`) and, on greenfield/redesign, `folds=` from the *map*. `scene=` quotes briefing Scene or the composition sentence. `object-swap=` is a foreign P0 plus *because*, or `n/a` when Inventory has fewer than two domain nouns ([composition.md](composition.md#frame)). App UI, redesign, and polish lock `style=none` and leave [design-styles.md](design-styles.md) closed. Greenfield **marketing** `style=` is a craft path only when *tension* requires a named look; *composition* writes *job*, *objects*, *kinship*, the *frame*, the Sketch, the *thesis*, and the *map* ([composition.md](composition.md)). App UI recipes: [product-register.md](product-register.md#dashboards). Briefing runs first unless *invent-all*. Unanswered blanks: no Read, no Lock, no markup ([briefing.md](briefing.md)).

## Example 1: SaaS landing page

**Brief:** "Create a landing page for our new developer tool Uptime that monitors API uptime." Scene filled by the user: "the live status fills the left; the CTA sits in a narrow rail."

**Composition.** *job:* The user is here to start monitoring before the next outage. *objects:* live status (monitor), alert path (do), named outage (know), Start monitoring (decide). P0 perception = live status; P0 action = Start monitoring. *tension:* industrial heat + on-call precision. *joins:* split | stack | full-bleed. *discarded:* stack (three-up feature cards: status becomes a tile); full-bleed (manifesto-only type: CTA leaves the first viewport). *frame* from named Scene: enter = live status larger track; rest = Start monitoring in the rail; `break=none` — rack-LED is material on the enter *object*, not a gutter badge. *Sketch:* `[======= live status 8 =======][== Start monitoring 4 ==]` `join=split tracks=enter 8 rest 4 break none`. *thesis:* Start monitoring while the live status is still in view. Live status on the named larger track, Start monitoring in the rail. *folds=* live status | alert path | cut. *object-swap:* a kiln photo in enter does not read because the live status *is* the field.

> Reading this as: product landing for technical practitioners (SREs, backend devs), with a sharp / industrial language, leaning toward brand register with minimal color and monospace accents.
>
> Lock: origin=greenfield; name=Uptime; scene=the live status fills the left; the CTA sits in a narrow rail; style=industrial; theme=dark; color=restrained; layout=offset; motion=fluid; density=regular; stack=project CSS; folds=live status | alert path | cut

## Example 2: Dashboard settings (after briefing answers)

**Brief:** "Build the settings page for our analytics dashboard." Name was blank. Look skipped (`none`). User answered: name from chrome; theme=light; still.

**Composition.** *job:* The user is here to persist notification and retention settings. *objects:* notification row (do), retention window (compare), Save (decide). P0 perception = current values; P0 action = Save. `recipe=editor` from the settings shell. Occupancy numbers are `none`. `Sketch=none`.

> Reading this as: dense app UI for daily-use analysts, with a utilitarian / calm language, leaning toward product register with a restrained palette and one sans family.
>
> Lock: origin=greenfield; name=from app chrome; scene=none; style=none; theme=light; color=restrained; layout=contained; motion=still; density=dense; stack=project; recipe=editor; Pareto=notification + retention

## Example 3: Portfolio site (after briefing answers)

**Brief:** "Design a portfolio for a ceramic artist." Name, audience, success, use, scene, theme, and stack were blank, so the question interface ran one field per turn (Scene: `You decide from the brief` plus two occupancy readings). Look was unnamed (`you-decide`; no Catalog table). Behave unnamed = `none` (`motion=still`). The user answered: name=Atelier Sol; collectors; book a studio visit; Use=a scan of minutes; Scene=`you-decide`; light; html+css+js.

**Composition.** *job:* The user is here to book a studio visit. *objects:* kiln in fire (discover), featured works (compare), Book a studio visit (decide). P0 perception = kiln; P0 action = book. *tension:* industrial heat + calendar precision. *joins:* overlap | split | stack. *discarded:* split (equal three-up catalog); stack (manifesto type). `fallback=no`. *frame:* enter = kiln full-bleed; rest = Book a studio visit on the same mass; `break=none`. *Sketch:* `[============ kiln in fire 12 ============]` `join=overlap tracks=enter 12 rest inset break none`. *thesis:* Book the visit on the kiln that is still on. Kiln full-bleed, Book on that mass. *folds=* kiln in fire | featured works | cut. *object-swap:* a SaaS chart in enter does not read because the kiln photo is the field and Book is its label. Pick vests heat on the kiln mass (`industrial` only if *tension* requires that Path).

> Reading this as: portfolio for art-world visitors and collectors, with an organic / tactile language, leaning toward brand register with generous whitespace and a sans display pairing.
>
> Lock: origin=greenfield; name=Atelier Sol; scene=kiln in fire full-bleed, Book a studio visit on that mass; style=industrial; theme=light; color=committed; layout=offset; motion=still; density=airy; stack=html+css+js; folds=kiln in fire | featured works | cut

## Example 4: Restaurant homepage (after briefing answers)

**Brief:** "Homepage for a new fine-dining restaurant." Look filled (`fine-dining` maps to `luxury`). Scene filled: "candlelit dining room after service; the photograph takes the wide column." Name and stack were blank; the user answered name=Maré and html+css+js.

**Composition.** *job:* The user is here to reserve tonight's table. *objects:* dining-room photograph (discover), tonight's menu (compare), Reserve a table (decide). P0 perception = room; P0 action = reserve. *tension:* intimate dark + menu precision. *frame* from named Scene: enter = photograph wide column; rest = Reserve a table; *break* = menu as full-bleed band (the menu *is* the band). *Sketch:* `[======= dining-room photograph 8 =======][== Reserve a table 4 ==]` then `[============ tonight's menu 12 =============]` `join=split tracks=enter 8 rest 4 break 12`. *thesis:* Reserve while the room is still candlelit. Photograph wide, Reserve beside it, menu band. *folds=* photograph | tonight's menu | cut.

> Reading this as: marketing surface for reservation-driven diners, with a luxurious / intimate language, leaning toward brand register with a dark scene and high-contrast photography.
>
> Lock: origin=greenfield; name=Maré; scene=candlelit dining room after service; style=luxury; theme=dark; color=drenched; layout=offset; motion=fluid; density=airy; stack=html+css+js; folds=photograph | tonight's menu | cut; break=menu full-bleed band

Drenched is the Lock exemption from 60-30-10. The scene owns the palette.

## Example 5: Redesign an existing homepage

**Brief:** "The marketing homepage looks generic. Keep the URLs and the navy." Aim: first fold does not state the job. Keep: wordmark + nav + navy. Scope: this page.

**Composition.** *job* from Aim: The user is here to complete the action the first fold currently hides. *objects* from keep: current hero photo (discover), Aim action (decide), navy tokens (know). *tension:* current brand + a first fold that states the job. *discarded:* interchangeable slogan on the same split; three equal feature cards. *frame* from Aim + keep (no Scene ask): enter = existing photo on the larger track the photo already occupies; rest = Aim action; `break=none` unless a keep *object* is orphaned. *Sketch:* cells named from keep *objects*; `tracks=` matches that photo's current span. *thesis:* the first fold states the job on the current photo. *map:* from keep *objects* and those numbers.

> Reading this as: existing product landing for returning visitors, with a sharper language on the current tokens, leaning toward brand register on the current CSS stack.
>
> Lock: origin=redesign; name=existing wordmark; scene=same product, first fold states the job; style=none; theme=light; color=committed; layout=offset; motion=fluid; density=regular; stack=project CSS; aim=first fold states the job; keep=wordmark+nav+navy+slugs; scope=page; folds=current hero photo | Aim action | cut

Audit listed before the first visual edit, keep/retire against Aim. Navy stays. Slugs stay. Catalog stays closed.

## Example 6: Personal work page (stop)

**Brief:** "Create a unique web page to showcase my work. My background: I have been a software engineer for N years and created software … engineer pipeline …"

Filled: Job, Constraints (keep the named software). Blank: Name, Audience, Success, Use, Scene, Theme, Stack. Behave unnamed = `none`. Look unnamed = `you-decide`. "Unique" is not invent-all.

Do not write a Design Read or Lock in this turn. Close this file. Open [briefing.md](briefing.md) and ask **Name** through the host's question interface ([briefing.md](briefing.md#worked-example)). After every field has an owner, open [after-briefing.md](after-briefing.md).

## Example 7: Polish an existing settings page

**Brief:** "Tighten the settings page. Contrast is weak and the save button has no loading state."

Existing markup, DESIGN.md, and tokens. Origin=`polish`. Look, Name, Stack filled by disk. No Catalog. No new folds. Craft audit listed contrast (P0) and save-button loading state (P1) before the first visual edit.

> Reading this as: existing settings for daily-use analysts, with the current product language, leaning toward the in-repo design system.
>
> Lock: origin=polish; name=from app chrome; scene=same analyst bay; style=none; theme=light; color=restrained; layout=contained; motion=still; density=dense; stack=project; Pareto=overview + alert inbox.

## When to ask

This file is after answers. Missing briefing fields: close this file and ask the next blank through the host's question interface ([briefing.md](briefing.md)). Extra asks after answers only when:

- Brief says "for everyone" and the product is niche.
- Brief describes a dashboard and asks for wow-factor animation on every chrome control.
- Origin is unclear: new UI vs redesign this page from the briefing vs polish what is here.

Skip the briefing form on *invent-all*. Still split files and still write DESIGN.md.

## Done when

- Briefing answers (or invent-all) completed; `name=` is the user's string, `invented`, or disk. Greenfield **marketing** Scene is an occupancy sentence or `you-decide`; Look is a catalog id, refs, or `you-decide` (unnamed is `you-decide`). App UI Scene and Look are skipped (`none`) unless the user named an `id`. Redesign and polish Look is disk; `style=none`; Scene was not asked. Greenfield `theme=` is `light` / `dark` / `system` from briefing Theme; redesign and polish Theme is disk. Lock `theme=system` at Implement: [color.md](color.md#system-theme).
- Both Read and Lock lines exist before markup. They do not exist in the same turn as unanswered blanks.
- Origin is in the Lock (`greenfield`, `redesign`, or `polish`). Redesign Lock also has `aim=`, `keep=`, `scope=`.
- The sentence names audience and register. "Clean and modern" fails this. Greenfield marketing `you-decide` includes the Pick sentences matched to *tension* (or `style=none` when *tension* needs no named look). App UI does not write Pick.
- App UI and marketing always have a Design Read; isolated components inherit the parent surface or skip.
