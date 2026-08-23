# Composition

Open from the Direction slot ([dispatch.md](dispatch.md)) when task is marketing and origin is `greenfield` or `redesign`. Skip on polish, app UI, and an isolated component. Unanswered blanks: [briefing.md](briefing.md) via the Briefing card.

Same pass as Direction. Style Pick and markup wait until this file's done criterion holds. Occupancy is *job* → *objects* → *kinship*. A named style is a craft path after Frame. [layout-patterns.md](layout-patterns.md) stays closed in this slot; Implement opens fold vocabulary after `tracks=` ([implement.md](implement.md)).

## Words

- *job* — one line: “The user is here to ______.” The verb is the product task.
- *objects* — domain nouns (deal, SKU, kiln, KPI delta). Not navbar, hero, card, sidebar.
- *kinship* — two *objects* answer the same question → same inner rectangle, smaller gap. Distinct tasks → sibling rectangles, larger gap.
- *topology* — who shares a rectangle, where empty sits, and the *join* (stack / split / full-bleed / overlap of the *same* object). Ratio is not *topology*.
- *thesis* — one sentence of *this product's experience*. A style name fails.
- *tension* — two contrasting traits *this* product justifies (precise+human, editorial+functional). An axis, not a moodboard.
- *recombination* — the named pattern plus this context. The test is best for *this* user, not first-ever.
- *object-swap* — put another product's P0 perception in the largest Sketch cell. Required when Inventory has ≥2 domain nouns; otherwise `n/a`. Grammar in Frame. App UI and polish: `none`.
- *sketch* — 12-column ASCII of first-viewport masses. Grammar in Frame. App UI and polish: `Sketch=none`.
- *break* — the one *object* with no *kinship* to enter or rest. Occupancy irregularity, not craft.

## Job

Complete from the Briefing card: “The user is here to ______.” Add context, frequency, friction, and knowledge level when the brief named them.

Done when a *cold reader* can say what the user came to *do*. The sentence names no hero, card, sidebar, bento, or mesh.

## Objects

List information and action entities this *job* must show. Numbered. At most 7. Each line: domain noun + what the user does with it (know / do / compare / discover / monitor / decide). Success stays on the list.

Greenfield: every line traces to a briefing field or a Headlines sentence. Redesign: the list is the keep blocks from the [audit](redesign.md#audit-before-changing).

Done when the numbered list exists, every item traces to the brief or the audit, Success is on it, and each line is a domain noun — not a component. An empty list or an invented object fails this step. A line that is only `hero`, `card`, `section`, `CTA`, `feature`, or `benefit` fails unless that word is the product's actual object in the brief. On a thin brief, Success's object (the thing the verb acts on) stays on the list; do not add `claim` as a noun.

## P0

At most one perception P0 and one action P0. Drop objects until the *job* + Success still hold. At most 5 remain. P3 may vanish. Success stays.

Done when each P0 fits in a phrase, three competing blocks are named and off the page, the remaining list is ≤5, and Success is still on it. Everything-is-P0 fails this step.

## Pattern

Name the known pattern that solves this *job* (PDP, editorial split, studio booking, manifesto, catalog). Filter: which audience that “best practice” was written for. If that audience ≠ the *job* phrase, write what breaks here.

The added value is a nameable sentence: missing feature, different public, different tone, different model. Same-as-existing is validation. *Recombination* is that pattern in this context.

Done when (a) the pattern has a name, (b) “this best practice fails here because…” exists, and (c) the added value points at an *object* or a P0, not a style id.

## Hierarchy

Write one line: first / second / rest. First is the perception P0. Second is the action P0 or the next *object*. Rest is everything that survived the cut.

Done when a *cold reader* points at the P0 without naming a component. “The hero” as first fails this step.

## Kinship

Draw rectangles for the remaining *objects* before any occupancy card.

1. Mark *kinship*. The number of visible groups *is* occupancy.
2. Inner gap < gap between groups < gap between regions. If every gap is 8–16px, occupancy is flat — open space *between* groups.
3. Group in this order: alignment → similarity → proximity. Container last. A container around groups that already cluster is noise — removing it increases useful occupancy.
4. Each group has a reason: information unit, comparison set, or persistent control. “SaaS has a sidebar” is not a reason.

Done when groups exist, each has a reason from that list, and a *cold reader* can name who shares a rectangle. Numbers of columns wait for Frame.

## Three occupancies

Write three cards from those *kinship* groups. Each card is four lines:

1. *thesis* (this product's experience)
2. *tension* (a pair this product justifies)
3. *topology*: who is largest, who is second, where empty sits, and the *join* token (`stack` / `split` / `full-bleed` / `overlap` of the *same* object)
4. three reasons: user + business + evidence. A style name is not a reason.

Cards differ in *join* token, not in catalog ids and not in column ratio of the same *join*. Swiss / botanical / neo-brutal as card titles fail this step. Three splits that differ only in column ratio fail this step. The first idea is not the solution.

Discard two with one sentence each, tied to *job* / P0 / audience. The survivor is not “the farthest from the median.”

Done when three cards exist, the three *joins* are three distinct tokens from `stack | split | full-bleed | overlap`, two discards name a *job* reason plus that token, and the survivor's line 3 is rectangles of *objects* — not a hero family.

## Frame

Quote Scene first when the user named a place, a remembered page, or an occupancy sentence. Redesign: occupancy from keep blocks + Aim; do not invent a new place.

On `you-decide` / `none` / invent-all: do not write column numbers until *kinship* rectangles exist. A category-default place fails ("desk at night" for a developer portfolio).

On the surviving card, size the first-viewport rectangles. Name the largest element, the second, deliberate empty, and where the grid breaks. Each points at a P0/P1 *object*.

**enter** — the lead *object*'s rectangle + the strongest type/shape contrast, with occupancy (column span or `fr`). That rectangle is the most characteristic thing in the subject's world (artifact, instrument, material, vernacular) in the form the *object* asks — not a generic headline + CTA. Asset only when *objects* already hold one. No asset: type takes the larger track. Do not add a stock photo to satisfy a “real visual” check.

**rest** — the Success control, with occupancy. One primary. Never full-bleed. Medium gap with enter (same task, not the same title).

***break*** — the one *object* with no *kinship* to enter or rest. Occupancy is overlap of the *same* object, a full-bleed band (when that object *is* the band), or span of the remainder. A two-mass page is valid: `break=none` plus why. Fabricating overlap to fill the Packet fails.

Licensed overlap: two *objects* contest the same place (the kiln photo *is* the object; the title is its label). Overlap-badge in the gutter: the *break* can leave without killing P0 — cut it.

The formula `asset ≥7/12` / `type ≥8/12` is fallback only when Scene is empty **and** no *object* imposes asymmetry — record `fallback=yes` with the words “fallback, not thesis”, then size enter from the surviving *join*. A media-column + CTA-rail split still needs *kinship* of two sibling tasks.

The *scene* sentence, when written here, includes those occupancy numbers and names what lives in each mass.

**Sketch.** Write a 12-column ASCII of the first viewport into the Packet and into DESIGN.md **Layout**. The drawing does not reopen occupancy.

```txt
Sketch:
[<object span>][<object span>]
join=<stack|split|full-bleed|overlap> tracks=enter <n> rest <n|inset|below> break <n|none>
```

1–3 lines. Each cell names an Inventory *object* — not “hero”. Footer `join=` is the surviving card's token. Visible columns on the first row sum to 12. `overlap`: enter 12, rest `inset`. `stack`: enter 12, rest `below`. `full-bleed`: enter 12, rest `inset` or `below`. `split`: enter + rest = 12. `break` is a later row or `none`; a break band may be 12. Frame occupancy numbers match the footer. A Frame with numbers and no Sketch fails.

**Object-swap.** SSOT for this check. Parent and QA point here; they do not restate the count.

Count Inventory nouns that trace to the brief, Keep, the redesign audit, or a named artifact in Constraints. Do not count Success's verb alone. Do not count `hero`, `card`, `section`, `CTA`, `feature`, or `benefit` unless that word is the product's actual object.

**≥2 domain nouns.** Write `object-swap=<foreign P0> in enter does not read because <this job's kinship>`. The foreign P0 is not an Inventory noun. The `because` clause cites an Inventory noun that is on the list. Put that foreign P0 in the largest Sketch cell. If `tracks=` and `join=` stay the same, rewrite *kinship* (the occupancy is a template). Done: the swap does *not* read — the Sketch cells would have to change. An omitted line, `object-swap=n/a`, a foreign noun that is already on Inventory, a `because` that names no Inventory noun, or a swap that still reads fails.

**<2 domain nouns.** Write `object-swap=n/a`. Three occupancy cards with distinct *joins* still run. Do not invent an object, place, or kinship to pass a swap. A `because` line, a kiln-like artifact that was not on the brief, or omitting `n/a` fails.

Scene named or `you-decide` does not flip this check. invent-all: count after the invented Inventory exists. App UI and polish skip this section (`object-swap=none`).

Done when a *cold reader* can read the Sketch and say *what* lives in each cell. Removing the *break* destroys P0; if it does not, the *break* is a badge. Occupancy numbers missing on a named Scene fail. `you-decide` without *kinship* rectangles fails. Sketch absent fails. Object-swap fails this file's Object-swap check.

## Thesis

Two sentences plus the Sketch block into DESIGN.md **Layout**: the survivor's *thesis* (experience), then enter / rest / *break* with occupancy — or two masses and `break=none` — then the Sketch. Lock bands still mutate spacing; they do not replace these sentences, the Sketch, or occupancy.

Done when the experience sentence names no style id, the occupancy sentence names the masses that exist (two or three) with numbers, the Sketch is in Layout, and Object-swap holds. A sentence without occupancy fails. Sketch absent fails. If DESIGN.md is not on disk yet, keep the sentences and the Sketch for the DESIGN.md step.

## Map

Fold 2 and fold 3 are leftover *objects*. Each fold names an *object* from the list. A fold with no object is cut (two-fold page). Spec, FAQ, logo wall, or a process section exist only as listed *objects*.

Write `folds=<enter object> | <fold2 object> [| <fold3 object>|cut]`. An optional family name may follow; it must not rewrite occupancy. Matching a hero family is not required.

Done when each remaining fold names an *object*, `folds=` traces to Inventory, and occupancy is unchanged. Filling a fold with an object that was not on the list fails this step.

## File done

*Job* phrase owned. *Objects* listed. P0 named. Pattern filtered. Hierarchy line written. *Kinship* rectangles drawn. Three occupancy cards with three distinct *join* tokens from `stack | split | full-bleed | overlap`; two discarded with a *job* reason. Frame masses with occupancy (two-mass page allowed). Sketch present: footer `join=` is the survivor, `tracks=` matches Frame, cells sum to 12, labels ⊂ Inventory. Packet `object-swap=` holds the Frame Object-swap check (`n/a` or a swap that does not read). *Thesis* (experience + occupancy) and the Sketch in DESIGN.md Layout. `fallback=yes` only with “fallback, not thesis”. `folds=` lists leftover *objects*. Style Pick may run.

## Worked: you-decide marketing

Briefing (owners only): Name = Kiln Desk; Audience = studio managers; Success = book a firing slot; Use = a scan of minutes; Scene = `you-decide`; Look = `you-decide`. Inventory has kiln + slot (≥2 domain nouns): object-swap is required.

Type-led stack (Look that needs no named Path):

```txt
job=The user is here to book a firing slot before the kiln cools.
P0=perception: the next open slot; action: book a slot
pattern=studio manifesto; fails here because managers scan a slot, not a catalog
tension=calendar precision + spoken heat
kinship=open slot and Book a slot are one task; schedule is fold 2
joins=stack | split | full-bleed
discarded=split (invented photo: no asset on the object list); full-bleed (three-up firing types: P0 becomes a tile)
fallback=no
Frame:
  enter: the open slot stacked type
  rest: Book a slot in the same column, medium gap
  break=none — two masses, one column
Sketch:
[======== open slot 12 ================]
[======== Book a slot below ==========]
join=stack tracks=enter 12 rest below break none
Thesis: The next slot is open; book it in the same column. Type stack, Book a slot below, no third mass.
folds=open slot | firing schedule | cut
object-swap=a dentist headline in enter does not read because fold 2 must be this kiln schedule or the page is a template
```

Overlap, same briefing:

```txt
job=The user is here to book a firing slot before the kiln cools.
P0=perception: kiln in fire; action: book a slot
pattern=PDP studio booking; fails here because the kiln is the product, not a SKU grid
tension=industrial heat + calendar precision
kinship=kiln photo is the field; Book a slot is its label (same rectangle)
joins=overlap | split | stack
discarded=split (equal three-up catalog: P0 kiln becomes a tile); stack (manifesto type: booking control leaves the kiln)
fallback=no
Frame:
  enter: kiln in fire full-bleed
  rest: Book a slot on the same mass
  break=none — the control is the kiln's label; a gutter badge would leave without killing P0
Sketch:
[============ kiln in fire 12 ============]
join=overlap tracks=enter 12 rest inset break none
Thesis: Book the next firing on the kiln that is still on. Kiln full-bleed, Book a slot on that mass, no third mass.
folds=kiln in fire | firing schedule | cut
object-swap=a SaaS status chart in enter does not read because the kiln photo is the field and Book a slot is its label
```

A ratio-only split (wide media column + CTA rail, no *kinship* of label-on-field) **fails** this *thesis*: object-swap still reads. Style Pick vests heat/material on the kiln mass after this Packet; it does not choose the *join*.

## Worked: thin brief (`object-swap=n/a`)

Briefing (owners only): Name = North Clinic; Audience = new patients; Success = book a visit; Use = a scan of minutes; Scene = `you-decide`; Look = `you-decide`. Inventory is Success's object only (visit). Do not invent a kiln, a place, or a second domain noun.

```txt
job=The user is here to book a visit.
P0=perception: the visit; action: book a visit
pattern=clinic booking; fails here because the brief names no instrument beyond the visit
tension=calm + a single action
kinship=the visit and Book a visit are one task
joins=stack | split | full-bleed
discarded=split (invented photo: no asset on the list); full-bleed (three visit types: P0 becomes a tile)
fallback=yes — fallback, not thesis
Frame:
  enter: the visit stacked type 12
  rest: Book a visit below
  break=none — two masses, one column
Sketch:
[======== the visit 12 ================]
[======== Book a visit below ==========]
join=stack tracks=enter 12 rest below break none
Thesis: Book the visit in the same column. Type stack, Book a visit below, no third mass.
folds=the visit | cut
object-swap=n/a
```

`object-swap=a dentist headline in enter does not read because…` **fails** this Packet: Inventory has fewer than two domain nouns; a `because` line is invented kinship.

Invalid Packet (three ratio-only splits; parent rejects before Implement):

```txt
joins=split 7/12 | split 8/12 | split 9/12
discarded=8/12; 9/12
```

Fails: the three *join* tokens are not distinct (`split` three times).

Invalid Packet (Inventory rich, swap missing or still reads):

```txt
object-swap=n/a
```

Fails on the Kiln briefing: ≥2 domain nouns, so `n/a` is illegal. `object-swap=a dentist headline in enter still reads` also fails.

Invalid Packet (Frame with numbers, Sketch absent):

```txt
Frame:
  enter: kiln in fire 12
  rest: Book a slot inset
  break=none
```

Fails: Sketch absent. File done and [dispatch.md](dispatch.md#valid-packet) use the same lines.
