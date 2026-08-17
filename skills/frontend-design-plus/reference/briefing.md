# Briefing

Load on every app UI and marketing run, and on any greenfield component that needs a product name.

A _briefing_ is one batch of _blanks_, then **stop**. Fields the user already named stay out of the form.

## invent-all

Skip the form only when the user said **invent-all**, **surprise me**, **pick freely**, or the same idea in those words.

"Unique", "creative", "showcase my work", and a bio are not invent-all.

On invent-all: skip the form. Still split files ([file-architecture.md](file-architecture.md)). Still write or follow DESIGN.md ([design-md.md](design-md.md)). Still run the _crit_ ([crit.md](crit.md)). Name from the job as a descriptive noun (`Invoice desk`, `API uptime`), never a coined startup or handle (`Nexus`, `Cloudly`, `swe-13`). Lock `name=invented`.

Otherwise invent no product, company, page title, persona, handle, or glossary term.

## Filled vs blank

A field is **filled** when the user named it in those words, or the repo already holds it (wordmark in chrome, `package.json` stack, DESIGN.md `name`).

A field is **blank** when it is missing, only implied, or only paraphrased. **Silence is blank.** `none` is a valid _user_ answer, not an agent default.

Inference is not an owner. "Software engineer for 13 years" does not fill Name, Audience, Success, Look, or Stack.

| Signal                                    | Status                                      |
| ----------------------------------------- | ------------------------------------------- |
| First-person bio, role, years             | fills **Job** only                          |
| Named artifacts (skills, products)        | copy to keep; not Name                      |
| "unique" / "creative" / "showcase"        | quality bar; not invent-all                 |
| Git user, folder name, or years-as-handle | not the wordmark unless they said that word |

## Fields

Ask every blank. One batch. Prefer the harness question tool; otherwise one short numbered list. Then **end the turn**. Do not write DESIGN.md, the Lock, or markup in the same turn as unanswered blanks.

| Field           | Why                                                      | Filled when                                      |
| --------------- | -------------------------------------------------------- | ------------------------------------------------ |
| **Name**        | Visible wordmark, `<title>`, DESIGN.md `name`            | User string, or invent-all                       |
| **Job**         | One sentence: who does what on this surface              | Concrete task in the prompt                      |
| **Audience**    | Who the UI is for                                        | Named group                                      |
| **Success**     | Primary CTA or done-state                                | One verb + object                                |
| **Use**         | Context of use: session length, interruption, stress     | Hours vs minutes, or user said `none`            |
| **Look**        | Marketing/portfolio: sites, screenshots, metaphor        | Listed, or user said `none`                      |
| **Constraints** | Copy to keep, a11y, regulated, brand assets              | Listed, or user said `none`                      |
| **Stack**       | Only when origin is greenfield and the repo has no stack | See [file-architecture.md](file-architecture.md) |

Quiet constraints the user already named (public-sector, kids, WCAG) override Lock bands. Do not re-ask those.

**Look** applies to marketing and portfolio. Skip it on app UI unless the user asked for a visual restyle. On user-said `none`, pick a direction that still passes [anti-slop.md](anti-slop.md) (not the category default).

## Worked example

Prompt: _Create a unique web page to showcase my work. My background: I have been a software engineer for N years and created and delivered high-quality software, such as `example 1`, `example 2`, and `example 3`._

| Field       | Status                                       |
| ----------- | -------------------------------------------- |
| Name        | blank                                        |
| Job         | filled (engineer showcasing you work/skills) |
| Audience    | blank                                        |
| Success     | blank                                        |
| Use         | blank                                        |
| Look        | blank                                        |
| Constraints | filled (keep the named skills)               |
| Stack       | blank if the repo has no stack               |

Not invent-all. Post the batch. Stop. Do not ship a coined name or a dark git-diff hero in this turn.

Batch for that prompt (adapt wording; keep these blanks):

1. **Name.** Wordmark / page title (your name, a studio name, or say invent-all)
2. **Audience.** Who is this for (hiring managers, other engineers, clients, …)
3. **Success.** The one primary action (hire, contact, try a skill, …)
4. **Use.** A hiring scan of minutes, a longer read, or none
5. **Look.** Sites, screenshots, a metaphor to commit to, or none (I pick a direction after)
6. **Stack.** Simple HTML+CSS+JS, Next.js, React, Vue, Astro, Svelte, Tailwind, Material UI, or other

## After the answers

Write the Design Read + Lock. Put `name=<user name>` in the Lock. Copy the name into DESIGN.md front matter. Use that name in the wordmark and document title. Map **Use** onto Lock `density=` (hours of expert work → `dense`; minutes per month → `airy`).

Done when every applicable field has an owner that is a quoted user string, disk evidence, or invent-all, and no unanswered blank shares a turn with DESIGN.md or markup.
