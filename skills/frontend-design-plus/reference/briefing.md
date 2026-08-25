# Briefing

SKILL.md opens this file after Classify when origin is not `polish`. Origin `polish`: close this file and open [polish.md](polish.md). Score fields here. A score made before this file was open is void.

When scoring Job, Audience, or Constraints, open [product-context.md](product-context.md) once if the target repo may hold `PRODUCT.md`, an `AGENTS.md` UX block, or DESIGN.md Overview. Quote those owners or mark evidence `absent`. Do not open that file at Classify.

Leave [design-styles.md](design-styles.md) closed in this window. Open [catalog.md](catalog.md) only on the [Style pick](#look) branch after the user said yes. Do not open [composition.md](composition.md) to write the A/B cards. Direction does not match catalog **When** clauses to invent an id.

## This turn

Pick the branch, then stop when that branch's done criterion holds.

| Branch | When | This turn |
| --- | --- | --- |
| invent-all | user said **invent-all**, **surprise me**, **pick freely**, or the same idea | Open [product-context.md](product-context.md) once. Skip the form. Open [after-briefing.md](after-briefing.md). |
| isolated component | Classify named component | Skip the form and [product-context.md](product-context.md). Open [after-briefing.md](after-briefing.md#isolated-component). |
| polish | origin `polish` | Close this file. Open [polish.md](polish.md). |
| redesign | origin `redesign` | Open [product-context.md](product-context.md) once. Ask **Aim**, **Keep**, **Scope** ([Redesign](#redesign)). |
| empty Job | greenfield, prompt named no concrete task | Open [product-context.md](product-context.md) once. If Job is still blank, ask Job only and end the turn. If Job filled from disk: marketing continues Character then A/B this file; app UI infers remaining owners and opens [after-briefing.md](after-briefing.md). |
| marketing loose | greenfield **marketing**, Job named, occupancy not owned | Infer [Character](#character). Ask **one** [Directions](#directions) question. End the turn. |
| style offer | greenfield **marketing**, occupancy owned, Look unnamed, Style not yet answered | Ask **Style** yes/no ([Look](#look)). End the turn. |
| style pick | user said yes to Style | Open [catalog.md](catalog.md). Print that table. Ask one id or Item ([Look](#look)). End the turn. |
| app UI | greenfield **app UI**, Job named | Infer owners ([Filled vs blank](#filled-vs-blank)). Skip A/B, Scene, Look. Open [after-briefing.md](after-briefing.md). |
| complete | every applicable owner already exists | Open [product-context.md](product-context.md) once if it was not opened this run. Skip the form. Open [after-briefing.md](after-briefing.md). |

A numbered list of questions in the chat message fails this file. Markup, Design Read, Lock, or an eight-field dump fails this file.

Unnamed Behave and Constraints are `none`. Do not ask those. Do not ask Name, Audience, Use, Scene, Theme, Palette, or Stack on marketing loose or app UI greenfield. Unnamed greenfield marketing Look is not `you-decide` until [Look](#look) is answered (no → `you-decide`; yes → catalog id or Item).

Done for this turn when the selected branch's question contract is the user-facing output, or the form was skipped. The briefing as a whole is done when every applicable field has an owner (inferred `character=` counts); then open [after-briefing.md](after-briefing.md).

## Character

Greenfield **marketing** with a named Job. App UI, polish, and redesign skip this section (`character=none`).

Infer four axes from the Job. Write them before the A/B call. Inference **is** the owner here. Do not ask Theme or Palette to learn the character.

```txt
character=risk=<trust|impact>; time=<document|scan|demo>; enter=<domain noun from the prompt>; spectacle=<low|mid|high>
first-character-costume=<the first category outfit this Job would wear>
```

| Axis | What the agent answers |
| --- | --- |
| **risk** | Must the visitor believe before they act (`trust`), or must the product land as a hit (`impact`)? |
| **time** | Document (slow read), scan (minutes), or demo (prove the artifact). Maps Lock `density=`: document → regular or dense; scan → airy; demo → regular. |
| **enter** | The ofício noun already in the prompt (parecer, case, artifact, queue). Not `hero`, `card`, or a second noun invented to look rich. |
| **spectacle** | `low` for regulated/trust; `mid` for a product; `high` for a campaign. |

`first-character-costume=` is the first outfit the domain suggests. Record it. It must not vest Frame, Pick, or CSS. The axis stays; the outfit leaves. Known scaffolds (this list is the owner):

- navy + serif + columns + justice photo (firm / consultancy)
- indigo + three feature cards (SaaS landing)
- mesh HUD / neon phosphor (tech / cyber)
- charcoal + coral + fake terminal + years-as-handle (developer portfolio)

QA and Implement say “veste o costume” and point here. Do not recopy the four.

Name: user string, disk wordmark, or a descriptive working title from the Job (`Litigation desk`). Not a coined handle. Audience: the public the Job already implies. Stack: `package.json` or `html+css+js`. Theme and Palette: disk or a user-named value; otherwise Direction fills craft after Frame from the object, not from the costume (no navy-for-law, no indigo-for-SaaS, no Neutrals-as-fear-default). Scene occupancy is [Directions](#directions) or a named occupancy sentence, not this section.

"professional" / "clean" / "modern" / "premium" is a quality bar. It does not fill Look, Scene, or `id=professional`.

Done when `character=` and `first-character-costume=` exist and enter is a prompt noun or Success's object.

## Directions

Greenfield **marketing** after Character. One structured question. Two options plus Other. Other is a typed occupancy sentence or a URL with an occupancy *why*.

Each option is one line: character reading + `join` token + enter object + Success verb+object.

```txt
A: <character line>; join=<stack|split|full-bleed|overlap>; enter=<object>; success=<verb + object>
B: <character line>; join=<token ≠ A>; enter=<object>; success=<verb + object>
```

Rules:

- Distinct `join` tokens.
- Neither option is `first-character-costume=` ([Character](#character)).
- Enter is a Job noun or Success's object. Do not invent a second domain noun to fill the card.
- Both options are buildable. A strawman fails this file.
- No catalog `id`, no palette, no "You decide from the brief".
- If the prompt already named Success, both cards share that verb. If Success is a slogan ("engage", "pop", "modern"), each card supplies a concrete verb+object; the pick owns Success.

Prompt stem (user's language): two ways this first viewport can work; pick the closer one.

The pick fills **Direction** (`direction=A|B`), **Success**, and Scene occupancy for composition. Look stays blank until [Look](#look).

invent-all skips this question. Direction then writes one Sketch. Do not open [composition.md](composition.md) from this file.

User already named occupancy (place, remembered page, or join *why*): skip A/B; that sentence owns Scene; Direction still infers `character=` and refuses the costume. Next turn is Style offer unless Look already has an id.

Done when the structured call is the user-facing output, or Scene already has an occupancy owner. After the pick, stay on this file for Style if Look is still unnamed. Do not open [after-briefing.md](after-briefing.md) until Look has an owner.

## invent-all

Skip the form only when the user said **invent-all**, **surprise me**, **pick freely**, or the same idea in those words.

"Unique", "creative", "showcase my work", and a bio are not invent-all.

On invent-all: open [product-context.md](product-context.md) once, then skip the form. Infer `character=` from the Job if one exists. Open [after-briefing.md](after-briefing.md). Invent-all on redesign does not invent a brand or catalog id — the Briefing card fills Aim/Keep/Scope defaults.

Otherwise invent no product, company, page title, persona, handle, or glossary term.

invent-all on greenfield marketing sets Look `you-decide` and skips Style. Direction locks `style=none` unless the prompt already named an `id`. App UI invent-all skips Look (`none`).

## Filled vs blank

A field is **filled** when the user named it in those words, disk owns it, or this file named an inferred owner (`character=`, working title, implied Audience, density from `time=`, A/B Success, Style **no** → Look `you-decide`).

Disk fills: DESIGN.md `name` → **Name**, wordmark in chrome → **Name**, `package.json` / framework config → **Stack**, theme switch / `prefers-color-scheme` / DESIGN.md dual tokens → **Theme**, DESIGN.md surface/accent colors → **Palette**. Git user, folder name, and years-as-handle do not fill Name.

Inference is not an owner for brand, regulated copy, metrics, or a second Inventory noun. Inference **is** an owner for `character=`, density, working title, implied Audience, and Theme/Palette *absence* (Direction crafts; do not ask).

| Signal | Status |
| --- | --- |
| First-person bio, role, years | fills **Job** only |
| Named artifacts (skills, products) | copy to keep; not Name |
| "unique" / "creative" / "showcase" | quality bar; not invent-all; not Scene |
| Place, remembered page, or occupancy sentence | fills **Scene**; skip A/B; then Style offer |
| URL or screenshot + occupancy *why* (span, split, full-bleed) | fills **Scene**; skip A/B; then Style offer |
| URL or screenshot + craft *why* (density, type, material) | fills **Look** |
| Catalog `id`, Item number, or craft refs | fills **Look** |
| Greenfield marketing silence on Look | blank; next question is Style offer after occupancy exists |
| Style offer **no** / **none** | fills **Look** `you-decide` |
| Style offer **yes** then an `id` or Item | fills **Look** with that catalog id |
| Named Job on greenfield marketing | infer `character=`; ask A/B unless Scene already owns occupancy |
| A/B pick | fills **Direction**, **Success**, Scene occupancy; Look still blank until Style |
| "professional" / "clean" / "modern" / "premium" | quality bar; not Look; not `id=professional` |
| "light" / "dark" / "both" / `system` | fills **Theme** (do not ask; user or disk only) |
| hex, brand color, or a named family | fills **Palette** (do not ask; user or disk only) |
| Silence on Behave/Constraints | owner `none` |

A **complete** prompt already named Job and, on marketing, occupancy (sentence or A/B pick) **and** Look (named `id` / Item / craft refs, Style **no** → `you-decide`, or invent-all `you-decide`). Behave and Constraints do not block complete. Theme and Palette do not block complete. Redesign needs Aim, Keep, and Scope. App UI skips Scene, Look, and A/B. Style unanswered on greenfield marketing is not complete.

## Fields

| Field | Why | Filled when |
| --- | --- | --- |
| **Job** | Who does what | Concrete task in the prompt, the Job question, or [product-context.md](product-context.md) |
| **Character** | Layout behavior for this domain | Inferred on marketing greenfield ([Character](#character)); else `none` |
| **Direction** | A/B winner | Pick, named occupancy, invent-all (`none`), app UI `none` |
| **Name** | Wordmark, `<title>`, DESIGN.md `name` | User string, disk, working title from Job, or invent-all |
| **Audience** | Who the UI is for | Named group, implied by Job, or product-context `users=` |
| **Success** | Primary CTA | Verb+object in the prompt, or the A/B pick |
| **Use** | Density | Inferred from `time=`; user hours/minutes/`none` if they named it |
| **Scene** | First-viewport occupancy | Named occupancy or A/B pick; invent-all `you-decide` |
| **Look** | Craft path | See [Look](#look) |
| **Theme** | Light, dark, or both | User or disk; else Direction after Frame |
| **Palette** | Surface hue | User or disk; else Direction after Frame from the object |
| **Behave** | Motion, states | Silence, named motion, or `none` |
| **Constraints** | Copy to keep, a11y, assets | Listed, artifacts, product-context `commitments=`, silence, or `none` |
| **Stack** | Greenfield with no stack on disk | Disk, or default `html+css+js` |
| **Aim** / **Keep** / **Scope** | Redesign | See [Redesign](#redesign) |
| **Focus** | Mute polish | [polish.md](polish.md#focus) |

Quiet constraints the user already named (public-sector, kids, WCAG) stay filled.

"Build the future", "all-in-one", "Scale without limits", and "transform your workflow" leave **Success** blank until the A/B cards name a verb+object.

## Behave and Constraints

Do not ask. Silence is owner `none`, not a blank.

**Behave** is filled when the user named motion or states (`still`, `fluid`, `cinematic`, hover, scroll) or said `none`. Unnamed Behave is `none`. Lock maps `none` / `still` → `motion=still`; hover/scroll → `fluid`; `cinematic` → `cinematic`. Do not invent cinematic.

**Constraints** is filled when the prompt listed artifacts, a11y, regulated copy, or brand assets to keep, or the user said `none`. Named artifacts copy into Constraints without asking. Unnamed Constraints with no artifacts is `none`.

Asking Behave or Constraints when the prompt did not name those facts fails this file.

## Look

**Look** is the briefing name for Lock `style=` / a catalog `id`. One concept. Applies to greenfield marketing and portfolio. Skip Style on **app UI** unless the user named a catalog `id`, refs, or a visual restyle. Skip it on an isolated component unless they asked for a visual restyle. Skip it on `redesign` and `polish`: disk owns the look. Skip it on invent-all (`you-decide`).

When occupancy is owned and Look is still unnamed: ask **one** Style question (user's language): whether they want to pick a design style. Options: yes; no (object craft, `style=none`). Other is a typed `id`, Item number, or `none`.

If **no** or `none`: Look = `you-decide`. Open [after-briefing.md](after-briefing.md). Direction locks `style=none` and does not match catalog **When**.

If **yes**: this turn ends. Next turn open [catalog.md](catalog.md), print that table in chat, and ask **one** pick: which Item or `id`. Options: **none** (object craft) and Other (type the `id` or Item number). Do not put thirty ids in the host option list. Printing that table before the user said yes fails this file.

A named `id`, Item number, or 1–3 sites with a craft *why* in the prompt fills Look and skips Style.

Filled when the user named a catalog `id`, an Item number, a look that maps to one id, 1–3 sites with a craft *why*, Style **no** / **none** (`you-decide`), invent-all (`you-decide`), origin is redesign/polish, or task is app UI and Look was skipped (`none`).

Job, bio, "unique", and quality adjectives do not fill a named Look `id`. App UI skipped Look stays `none`.

## Redesign

Applies when Classify named `origin=redesign`. Do not ask Scene, Look, Theme, Palette, Stack, or A/B. Do not print the Catalog.

**Aim** is the expected outcome. Without it, Direction fails. Filled when the user named what should be true after the redesign that is not true now. Silence is blank.

When Aim is among remaining blanks: glance at the existing page (not a tour). Include Aim in the structured question call with four readings that fit the prompt and that glance:

- The primary action fails
- The first fold does not state the job
- IA hides what the visitor or operator came to do
- The visual no longer matches this product (brand tokens stay)

Other is the user's sentence. Map onto Lock `aim=`.

**Keep** is preservation intent. Filled when the user named what must still feel like this product, or said `all of these`. When it is among remaining blanks: wordmark + nav; routes and analytics; copy voice; accent and tokens; all of these. Other names the sacred piece. Map onto Lock `keep=`. Direction owns preservation rules; do not open [redesign.md](redesign.md) from this file.

**Scope** is how far composition may change. Filled when the user named first viewport, this page, or this flow. When it is among remaining blanks: First viewport only; this page (sections); this flow (linked pages, same chrome). Suggested default in the option labels: this page. Map onto Lock `scope=` (`first-viewport` / `page` / `flow`).

**Audience** after Scope: ask only if Aim names a new public or the prompt does not name who uses the surface now. Disk + Job otherwise fill it.

**Success** if still blank. Options: verb + object readings from the page and Aim.

Do not ask **Behave** or **Constraints** unless Aim named motion, states, artifacts, or restrictions. Unnamed Behave and Constraints are owner `none`. Constraints must not repeat Keep.

1–3 pasted reference sites with a *why* fill flavor for Direction and, when the *why* names occupancy, Scene.

Done when Aim, Keep, and Scope have owners. Then open [after-briefing.md](after-briefing.md). Scan and audit run in Direction. Do not open [redesign.md](redesign.md) from this file.

## Polish

Applies when Classify named `origin=polish`. This file is not the owner. Open [polish.md](polish.md).

## Worked examples

### Portfolio bio (marketing loose)

Prompt: *Create a unique web page to showcase my work. My background: I have been a software engineer for N years and created and delivered high-quality software, such as `example 1`, `example 2`, and `example 3`.*

Job filled. Not invent-all. Infer `character=risk=trust; time=scan; enter=example 1; spectacle=mid`. `first-character-costume=charcoal + coral + fake terminal + three project cards`. Name = working title. Audience = hiring managers. Ask A/B this turn. After the pick, ask Style yes/no. Do not ask Name, Audience, Use, Scene, Theme, Palette, Behave, or Constraints. Do not print the Catalog until they said yes.

### Law firm (marketing loose)

Prompt: *Site para um escritório de advocacia.*

```txt
character=risk=trust; time=document; enter=parecer; spectacle=low
first-character-costume=navy + serif + columns + justice photo
A: document rhythm; join=stack; enter=parecer; success=agendar consulta
B: proof beside the argument; join=split; enter=caso; success=falar com o escritório
```

Neither card is navy columns or a values-card grid. Theme stays unset for Direction craft (light unless disk says otherwise). Palette is not navy.

### Tech product landing

Prompt: *Landing page de um produto de tecnologia.*

```txt
character=risk=impact; time=demo; enter=the product artifact; spectacle=mid
first-character-costume=mesh + HUD + id=cyberpunk
A: the instrument is the field; join=overlap; enter=the instrument; success=começar o trial
B: artifact + action; join=split; enter=the instrument; success=ver o produto
```

Overlap is one valid option when the prompt already holds an artifact that can *be* the field. Stack vs split is also valid. Do not pick `id=terminal` because the Job said tech.

### SaaS they built

Prompt: *Landing page para o SaaS que eu criei.*

```txt
character=risk=impact; time=scan; enter=the product; spectacle=mid
first-character-costume=indigo + three feature cards + id=saas
A: thesis then action; join=stack; enter=the product; success=começar
B: product beside the action; join=split; enter=the product; success=ver o produto
```

Do not invent features. Enter is the product named in the prompt, or Success's object if they named no artifact.

### Empty prompt

Prompt: *Cria uma landing.*

Ask Job only. After the answer, infer `character=` and ask A/B. After the pick, ask Style. Do not invent a product named Nexus.
