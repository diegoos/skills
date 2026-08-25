# Composition

Open from the Direction slot ([dispatch.md](dispatch.md)) when task is marketing and origin is `greenfield` or `redesign`. Skip on polish, app UI, and an isolated component. Public terms live in [SKILL.md](../SKILL.md#words). This file owns the internal occupancy grammar (*kinship*, *join*, *costume*). Unanswered blanks belong to the Briefing card; do not reopen [briefing.md](briefing.md).

Same pass as Direction. Style Pick and markup wait until this file's done criterion holds. Occupancy is *job* → *objects* → *kinship* → Sketch. A named style is a craft path after Frame. [layout-patterns.md](layout-patterns.md) stays closed in this slot; fold vocabulary waits for Implement. Do not open [implement.md](implement.md) from this file. The model chooses *join* (A/B winner, or one Sketch on invent-all). This file orients craft; it does not fail a layout for lacking originality.

## Words

- *job* — one line: “The user is here to ______.” The verb is the product task.
- *objects* — domain nouns (deal, SKU, kiln, KPI delta). Not navbar, hero, card, sidebar.
- *character* — four axes from the Briefing card: risk, time, enter noun, spectacle. How this domain's layout behaves. Not a catalog `id`.
- *costume* — the first category outfit (`first-character-costume=`). Owner is Packet `character=` / `first-character-costume=`. The axis stays; the outfit cannot vest Frame, Pick, or CSS.
- *kinship* — two *objects* answer the same question → same inner rectangle, smaller gap. Distinct tasks → sibling rectangles, larger gap.
- *join* — how enter and rest share the first viewport: `stack` / `split` / `full-bleed` / `overlap` of the *same* object. Ratio is not a join.
- *scan* — reading path of the first viewport: `pyramid` (thesis + action first), `Z` (sparse, CTA on the path corners), `F` (dense proof, left-anchored). Chosen from Job + *character*, not as a style.
- *form* — how the enter *object* displays: `list` | `table` | `magazine` | `split-tasks` | `catalog-cards`. The object asks; a card farm does not.
- *thesis* — one sentence of *this product's experience*. A style name fails. Occupancy lives in the Sketch, not in this sentence.
- *tension* — optional pair this product justifies (precise+human). `none` is valid. Craft contrast in DESIGN.md, not a catalog **When** match.
- *sketch* — 12-column ASCII of first-viewport masses. Grammar in Frame. The Packet occupancy is this block. App UI and polish: `Sketch=none`.
- *break* — the one *object* with no *kinship* to enter or rest. Occupancy irregularity, not craft.

## Job

Complete from the Briefing card: “The user is here to ______.” Add context, frequency, friction, and knowledge level when the brief named them.

Done when a *cold reader* can say what the user came to *do*. The sentence names no hero, card, sidebar, bento, or mesh.

## Character

Copy `character=` and `first-character-costume=` from the Briefing card. invent-all with a Job: write them here if the card omitted them. App UI and polish: `character=none`.

Choose `scan=` from Job + *character*:

- `pyramid` — trust, document time, first visit, a single action (firm, SaaS for a new buyer).
- `Z` — sparse, few objects, one artifact + one action (product landing).
- `F` — dense proof, comparison, long read.

Choose `form=` for enter from the object: schedule/queue → `list`; compare → `table`; argument/tese → `magazine`; two sibling tasks → `split-tasks`; a catalog of independent items → `catalog-cards`. A firm enter is `magazine`, not `catalog-cards`.

Done when `character=`, `first-character-costume=`, `scan=`, and `form=` exist on marketing greenfield. The costume is not a Frame mass, a catalog `id`, or a palette.

## Objects

List information and action entities this *job* must show. Numbered. At most 7. Each line: domain noun + what the user does with it (know / do / compare / discover / monitor / decide). Success stays on the list.

Greenfield: every line traces to a briefing field, the A/B enter object, or a Headlines sentence. Redesign: the list is the keep blocks from the audit already in this slot.

Done when the numbered list exists, every item traces to the brief or the audit, Success is on it, and each line is a domain noun — not a component. An empty list or an invented object fails this step. A line that is only `hero`, `card`, `section`, `CTA`, `feature`, or `benefit` fails unless that word is the product's actual object in the brief. On a thin brief, Success's object stays on the list; `character=` enter stays if it traces to the prompt. Do not add `claim` as a noun.

## P0

At most one perception P0 and one action P0. Drop objects until the *job* + Success still hold. At most 5 remain. P3 may vanish. Success stays.

Done when each P0 fits in a phrase, three competing blocks are named and off the page (`Cut:`), the remaining list is ≤5, and Success is still on it. Everything-is-P0 fails this step.

## Hierarchy

Write one line: first / second / rest. First is the perception P0. Second is the action P0 or the next *object*. Rest is everything that survived the cut.

Done when a *cold reader* points at the P0 without naming a component. “The hero” as first fails this step.

## Kinship

Draw rectangles for the remaining *objects* before occupancy.

1. Mark *kinship*. The number of visible groups *is* occupancy.
2. Inner gap < gap between groups < gap between regions. If every gap is 8–16px, occupancy is flat — open space *between* groups.
3. Group in this order: alignment → similarity → proximity. Container last. A container around groups that already cluster is noise — removing it increases useful occupancy.
4. Each group has a reason: information unit, comparison set, or persistent control. “SaaS has a sidebar” is not a reason.

Done when groups exist, each has a reason from that list, and a *cold reader* can name who shares a rectangle. Numbers of columns wait for Frame.

## Occupancy

### A/B pick (`direction=A|B`)

Write one Sketch from the picked card's `join`. The user's join is authorship. The picked join must not be Packet `first-character-costume=`.

Done when `direction=` exists, Sketch `join=` is the picked token, and line 3 of Frame is rectangles of *objects* — not a hero family.

### invent-all, redesign, or no A/B

Write **one** Sketch. Pick a `join` that is not the category scaffold in `first-character-costume=`. The first workable idea may survive. Do not write three occupancy cards.

Done when one Sketch exists, `join=` is one of `stack | split | full-bleed | overlap`, and Frame line 3 is rectangles of *objects*.

## Frame

Quote Scene first when the user named a place, a remembered page, or an occupancy sentence. A/B pick: occupancy from the winning card. Redesign: occupancy from keep blocks + Aim; do not invent a new place.

On `you-decide` / `none` / invent-all: do not write column numbers until *kinship* rectangles exist. A category-default place fails ("desk at night" for a developer portfolio). `first-character-costume=` as a place or palette fails.

On the surviving occupancy, size the first-viewport rectangles. Name the largest element, the second, deliberate empty, and where the grid breaks. Each points at a P0/P1 *object*.

**enter** — the lead *object*'s rectangle + the strongest type/shape contrast, with occupancy (column span or `fr`), in Packet `form=`. That rectangle is the most characteristic thing in the subject's world (artifact, instrument, material, vernacular) in the form the *object* asks — not a generic headline + CTA. Asset only when *objects* already hold one. No asset: type takes the larger track. Do not add a stock photo to satisfy a “real visual” check. Do not add a category photo (lawyer in a suit, laptop on white) to look on-domain.

**rest** — the Success control, with occupancy. One primary. Never full-bleed. Medium gap with enter (same task, not the same title). The visible CTA label is the Success verb+object.

***break*** — the one *object* with no *kinship* to enter or rest. Occupancy is overlap of the *same* object, a full-bleed band (when that object *is* the band), or span of the remainder. A two-mass page is valid: `break=none` plus why. Fabricating overlap to fill the Packet fails.

**Contrast when `break=none`.** One mass is clearly larger, empty is named, or enter has a type/shape jump against rest. Three equal bands fail this step.

Licensed overlap: two *objects* contest the same place (the kiln photo *is* the object; the title is its label). Overlap-badge in the gutter: the *break* can leave without killing P0 — cut it.

A media-column + CTA-rail split still needs *kinship* of two sibling tasks.

The *scene* sentence, when written here, includes those occupancy numbers and names what lives in each mass.

**Sketch.** Write a 12-column ASCII of the first viewport into the Packet and into DESIGN.md **Layout**. The drawing does not reopen occupancy.

```txt
Sketch:
[<object span>][<object span>]
join=<stack|split|full-bleed|overlap> tracks=enter <n> rest <n|inset|below> break <n|none> scan=<pyramid|Z|F> form=<list|table|magazine|split-tasks|catalog-cards>
```

1–3 lines. Each cell names an Inventory *object* — not “hero”. Footer `join=` is the A/B winner or the invent-all choice. Visible columns on the first row sum to 12. `overlap`: enter 12, rest `inset`. `stack`: enter 12, rest `below`. `full-bleed`: enter 12, rest `inset` or `below`. `split`: enter + rest = 12. `break` is a later row or `none`; a break band may be 12. Frame occupancy numbers match the footer. A Frame with numbers and no Sketch fails. P0 and the Success control sit on the `scan=` path (pyramid = first look; Z = path corners; F = left column).

Done when a *cold reader* can read the Sketch and say *what* lives in each cell. Removing the *break* destroys P0; if it does not, the *break* is a badge. Occupancy numbers missing on a named Scene fail. `you-decide` without *kinship* rectangles fails. Sketch absent fails. Costume vest fails. `scan=` / `form=` missing on greenfield marketing fail.

## Thesis

One experience sentence plus the Sketch block into DESIGN.md **Layout**. Lock bands still mutate spacing; they do not replace the sentence or the Sketch. Occupancy numbers live in the Sketch footer, not in this sentence.

Done when the experience sentence names no style id and the Sketch is in Layout. Sketch absent fails. If DESIGN.md is not on disk yet, keep the sentence and the Sketch for the DESIGN.md step.

## Map

Fold 2 and fold 3 are leftover *objects*. Each fold names an *object* from the list and the *form* that object asks for (`list` | `table` | `magazine` | `one-proof` | `cta` | `catalog-cards`). A fold with no object is cut (two-fold page). Spec, FAQ, logo wall, or a process section exist only as listed *objects*. Card-family only when the object *is* a catalog of independent items.

Write `folds=<enter object>:<form> | <fold2 object>:<form> [| <fold3 object>:<form>|cut]`. An optional family name may follow; it must not rewrite occupancy.

Done when each remaining fold names an *object* and a *form*, `folds=` traces to Inventory, and occupancy is unchanged. Filling a fold with an object that was not on the list fails this step. Icon + title + blurb × N fails unless the object is a catalog of items.

## File done

Direction only. Every heading above has met its own done criterion. Sketch is in the Packet and in DESIGN.md **Layout**; costume does not vest; `folds=` lists leftover *objects* with `:<form>`. Style Pick may run.

Parent does not use this heading. Parent checks presence and Sketch/Inventory string overlap on the Packet ([dispatch.md](dispatch.md#valid-packet)).

## Worked: A/B law firm

Briefing: Job = site for a law office; `direction=A`; Success = agendar consulta.

```txt
character=risk=trust; time=document; enter=parecer; spectacle=low
first-character-costume=navy + serif + columns + justice photo
direction=A
scan=pyramid
form=magazine
job=The user is here to book a consult after reading what the firm handles.
P0=perception: the matter they brought; action: book a consult
Inventory: parecer (know); Agendar consulta (do)
kinship=parecer and Agendar consulta are one task
join=stack
Sketch:
[======== parecer 12 =================]
[======== Agendar consulta below =====]
join=stack tracks=enter 12 rest below break none scan=pyramid form=magazine
Thesis: Read the matter, then book.
folds=parecer:magazine | cut
```

Navy columns, a justice photo, or three “áreas de atuação” cards **fail** this Packet. `id=professional` as Pick **fails**.

## Worked: A/B product with a field artifact

Briefing: Job = landing for a firing-slot product they built; the prompt names the kiln; `direction=A`; Success = book a firing slot. The picked join may be overlap, split, or stack so long as it is not the costume.

```txt
character=risk=impact; time=demo; enter=kiln; spectacle=mid
first-character-costume=studio hero photo + three firing-type cards
direction=A
scan=Z
form=split-tasks
job=The user is here to book a firing slot before the kiln cools.
P0=perception: kiln in fire; action: book a slot
Inventory: kiln in fire (know); firing schedule (monitor); Book a slot (do)
kinship=kiln photo is the field; Book a slot is its label
join=overlap
Sketch:
[============ kiln in fire 12 ============]
join=overlap tracks=enter 12 rest inset break none scan=Z form=split-tasks
Thesis: Book the next firing on the kiln that is still on.
folds=kiln in fire:one-proof | firing schedule:list | cut
```

Three equal firing-type cards **fail**. A type-led stack with the slot as P0 is valid when that is the A/B pick or the invent-all choice.
