# Design Read examples

One sentence plus one Lock line before markup.

## Format

```txt
Reading this as: <page kind> for <audience>, with a <vibe> language, leaning toward <register or design system>.
Lock: origin=<greenfield|redesign>; name=<briefing name or invented>; scene=<place/time/mood>; color=<restrained|committed|full|drenched>; layout=<contained|offset|wild>; motion=<still|fluid|cinematic>; density=<airy|regular|dense>; stack=<detected, asked, or html+css+js>.
```

Product Locks also name the 1–2 Pareto screens. Marketing Locks name the one memorable break. Redesign Locks also name `mode=preserve|overhaul`. Briefing runs first unless _invent-all_. Unanswered blanks: no Read, no Lock, no markup ([briefing.md](briefing.md)).

## Example 1: SaaS landing page

**Brief:** "Create a landing page for our new developer tool Uptime that monitors API uptime."

> Reading this as: product landing for technical practitioners (SREs, backend devs), with a sharp / industrial language, leaning toward brand register with minimal color and monospace accents.
>
> Lock: origin=greenfield; name=Uptime; scene=overnight NOC with rack LEDs; color=restrained; layout=offset; motion=fluid; density=regular; stack=project CSS.

## Example 2: Dashboard settings

**Brief:** "Build the settings page for our analytics dashboard."

> Reading this as: dense app UI for daily-use analysts, with a utilitarian / calm language, leaning toward product register with a restrained palette and one sans family.
>
> Lock: origin=greenfield; name=from app chrome; scene=fluorescent analyst bay, day shift; color=restrained; layout=contained; motion=still; density=dense; stack=project; Pareto=overview + alert inbox.

## Example 3: Portfolio site (after briefing answers)

**Brief:** "Design a portfolio for a ceramic artist." Name, audience, success, look, and stack were blank, so the briefing batch ran and the user answered: name=Atelier Sol; collectors; book a studio visit; none; html+css+js.

> Reading this as: portfolio for art-world visitors and collectors, with an organic / tactile language, leaning toward brand register with generous whitespace and a sans display pairing.
>
> Lock: origin=greenfield; name=Atelier Sol; scene=sunlit studio shelf of unglazed ware; color=committed; layout=wild; motion=still; density=airy; stack=html+css+js; break=one full-bleed kiln photo.

## Example 4: Restaurant homepage (after briefing answers)

**Brief:** "Homepage for a new fine-dining restaurant." Name and stack were blank; the user answered name=Maré and html+css+js.

> Reading this as: marketing surface for reservation-driven diners, with a luxurious / intimate language, leaning toward brand register with a dark scene and high-contrast photography.
>
> Lock: origin=greenfield; name=Maré; scene=candlelit dining room after service; color=drenched; layout=offset; motion=fluid; density=airy; stack=html+css+js; break=container-free menu fold.

Drenched is the Lock exemption from 60-30-10. The scene owns the palette.

## Example 5: Redesign an existing homepage

**Brief:** "The marketing homepage looks generic. Keep the URLs and the navy."

> Reading this as: existing product landing for returning visitors, with a sharper industrial language, leaning toward brand register on the current CSS stack.
>
> Lock: origin=redesign; mode=preserve; name=existing wordmark; scene=same product, daylight office; color=committed; layout=offset; motion=fluid; density=regular; stack=project CSS; break=asymmetric split on the current hero photo.

Audit listed before the first visual edit. Navy stays. Slugs stay.

## Example 6: Personal work page (stop)

**Brief:** "Create a unique web page to showcase my work. My background: I have been a software engineer for N years and created software … engineer pipeline …"

Filled: Job, Constraints (keep the named software). Blank: Name, Audience, Success, Use, Look, Stack. "Unique" is not invent-all.

Do not write a Design Read or Lock in this turn. Ask the blanks ([briefing.md](briefing.md#worked-example)). After answers, resume at workflow step 3.

## When to ask

Missing briefing fields go in **one** batch ([briefing.md](briefing.md)), not a drip of single questions. A confident inference does not skip the form. Extra asks after answers only when:

- Brief says "for everyone" and the product is niche.
- Brief describes a dashboard and asks for wow-factor animation on every chrome control.
- Origin is unclear: new UI vs an existing page. Preserve vs overhaul is unclear on a redesign.

Skip the briefing form on _invent-all_. Still split files and still write DESIGN.md.

## Done when

- Briefing answers (or invent-all) completed; `name=` is the user's string or `invented`.
- Both Read and Lock lines exist before markup. They do not exist in the same turn as unanswered blanks.
- Origin is in the Lock (`greenfield` or `redesign`).
- The sentence names audience and register. "Clean and modern" fails this.
- App UI and marketing always have a Design Read; isolated components inherit the parent surface or skip.
