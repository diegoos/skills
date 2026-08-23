# Briefing

SKILL.md opens this file after Classify. Score fields here. A score made before this file was open is void.

Leave [design-styles.md](design-styles.md) closed in this window. Catalog and Pick belong to Direction ([dispatch.md](dispatch.md#direction)). Printing the Catalog table here fails this file.

## This turn

Call `AskQuestion` for **exactly one** remaining blank. Then the turn ends.

A numbered list of questions in the chat message fails this file. A Design Read, Lock, scene sentence, concept paragraph, or markup fails this file.

A first-person bio plus "showcase my work" / "unique" is the [Worked example](#worked-example). Ask Name first.

Done for this turn when that one `AskQuestion` call is the user-facing output. The briefing as a whole is done when every field has an owner; then open [after-briefing.md](after-briefing.md). After each answer, if blanks remain, ask the next blank on the next turn.

## Ask

Order of blanks (skip any already filled). Origin `greenfield`: **Name**, **Audience**, **Success**, **Use**, **Scene**, **Theme**, **Palette**, **Stack**. Do not ask **Look** ([Look](#look)). Do not ask **Behave** or **Constraints** unless the prompt already named motion, states, artifacts, or restrictions ([Behave and Constraints](#behave-and-constraints)). Origin `redesign`: **Aim**, **Keep**, **Scope**, then **Audience** (only if it applies), **Success** (if blank), **Use** if still blank. Skip Name, Scene, Look, Theme, Palette, Stack on redesign. Skip Behave and Constraints on redesign unless Aim named them. Origin `polish`: skip this form unless the goal is mute; then **Focus** only ([Polish](#polish)).

One field per call. At least two options. **Other** is how the user types a custom answer; do not add a duplicate Other option.

Write the prompt in the user's language. English stems below are the template.

Build options from the prompt. Nearby readings that fit the job go in the list. When no nearby reading exists, still call the tool: two working options derived from the job (descriptive nouns, not coined handles), so the picker has choices and Other still takes a typed answer.

| Field           | Prompt stem                                                                   | Options                                                                         |
| --------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **Name**        | I couldn't determine the project name. What name or title do you want to use? | Nearby names or titles from the prompt. If none: two job-derived working titles |
| **Audience**    | What audience do you want to reach with this project?                         | Groups that fit the job (hiring managers, other engineers, clients, …)          |
| **Success**     | What is the one primary action on this page?                                  | Verb + object readings that fit the job (hire, contact, try a skill, …)         |
| **Use**         | How will people use this page?                                                | A scan of minutes, a longer read, `none`                                        |
| **Scene**       | Name first-viewport occupancy, a place, or let the brief decide.              | You decide first, then two Job readings with different topology                 |
| **Theme**       | Which theme should this UI use?                                               | Light, Dark, Both (`system`: two modes + a chrome switch)                       |
| **Palette**     | Which color palette should this UI use?                                       | Neutrals (charcoal + one accent), plus two hues from the job                    |
| **Stack**       | Which stack should I use?                                                     | HTML+CSS+JS, Next.js, React, Vue, Astro, Svelte, Tailwind, Material UI          |
| **Aim**         | What should be true after this redesign that is not true now?                 | Four readings from a page glance ([Redesign](#redesign))                        |
| **Keep**        | What must still feel like this product?                                       | Wordmark + nav; routes; copy voice; tokens; all of these                        |
| **Scope**       | How far may composition change?                                               | First viewport only; this page; this flow (linked pages, same chrome)           |
| **Focus**       | What should feel better first?                                                | Hierarchy and scan; spacing rhythm; inconsistent color; states; a11y            |

## invent-all

Skip the form only when the user said **invent-all**, **surprise me**, **pick freely**, or the same idea in those words.

"Unique", "creative", "showcase my work", and a bio are not invent-all.

On invent-all: skip the form. Open [after-briefing.md](after-briefing.md). Invent-all on redesign does not invent a brand or catalog id — the Briefing card in [after-briefing.md](after-briefing.md) fills Aim/Keep/Scope defaults.

Otherwise invent no product, company, page title, persona, handle, or glossary term.

Greenfield **marketing** Look with no named `id`, Item number, or craft refs is `you-decide` (silence included). Do not ask. Direction runs Pick after Frame ([dispatch.md](dispatch.md#direction)). Do not average the Catalog. App UI invent-all still skips Look (`none`) and does not run Pick.

`you-decide` on **Scene** is greenfield **marketing** only, and is not invent-all. Ask the other blanks. [composition.md](composition.md) writes occupancy from *objects* and *kinship* after those answers. Do not invent occupancy in this turn. App UI invent-all still skips Scene (`none`).

## Filled vs blank

A field is **filled** when the user named it in those words. Disk fills five slots: DESIGN.md `name` → **Name**, wordmark already in chrome → **Name**, `package.json` / framework config → **Stack**, theme switch / `prefers-color-scheme` / DESIGN.md dual tokens → **Theme**, DESIGN.md surface/accent colors → **Palette**. Git user, folder name, and years-as-handle do not fill Name.

A field is **blank** when it is missing, only implied, or only paraphrased. **Silence is blank**, except greenfield **marketing** Look: unnamed Look is owner `you-decide`, not a blank ([Look](#look)); and **Behave** / **Constraints**: unnamed is owner `none`, not a blank ([Behave and Constraints](#behave-and-constraints)). `none` is a valid *user* answer. On Behave and Constraints it is also the agent default when the prompt did not name those facts.

Inference is not an owner. For example, "Software engineer for N years" does not fill Name, Audience, Success, Scene, Theme, Palette, or Stack. It does not fill a named Look `id`. "Showcase my work" fills **Job** only; it does not fill Success, Use, or Scene. A marketing row that says "portfolio" does not fill Audience. "Dashboard" / "CMS" / "admin" does not fill Theme. "Sports" / "CMS" / a guessed accent does not fill Palette. A guessed category place does not fill Scene.

| Signal                                                                 | Status                                                         |
| ---------------------------------------------------------------------- | -------------------------------------------------------------- |
| First-person bio, role, years                                          | fills **Job** only                                             |
| Named artifacts (skills, products)                                     | copy to keep; not Name                                         |
| "unique" / "creative" / "showcase"                                     | quality bar; not invent-all; not Scene                         |
| Place, remembered page, or occupancy sentence                          | fills **Scene**                                                |
| URL or screenshot + occupancy *why* (span, split, full-bleed)          | fills **Scene**; not Look                                      |
| URL or screenshot + craft *why* (density, type, material)              | fills **Look**; not Scene                                      |
| Catalog `id`, Item number, or craft refs                               | fills **Look**                                                 |
| Greenfield marketing silence on Look                                   | owner `you-decide`; Pick after Frame; not a briefing blank     |
| `you-decide` / "You decide from the brief" on occupancy                | fills **Scene** on marketing; write sentence in composition    |
| `you-decide` / "you pick the style"                                    | fills **Look** only on marketing; Pick after Frame             |
| "professional" / "nível profissional" / "clean" / "modern" / "premium" | quality bar; not Look; not Scene; not `id=professional`        |
| "light" / "dark" / "dark mode" / "both" / `system`                     | fills **Theme**                                                |
| hex, brand color, "neutrals", or a named family ("navy", "forest")     | fills **Palette**                                              |
| Git user, folder name, or years-as-handle                              | not the wordmark unless they said that word                    |
| Silence on Behave/Constraints (unnamed)                                | owner `none`; not a briefing blank                             |

## Fields

Skip filled fields. Ask remaining blanks one at a time via `AskQuestion`. Ending the briefing while Scene, Theme, Palette, Use, or Stack is still blank (when those apply) fails this file. Unnamed greenfield marketing Look is not a remaining blank. Unnamed Behave and Constraints are owner `none`, not remaining blanks. Origin `redesign`: Aim, Keep, or Scope still blank fails this file. Origin `polish` with a mute goal: Focus still blank fails this file.

| Field           | Why                                                      | Filled when                                   |
| --------------- | -------------------------------------------------------- | --------------------------------------------- |
| **Name**        | Visible wordmark, `<title>`, DESIGN.md `name`            | User string, or invent-all                    |
| **Job**         | One sentence: who does what on this surface              | Concrete task in the prompt only              |
| **Audience**    | Who the UI is for                                        | Named group                                   |
| **Success**     | Primary CTA or done-state                                | Marketing logo-swap; app UI persist/queue     |
| **Use**         | Context of use: session length, interruption, stress     | Hours vs minutes, or user said `none`         |
| **Scene**       | First-viewport occupancy or `you-decide`                 | See [Scene](#scene)                           |
| **Look**        | Craft path: catalog `id`, refs, or `you-decide`          | See [Look](#look)                             |
| **Theme**       | Light, dark, or both                                     | See [Theme](#theme)                           |
| **Palette**     | Surface hue: neutrals vs a named accent family           | See [Palette](#palette)                       |
| **Behave**      | Interactivity, motion, states that matter                | Silence, named motion, or `none`              |
| **Constraints** | Copy to keep, a11y, regulated, brand assets              | Listed, artifacts, silence, or `none`         |
| **Stack**       | Only when origin is greenfield and the repo has no stack | User named a stack from the Ask list above    |
| **Aim**         | Redesign outcome                                         | See [Redesign](#redesign)                     |
| **Keep**        | What stays this product                                  | See [Redesign](#redesign)                     |
| **Scope**       | How far composition may change                           | See [Redesign](#redesign)                     |
| **Focus**       | Polish first problem when the goal is mute               | See [Polish](#polish)                         |

Quiet constraints the user already named (public-sector, kids, WCAG) stay filled. Do not re-ask those.

"Build the future", "all-in-one", "Scale without limits", and "transform your workflow" leave **Success** blank. Marketing: ask for a verb + object that would fail a logo-swap. App UI: ask for the persist or queue verb + object.

A **complete** prompt already named Audience, Success, and Use, Theme when it applies (greenfield app UI and marketing), Palette when it applies, and on marketing also Scene (greenfield), or those sit on disk (redesign/polish). Look is not required in the prompt: unnamed greenfield marketing Look is `you-decide`. Unnamed Behave and Constraints are `none` and do not block complete. Redesign also needs Aim, Keep, and Scope (or the prompt named them). App UI Scene and Look are skipped (`none`) and do not block complete. Theme blank on greenfield app UI or marketing fails complete. Palette blank when hue has no owner fails complete. Scene blank on greenfield marketing fails complete. Use blank when it applies fails complete. Score the rest. Zero remaining blanks: skip the form and open [after-briefing.md](after-briefing.md). Named Job plus a bio is not complete.

Origin `redesign`: Name, Scene, Look, Theme, Palette, and Stack are disk. Ask Aim, Keep, Scope, then remaining blanks only. Leave [design-styles.md](design-styles.md) closed. Do not ask Scene.

Origin `polish`: Name, Scene, Look, Theme, Palette, and Stack are disk. Skip the form when the user named what to tighten. If they only said "improve this" / "melhora isso" with no problem named, ask **Focus** once, then open [after-briefing.md](after-briefing.md). Leave [design-styles.md](design-styles.md) closed. Do not ask Scene.

**Use** applies to app UI and marketing. Skip it on an isolated component. Hours of work → Lock `density=dense`. A scan of minutes → `density=airy`. User said `none` → `density=regular`. Silence on Use is still blank: ask it.

**Behave** applies to app UI and marketing. Skip it on an isolated component unless the user asked for interaction.

**Stack** applies when origin is greenfield and the repo has no stack.

## Behave and Constraints

Do not ask. Silence is owner `none`, not a blank.

**Behave** is filled when the user named motion or states (`still`, `fluid`, `cinematic`, hover, scroll) or said `none`. Unnamed Behave is `none`. Lock maps `none` / `still` → `motion=still`; hover/scroll → `fluid`; `cinematic` → `cinematic`. Do not invent cinematic.

**Constraints** is filled when the prompt listed artifacts, a11y, regulated copy, or brand assets to keep, or the user said `none`. Named artifacts in the prompt (skills, products, wordmark files) copy into Constraints without asking. Unnamed Constraints with no artifacts in the prompt is `none`. Quiet constraints the user already named (public-sector, kids, WCAG) stay filled.

Asking Behave or Constraints when the prompt did not name those facts fails this file. Re-asking artifacts already copied into Constraints fails this file.

## Scene

**Scene** applies to greenfield marketing and portfolio. Skip it on **app UI** (dashboard, admin, CMS, settings, authenticated tool): treat as filled `none`. Skip it on an isolated component. Skip it on `redesign` and `polish`: Aim/Keep (redesign) or disk (polish) own occupancy. Do not ask.

Filled when the user named a place, a remembered page, or occupancy in one sentence ("the work fills the screen; the name is small", "newspaper front page", "one full-bleed kiln photo"), pasted a URL or screenshot with one clause of *why* that names occupancy (column span, split, full-bleed — not pixels, not type, not material), said `you-decide` / `none` / "You decide from the brief" on **marketing**, or origin is redesign/polish (skip), or task is app UI and Scene was skipped (`none`).

Job, bio, "unique", and quality adjectives ("professional", "nível profissional", "clean", "modern", "editorial" as a vibe with no occupancy) do not fill Scene. A guessed category place ("desk at night" for a developer portfolio) does not fill Scene. A craft-only ref (density, type, material) fills Look, not Scene.

When Scene is the **current blank** and origin is **greenfield** and task is **marketing**:

Call `AskQuestion` with **three** options: `You decide from the brief` first, then two occupancy readings derived from Job. The two readings differ in *topology* (stack vs split vs full-bleed), not in two column ratios of the same join. Place or first-viewport mass — not catalog ids, not quality adjectives. Prompt stem: name a place, a page you remember, or how the first viewport is occupied; or let the agent decide from the brief. Other is a typed occupancy sentence or a URL with an occupancy *why*.

Do not invent occupancy in this turn. On `you-decide` / `none`: after the rest of the briefing has owners, [composition.md](composition.md) writes occupancy from *objects* and *kinship*. Invent-all skipped the form: same. App UI skipped Scene does not run that write as a composition input.

## Look

**Look** applies to greenfield marketing and portfolio. Skip it on **app UI** (dashboard, admin, CMS, settings, authenticated tool): treat as filled `none` unless the user named a catalog `id`, refs, or a visual restyle. Skip it on an isolated component unless the user asked for a visual restyle. Skip it on `redesign` and `polish`: disk owns the look. Leave [design-styles.md](design-styles.md) closed in this window.

Do not ask. Printing the Catalog table in this window fails this file. Direction opens the Catalog for Pick ([design-styles.md](design-styles.md#pick)). To lock a look, the user names an `id` or Catalog Item number in the prompt ([design-styles.md](design-styles.md#catalog)).

Filled when the user named a catalog `id` (greenfield), typed a Catalog Item number, described a look that maps to one id ("Swiss grid", "dark academia"), pasted 1–3 sites or screenshots with one clause of *why* (density, type, material — not pixels, not occupancy), said `you-decide` / `none` on **marketing**, origin is redesign/polish (disk), task is app UI and Look was skipped (`none`), **or** origin is greenfield marketing and Look was unnamed (owner `you-decide`).

Job, bio, "unique", and quality adjectives ("professional", "nível profissional", "clean", "modern") do not fill a named Look `id`. A guessed developer-portfolio or SaaS default does not fill Look. `you-decide` on app UI stays `none` and does not run Pick. An occupancy *why* on a pasted ref fills Scene, not Look.

On greenfield **marketing** `you-decide` (including silence) or `none`: Direction runs the **Pick** after Frame ([dispatch.md](dispatch.md#direction)). Do not pick an id in this file. App UI skipped Look does not run Pick.

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

## Redesign

Applies when Classify named `origin=redesign`. Do not ask Scene, Look, Theme, Palette, or Stack. Do not print the Catalog.

**Aim** is the expected outcome. Without it, Direction fails. Filled when the user named what should be true after the redesign that is not true now. Silence is blank.

When Aim is the current blank: glance at the existing page (not a tour). Call `AskQuestion` with four readings that fit the prompt and that glance:

- The primary action fails
- The first fold does not state the job
- IA hides what the visitor or operator came to do
- The visual no longer matches this product (brand tokens stay)

Other is the user's sentence. Map onto Lock `aim=`.

**Keep** is preservation intent. Filled when the user named what must still feel like this product, or said `all of these`. When it is the current blank: wordmark + nav; routes and analytics; copy voice; accent and tokens; all of these. Other names the sacred piece. Do not re-ask the same facts as Constraints. Map onto Lock `keep=`. Preservation rules: [redesign.md](redesign.md#preservation).

**Scope** is how far composition may change. Filled when the user named first viewport, this page, or this flow. When it is the current blank: First viewport only; this page (sections); this flow (linked pages, same chrome). Suggested default in the option labels: this page. Rewriting the product is not an option until they ask. Map onto Lock `scope=` (`first-viewport` / `page` / `flow`). Levers 6–8 only inside that scope ([redesign.md](redesign.md#levers-stop-when-the-brief-is-satisfied)).

**Audience** after Scope: ask only if Aim names a new public or the prompt does not name who uses the surface now. Disk + Job otherwise fill it.

**Success** if still blank. Prompt stem: "After this redesign, which one action should someone complete that they fail today?" Options: verb + object readings from the page and Aim. Marketing: that sentence must fail a logo-swap after recomposition. App UI: a persist or queue done-state, no logo-swap.

**Use** if still blank. Prompt stem: "How will people use this page after the redesign?" Options: a scan of minutes; a longer read; `none`. Map onto Lock `density=` (minutes → airy; hours → dense; `none` → regular).

Do not ask **Behave** or **Constraints** unless Aim named motion, states, artifacts, or restrictions. Unnamed Behave and Constraints are owner `none`. Constraints must not repeat Keep. Named artifacts on disk stay in Keep.

1–3 pasted reference sites with a *why* (density, type, occupancy) fill flavor for Direction and, when the *why* names occupancy, the [composition.md](composition.md) *frame*. They do not fill Look or Scene as catalog fields and do not open the Catalog.

Done when Aim, Keep, and Scope have owners and every remaining applicable blank has an owner. Then open [after-briefing.md](after-briefing.md). Scan and audit run in Direction ([redesign.md](redesign.md)).

## Polish

Applies when Classify named `origin=polish`. Skip the form when the user already named the problem (spacing, contrast, states, tighten, a11y).

When they only said "improve this" / "melhora isso" / "make it better" with no problem: **Focus** is blank. Call `AskQuestion` once: hierarchy and scan; spacing rhythm; inconsistent color; states (hover, focus, loading); a11y. Other is their sentence. Then open [after-briefing.md](after-briefing.md). The [craft audit](redesign.md#craft-audit) is Direction. Do not start a second briefing.

If the user names an IA problem (home is a chart gallery, wrong first fold, new job), reclassify origin to `redesign` and ask Aim.

## Worked example

Prompt: *Create a unique web page to showcase my work. My background: I have been a software engineer for N years and created and delivered high-quality software, such as `example 1`, `example 2`, and `example 3`.*

| Field       | Status                                        |
| ----------- | --------------------------------------------- |
| Name        | blank                                         |
| Job         | filled (engineer showcasing your work/skills) |
| Audience    | blank                                         |
| Success     | blank                                         |
| Use         | blank                                         |
| Scene       | blank                                         |
| Look        | `you-decide` (unnamed; Pick after Frame)      |
| Theme       | blank                                         |
| Palette     | blank                                         |
| Behave      | `none` (unnamed; do not ask)                  |
| Constraints | filled (keep the named skills)                |
| Stack       | blank if the repo has no stack                |

Not invent-all. First remaining blank is **Name**. Call `AskQuestion` with the Name stem. Options: two working titles from the job (descriptive nouns). Other is the user's own name. Stop. Do not list Audience through Stack in chat.

After Name is answered, next turn asks **Audience** the same way, then Success, Use, Scene (`You decide from the brief` plus two occupancy readings), Theme, Palette, Stack. Do not ask Look, Behave, or Constraints. Then open [after-briefing.md](after-briefing.md). App UI never uses Scene or Look; skipped Scene and Look are `none`.
