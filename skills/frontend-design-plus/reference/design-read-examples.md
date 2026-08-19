# Design Read examples

Load from [after-briefing.md](after-briefing.md) at Declare if the Lock shape is unclear. If Name, Audience, Success, Use, Look, Theme, Palette, Behave, or Stack is still blank: close this file and open [briefing.md](briefing.md).

One sentence plus one Lock line before markup. These examples are **after** briefing answers (or invent-all). The personal-work-page prompt is [briefing.md](briefing.md#worked-example), not a Lock in this file.

## Format

```txt
Reading this as: <page kind> for <audience>, with a <vibe> language, leaning toward <register or design system>.
Lock: origin=<greenfield|redesign|polish>; name=<briefing name or invented>; scene=<place/time/mood>; style=<id|none>; theme=<light|dark|system>; color=<restrained|committed|full|drenched>; layout=<contained|offset|wild>; motion=<still|fluid|cinematic>; density=<airy|regular|dense>; stack=<detected, asked, or html+css+js>.
```

Product Locks also name the 1–2 Pareto screens. Marketing Locks name the one memorable break. App UI, redesign, and polish lock `style=none` and leave [design-styles.md](design-styles.md) closed. Greenfield **marketing** `style=` is a craft path from that catalog; layout families still come from layout-patterns.md (marketing) or product-register.md (app UI). Briefing runs first unless *invent-all*. Unanswered blanks: no Read, no Lock, no markup ([briefing.md](briefing.md)).

## Example 1: SaaS landing page

**Brief:** "Create a landing page for our new developer tool Uptime that monitors API uptime."

> Reading this as: product landing for technical practitioners (SREs, backend devs), with a sharp / industrial language, leaning toward brand register with minimal color and monospace accents.
>
> Lock: origin=greenfield; name=Uptime; scene=overnight NOC with rack LEDs; style=industrial; theme=dark; color=restrained; layout=offset; motion=fluid; density=regular; stack=project CSS.

## Example 2: Dashboard settings (after briefing answers)

**Brief:** "Build the settings page for our analytics dashboard." Name was blank. Look skipped (`none`). User answered: name from chrome; theme=light; still.

> Reading this as: dense app UI for daily-use analysts, with a utilitarian / calm language, leaning toward product register with a restrained palette and one sans family.
>
> Lock: origin=greenfield; name=from app chrome; scene=fluorescent analyst bay, day shift; style=none; theme=light; color=restrained; layout=contained; motion=still; density=dense; stack=project; Pareto=overview + alert inbox.

## Example 3: Portfolio site (after briefing answers)

**Brief:** "Design a portfolio for a ceramic artist." Name, audience, success, look, theme, behave, and stack were blank, so `AskQuestion` ran one field per turn (Look: Catalog table plus four fitting ids) and the user answered: name=Atelier Sol; collectors; book a studio visit; `you-decide`; light; still; html+css+js.

> Reading this as: portfolio for art-world visitors and collectors, with an organic / tactile language, leaning toward brand register with generous whitespace and a sans display pairing.
>
> Lock: origin=greenfield; name=Atelier Sol; scene=sunlit studio shelf of unglazed ware; style=organic; theme=light; color=committed; layout=wild; motion=still; density=airy; stack=html+css+js; break=one full-bleed kiln photo.

## Example 4: Restaurant homepage (after briefing answers)

**Brief:** "Homepage for a new fine-dining restaurant." Look filled (`fine-dining` maps to `luxury`). Name and stack were blank; the user answered name=Maré and html+css+js.

> Reading this as: marketing surface for reservation-driven diners, with a luxurious / intimate language, leaning toward brand register with a dark scene and high-contrast photography.
>
> Lock: origin=greenfield; name=Maré; scene=candlelit dining room after service; style=luxury; theme=dark; color=drenched; layout=offset; motion=fluid; density=airy; stack=html+css+js; break=container-free menu fold.

Drenched is the Lock exemption from 60-30-10. The scene owns the palette.

## Example 5: Redesign an existing homepage

**Brief:** "The marketing homepage looks generic. Keep the URLs and the navy."

> Reading this as: existing product landing for returning visitors, with a sharper language on the current tokens, leaning toward brand register on the current CSS stack.
>
> Lock: origin=redesign; name=existing wordmark; scene=same product, daylight office; style=none; theme=light; color=committed; layout=offset; motion=fluid; density=regular; stack=project CSS; break=asymmetric split on the current hero photo.

Audit listed before the first visual edit. Navy stays. Slugs stay. Catalog stays closed.

## Example 6: Personal work page (stop)

**Brief:** "Create a unique web page to showcase my work. My background: I have been a software engineer for N years and created software … engineer pipeline …"

Filled: Job, Constraints (keep the named software). Blank: Name, Audience, Success, Use, Look, Theme, Behave, Stack. "Unique" is not invent-all.

Do not write a Design Read or Lock in this turn. Close this file. Open [briefing.md](briefing.md) and ask **Name** with `AskQuestion` ([briefing.md](briefing.md#worked-example)). After every field has an owner, open [after-briefing.md](after-briefing.md).

## Example 7: Polish an existing settings page

**Brief:** "Tighten the settings page. Contrast is weak and the save button has no loading state."

Existing markup, DESIGN.md, and tokens. Origin=`polish`. Look, Name, Stack filled by disk. No Catalog. No new layout family.

> Reading this as: existing settings for daily-use analysts, with the current product language, leaning toward the in-repo design system.
>
> Lock: origin=polish; name=from app chrome; scene=same analyst bay; style=none; theme=light; color=restrained; layout=contained; motion=still; density=dense; stack=project; Pareto=overview + alert inbox.

## When to ask

This file is after answers. Missing briefing fields: close this file and ask the next blank with `AskQuestion` ([briefing.md](briefing.md)). Extra asks after answers only when:

- Brief says "for everyone" and the product is niche.
- Brief describes a dashboard and asks for wow-factor animation on every chrome control.
- Origin is unclear: new UI vs redesign this page from the briefing vs polish what is here.

Skip the briefing form on *invent-all*. Still split files and still write DESIGN.md.

## Done when

- Briefing answers (or invent-all) completed; `name=` is the user's string, `invented`, or disk. Greenfield **marketing** Look is a catalog id, refs, or `you-decide`. App UI Look is skipped (`none`) unless the user named an `id`. Redesign and polish Look is disk; `style=none`. Greenfield `theme=` is `light` / `dark` / `system` from briefing Theme; redesign and polish Theme is disk. Lock `theme=system` at Implement: [color.md](color.md#system-theme).
- Both Read and Lock lines exist before markup. They do not exist in the same turn as unanswered blanks.
- Origin is in the Lock (`greenfield`, `redesign`, or `polish`).
- The sentence names audience and register. "Clean and modern" fails this. Greenfield marketing `you-decide` includes the Pick sentences; `saas` / `enterprise` / `modern-dark` only when the user named that id. App UI does not write Pick.
- App UI and marketing always have a Design Read; isolated components inherit the parent surface or skip.
