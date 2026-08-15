# Design Read examples

One sentence plus one Lock line before markup.

## Format

```txt
Reading this as: <page kind> for <audience>, with a <vibe> language, leaning toward <register or design system>.
Lock: origin=<greenfield|redesign>; scene=<place/time/mood>; color=<restrained|committed|full|drenched>; layout=<contained|offset|wild>; motion=<still|fluid|cinematic>; density=<airy|regular|dense>; stack=<detected or asked>.
```

Product Locks also name the 1–2 Pareto screens. Marketing Locks name the one memorable break. Redesign Locks also name `mode=preserve|overhaul`.

## Example 1: SaaS landing page

**Brief:** "Create a landing page for our new developer tool that monitors API uptime."

> Reading this as: product landing for technical practitioners (SREs, backend devs), with a sharp / industrial language, leaning toward brand register with minimal color and monospace accents.
>
> Lock: origin=greenfield; scene=overnight NOC with rack LEDs; color=restrained; layout=offset; motion=fluid; density=regular; stack=project CSS.

## Example 2: Dashboard settings

**Brief:** "Build the settings page for our analytics dashboard."

> Reading this as: dense app UI for daily-use analysts, with a utilitarian / calm language, leaning toward product register with a restrained palette and one sans family.
>
> Lock: origin=greenfield; scene=fluorescent analyst bay, day shift; color=restrained; layout=contained; motion=still; density=dense; stack=project; Pareto=overview + alert inbox.

## Example 3: Portfolio site

**Brief:** "Design a portfolio for a ceramic artist."

> Reading this as: portfolio for art-world visitors and collectors, with an organic / tactile language, leaning toward brand register with generous whitespace and a sans display pairing.
>
> Lock: origin=greenfield; scene=sunlit studio shelf of unglazed ware; color=committed; layout=wild; motion=still; density=airy; stack=asked; break=one full-bleed kiln photo.

## Example 4: Restaurant homepage

**Brief:** "Homepage for a new fine-dining restaurant."

> Reading this as: marketing surface for reservation-driven diners, with a luxurious / intimate language, leaning toward brand register with a dark scene and high-contrast photography.
>
> Lock: origin=greenfield; scene=candlelit dining room after service; color=drenched; layout=offset; motion=fluid; density=airy; stack=asked; break=container-free menu fold.

Drenched is the Lock exemption from 60-30-10. The scene owns the palette.

## Example 5: Redesign an existing homepage

**Brief:** "The marketing homepage looks generic. Keep the URLs and the navy."

> Reading this as: existing product landing for returning visitors, with a sharper industrial language, leaning toward brand register on the current CSS stack.
>
> Lock: origin=redesign; mode=preserve; scene=same product, daylight office; color=committed; layout=offset; motion=fluid; density=regular; stack=project CSS; break=asymmetric split on the current hero photo.

Audit listed before the first visual edit. Navy stays. Slugs stay.

## When to ask one question

Ask once when the read diverges from the brief:

- Brief says "for everyone" and the product is niche.
- Brief describes a dashboard and asks for wow-factor animation on every chrome control.
- Brief has no aesthetic clue and two directions are equally valid.
- Stack matters and the repo does not reveal one.
- Origin is unclear: new UI vs an existing page. Preserve vs overhaul is unclear on a redesign.

## Done when

- Both lines exist before markup.
- Origin is in the Lock (`greenfield` or `redesign`).
- The sentence names audience and register. "Clean and modern" fails this.
- One clarifying question at most.
- App UI and marketing always have a Design Read; isolated components inherit the parent surface or skip.
