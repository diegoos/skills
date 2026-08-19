# Briefing

SKILL.md opens this file after Classify. Score fields here. A score made before this file was open is void.

Open [design-styles.md](design-styles.md) in the same turn only when the current blank is **Look**, origin is greenfield, task type is **marketing**, and Look is blank.

## This turn

Call `AskQuestion` for **exactly one** remaining blank. Then the turn ends.

A numbered list of questions in the chat message fails this file. A Design Read, Lock, scene sentence, concept paragraph, or markup fails this file. Marketing Look may print the Catalog table, then the `AskQuestion` call. App UI never prints that table.

A first-person bio plus "showcase my work" / "unique" is the [Worked example](#worked-example). Ask Name first.

Done for this turn when that one `AskQuestion` call is the user-facing output. The briefing as a whole is done when every field has an owner; then open [after-briefing.md](after-briefing.md). After each answer, if blanks remain, ask the next blank on the next turn.

## Ask

Order of blanks (skip any already filled): **Name**, **Audience**, **Success**, **Use**, **Look**, **Theme**, **Palette**, **Behave**, **Constraints**, **Stack**.

One field per call. At least two options. **Other** is how the user types a custom answer; do not add a duplicate Other option.

Write the prompt in the user's language. English stems below are the template.

Build options from the prompt. Nearby readings that fit the job go in the list. When no nearby reading exists, still call the tool: two working options derived from the job (descriptive nouns, not coined handles), so the picker has choices and Other still takes a typed answer.

| Field           | Prompt stem                                                                   | Options                                                                         |
| --------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **Name**        | I couldn't determine the project name. What name or title do you want to use? | Nearby names or titles from the prompt. If none: two job-derived working titles |
| **Audience**    | What audience do you want to reach with this project?                         | Groups that fit the job (hiring managers, other engineers, clients, …)          |
| **Success**     | What is the one primary action on this page?                                  | Verb + object readings that fit the job (hire, contact, try a skill, …)         |
| **Use**         | How will people use this page?                                                | A scan of minutes, a longer read, `none`                                        |
| **Look**        | Choose a style from the list, type a table item number, or describe one.      | Four Catalog styles that fit the job, plus "I'll specify a different style"     |
| **Theme**       | Which theme should this UI use?                                               | Light, Dark, Both (`system`: two modes + a chrome switch)                       |
| **Palette**     | Which color palette should this UI use?                                       | Neutrals (charcoal + one accent), plus two hues from the job                    |
| **Behave**      | How should this page behave?                                                  | `still`, `fluid`, `cinematic`, `none`                                           |
| **Constraints** | Any constraints I should keep?                                                | Named artifacts already in the prompt, `none`                                   |
| **Stack**       | Which stack should I use?                                                     | HTML+CSS+JS, Next.js, React, Vue, Astro, Svelte, Tailwind, Material UI          |

## invent-all

Skip the form only when the user said **invent-all**, **surprise me**, **pick freely**, or the same idea in those words.

"Unique", "creative", "showcase my work", and a bio are not invent-all.

On invent-all: skip the form. Open [after-briefing.md](after-briefing.md).

Otherwise invent no product, company, page title, persona, handle, or glossary term.

`you-decide` on **Look** is greenfield **marketing** only, and is not invent-all. Ask the other blanks. The style Pick runs after those answers, in [after-briefing.md](after-briefing.md). Do not average the Catalog. App UI invent-all still skips Look (`none`) and does not run Pick.

## Filled vs blank

A field is **filled** when the user named it in those words. Disk fills five slots: DESIGN.md `name` → **Name**, wordmark already in chrome → **Name**, `package.json` / framework config → **Stack**, theme switch / `prefers-color-scheme` / DESIGN.md dual tokens → **Theme**, DESIGN.md surface/accent colors → **Palette**. Git user, folder name, and years-as-handle do not fill Name.

A field is **blank** when it is missing, only implied, or only paraphrased. **Silence is blank.** `none` is a valid *user* answer, not an agent default.

Inference is not an owner. For example, "Software engineer for N years" does not fill Name, Audience, Success, Look, Theme, Palette, Behave, or Stack. "Showcase my work" fills **Job** only; it does not fill Success or Use. A marketing row that says "portfolio" does not fill Audience. "Dashboard" / "CMS" / "admin" does not fill Theme. "Sports" / "CMS" / a guessed accent does not fill Palette.

| Signal                                                                 | Status                                                         |
| ---------------------------------------------------------------------- | -------------------------------------------------------------- |
| First-person bio, role, years                                          | fills **Job** only                                             |
| Named artifacts (skills, products)                                     | copy to keep; not Name                                         |
| "unique" / "creative" / "showcase"                                     | quality bar; not invent-all                                    |
| Catalog `id`, Item number, or refs                                     | fills **Look**                                                 |
| `you-decide` / "you pick the style"                                    | fills **Look** only on marketing; pick after the other answers |
| "professional" / "nível profissional" / "clean" / "modern" / "premium" | quality bar; not Look; not catalog `id=professional`           |
| "light" / "dark" / "dark mode" / "both" / `system`                     | fills **Theme**                                                |
| hex, brand color, "neutrals", or a named family ("navy", "forest")     | fills **Palette**                                              |
| Git user, folder name, or years-as-handle                              | not the wordmark unless they said that word                    |

## Fields

Skip filled fields. Ask remaining blanks one at a time via `AskQuestion`. Ending the briefing while Look, Theme, Palette, Behave, or Stack is still blank (when those apply) fails this file.

| Field           | Why                                                      | Filled when                                   |
| --------------- | -------------------------------------------------------- | --------------------------------------------- |
| **Name**        | Visible wordmark, `<title>`, DESIGN.md `name`            | User string, or invent-all                    |
| **Job**         | One sentence: who does what on this surface              | Concrete task in the prompt only              |
| **Audience**    | Who the UI is for                                        | Named group                                   |
| **Success**     | Primary CTA or done-state                                | One verb + object that would fail a logo-swap |
| **Use**         | Context of use: session length, interruption, stress     | Hours vs minutes, or user said `none`         |
| **Look**        | Craft path: catalog `id`, refs, or `you-decide`          | See [Look](#look)                             |
| **Theme**       | Light, dark, or both                                     | See [Theme](#theme)                           |
| **Palette**     | Surface hue: neutrals vs a named accent family           | See [Palette](#palette)                       |
| **Behave**      | Interactivity, motion, states that matter                | Named motion/states, or user said `none`      |
| **Constraints** | Copy to keep, a11y, regulated, brand assets              | Listed, or user said `none`                   |
| **Stack**       | Only when origin is greenfield and the repo has no stack | User named a stack from the Ask list above    |

Quiet constraints the user already named (public-sector, kids, WCAG) stay filled. Do not re-ask those.

"Build the future", "all-in-one", "Scale without limits", and "transform your workflow" leave **Success** blank. Ask for a verb + object that would fail a logo-swap.

A **complete** prompt already named Audience and Success, Theme when it applies (greenfield app UI and marketing), Palette when it applies, and on marketing also Look (greenfield), or those sit on disk (redesign/polish). App UI Look is skipped (`none`) and does not block complete. Theme blank on greenfield app UI or marketing fails complete. Palette blank when hue has no owner fails complete. Score the rest. Zero remaining blanks: skip the form and open [after-briefing.md](after-briefing.md). Named Job plus a bio is not complete.

Origin `redesign` and `polish`: Name, Look, Theme, Palette, and Stack are disk. Ask remaining blanks only. Polish often has no blanks; skip the form and open [after-briefing.md](after-briefing.md). Leave [design-styles.md](design-styles.md) closed.

**Behave** applies to app UI and marketing. Skip it on an isolated component unless the user asked for interaction.

**Stack** applies when origin is greenfield and the repo has no stack.

## Look

**Look** applies to greenfield marketing and portfolio. Skip it on **app UI** (dashboard, admin, CMS, settings, authenticated tool): treat as filled `none` unless the user named a catalog `id`, refs, or a visual restyle. Skip it on an isolated component unless the user asked for a visual restyle. Skip it on `redesign` and `polish`: disk owns the look. Leave [design-styles.md](design-styles.md) closed.

Filled when the user named a catalog `id` (greenfield), chose one of the four tool options, typed a Catalog Item number, described a look that maps to one id ("Swiss grid", "dark academia"), pasted 1–3 sites or screenshots with one clause of *why* (density, type, occupancy — not pixels), said `you-decide` / `none` on **marketing**, or origin is redesign/polish (disk), or task is app UI and Look was skipped (`none`).

Job, bio, "unique", and quality adjectives ("professional", "nível profissional", "clean", "modern") do not fill Look. A guessed developer-portfolio or SaaS default does not fill Look. `you-decide` on app UI stays `none` and does not run Pick.

When Look is the **current blank** and origin is **greenfield** and task is **marketing**:

1. Load the Catalog in [design-styles.md](design-styles.md).
2. Print **one** markdown table in chat, every Catalog row, columns: Item, Style, Default Theme Mode, Short description. Style is the `id` in Title Case. Default Theme Mode is Mode (`Light` / `Dark`). Short description is Description. Keep the Catalog Item numbers. This table is reference, not the question.
3. Pick **four** `id`s that fit Job (and Audience, Success, Use, Behave when those already have owners). Vary the set: not four median-cluster ids, not the [anti-slop.md](anti-slop.md) category default for this job (developer portfolio is not `terminal` / `cyberpunk` / `web3` / `industrial`). Do not pick an id as the answer.
4. Call `AskQuestion` with **five** options: the four as `Item N — StyleName`, then `I'll specify a different style`. Prompt stem: choose from the list, type a table item number, or describe the look (including `you-decide`). Other is a typed id, item number, refs, or description.

Do not put all Catalog ids in `AskQuestion`. A 30-option picker fails this step. Printing the Catalog table on app UI fails this step.

On greenfield **marketing** `you-decide` or `none`: after the rest of the briefing has owners, [after-briefing.md](after-briefing.md) runs the **Pick**. Do not pick an id in this turn. App UI skipped Look does not run Pick.

## Theme

**Theme** applies to greenfield app UI and greenfield marketing. Skip it on an isolated component. Skip it on `redesign` and `polish`, or when disk already owns Theme.

Filled when the user named `light`, `dark`, `both`, or `system` (or the same idea in the user's language), or disk owns Theme. Job, "dashboard", "CMS", and "admin" leave Theme blank. `none` is invalid: pick Light, Dark, or Both.

When Theme is the **current blank** and it applies: call `AskQuestion` with Light, Dark, and Both. Both maps to Lock `theme=system`. Ship it per [color.md](color.md#system-theme). Other is a typed `light` / `dark` / `system`.

Map the answer onto Lock `theme=` at Declare. Scene owns temperature ([color.md](color.md#scene-sentence-temperature-before-hex)).

## Palette

**Palette** applies to greenfield app UI and greenfield marketing when hue has no owner. Skip it on an isolated component. Skip it on `redesign` and `polish`, or when DESIGN.md already names surface and accent colors.

Filled when the user named hex, a brand color, `neutrals`, or a family ("navy", "forest"), or disk owns Palette. Theme (light/dark) is the mode; it does not fill Palette. Job, "dashboard", "CMS", "sports", and a guessed accent leave Palette blank.

When Palette is the **current blank** and it applies: call `AskQuestion`. Options: Neutrals (charcoal / off-white surfaces + one accent), plus two hues derived from the job. Other is a typed family, hex, or `neutrals`. Neutrals is the product default.

Ship per [color.md](color.md#building-a-palette). A named hue is the accent, not the dark canvas, unless the user asked for a tinted field or Lock `color=drenched`.

## Worked example

Prompt: *Create a unique web page to showcase my work. My background: I have been a software engineer for N years and created and delivered high-quality software, such as `example 1`, `example 2`, and `example 3`.*

| Field       | Status                                        |
| ----------- | --------------------------------------------- |
| Name        | blank                                         |
| Job         | filled (engineer showcasing your work/skills) |
| Audience    | blank                                         |
| Success     | blank                                         |
| Use         | blank                                         |
| Look        | blank                                         |
| Theme       | blank                                         |
| Palette     | blank                                         |
| Behave      | blank                                         |
| Constraints | filled (keep the named skills)                |
| Stack       | blank if the repo has no stack                |

Not invent-all. First remaining blank is **Name**. Call `AskQuestion` with the Name stem. Options: two working titles from the job (descriptive nouns). Other is the user's own name. Stop. Do not list Audience through Stack in chat.

After Name is answered, next turn asks **Audience** the same way, then Success, Use, Look (Catalog table in chat, four fitting ids plus specify), Theme, Palette, Behave, Stack. Then open [after-briefing.md](after-briefing.md). App UI never uses that Look step; skipped Look is `none`.
