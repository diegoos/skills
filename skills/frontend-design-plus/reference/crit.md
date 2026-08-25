# Crit

Run from the QA slot ([dispatch.md](dispatch.md#qa)) after markup, before pre-flight. Isolated component: skip this file ([after-briefing.md](after-briefing.md#isolated-component) — no crit slot). Origin `polish` on marketing or app UI: skip this file ([polish.md](polish.md)). Fill from the **Packet and DESIGN.md**, not by reopening [briefing.md](briefing.md). Three hats in order: **frame** (presenter) → **silent written crit** (no edits) → **rank**. Critique the files, not the prompt. Praise is a keep-list, not a ship signal.

If you have not framed, you must not critique. If you have not written and ranked, you must not return. QA does not edit markup, CSS, or JS.

## Frame (write this from the briefing, then stop)

Fill from the **Packet and DESIGN.md**, not from the markup you just wrote. A missing line means ask or shrink the job; do not invent users.

```txt
User: <audience + job>
Goal: <user outcome; product outcome>
Constraints: <DESIGN.md, stack split, a11y, origin greenfield|redesign|polish>
Looking for / not: <hierarchy, path to CTA, file split> / <radius trivia, extra pages, new product name>
```

Done when a *cold reader* could judge the work against those four lines. A *context vacuum* ("what do you think of this page?") fails this step. An anti-slop hit may set `rule=` on the P0/P1 row ([anti-slop.md](anti-slop.md#rule-ids)). Persona tests and invented users fail this file.

## Silent written crit

Zero markup/CSS/JS edits in this step. Walk the primary task, not a visual tour. If a screenshot or browser exists this run, walk that render. Do not invent visual tells from an imagined page. Without visual evidence, skip visual tells and record them unverified. Occupancy is not unverified: marketing greenfield/redesign requires Sketch, `tracks=`, and `data-mass` on disk. Findings name a **user problem** (`this may cause trouble because…`), not a widget recipe. Ban "I like."

Write the triad, then the table. Empty failures are allowed only after an explicit scan of Q1 ([Question 1](#silent-written-crit)), the *cut*, empty grid tracks, 320 / 768 / 1024 viewports, form error row when a form exists, structural a11y, chrome containment at 1024 / 1440 on app UI, and logo-swap on marketing greenfield/redesign. "No issues" without that scan fails the gate.

**(a) What works** — one keep, tied to the user or business goal.

**(b) User-goal failures** — named risks. Unlinked taste is invalid.

**(c) One alternative** — the answer to **How would a UX expert improve this?** Not a color or 8px nudge. Greenfield/redesign **marketing:** a different *map* from leftover Packet *objects*. **App UI:** a different product recipe (`queue-home` / `list-filter` / `editor` / `accounts`), or in-place craft if that recipe is already on screen. Origin `polish`: in-place craft or a named deletion that keeps the current family. "More polish" as empty praise still fails.

| #   | Question                                                                                                                                                                                                                                                                                                                                                     | Fail if                                                                                                                                                                                    |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | **First viewport matches Sketch?** Marketing: measured vs Sketch ≤1 col; `See:`=enter noun in rectangle text/alt (not `data-mass`); `scale=` holds; costume fails; CTA=Success; unused browser on those claims is P0. App UI: main= matches recipe; greeting or 4 KPIs fail; recipe=none OK on settings.                                                     | Sketch/`tracks=`/`scale=` absent; `See:` not enter text; `scale=` miss; costume on screen; `distinct=`=data-mass/class/color; generic CTA; missing main=/proof=; polish                    |
| 2   | **(c) above** — *map* (marketing greenfield/redesign), recipe or in-place craft (app UI), in-place craft or deletion (polish)                                                                                                                                                                                                                                | Empty, pixel tweak, or "more polish"; new folds or recipe on origin=polish; marketing family on app UI                                                                                     |
| 3   | First viewport states the job and shows the primary action. Marketing greenfield/redesign: logo-swap must break the read; each fold shows its *object* in Packet `form=`; removing the *break* kills P0; `scan=` path holds P0 and CTA. App UI: work queue in `main`, chrome in the rail.                                                                    | Hero is vibe-only; logo-swap still reads; fold without its *object* or *form*; *break* can leave without killing P0; greeting occupies `main`; chrome overflows                            |
| 4   | Wordmark and copy use the briefing name                                                                                                                                                                                                                                                                                                                      | Invented startup or handle (Nexus, Cloudly, swe-13) without invent-all                                                                                                                     |
| 5   | Files match Packet `stack=` and the tree Implement wrote; default stack is not one-file HTML+CSS                                                                                                                                                                                                                                                             | One-file HTML+CSS on the default stack; React Lock + vanilla dump                                                                                                                          |
| 6   | Colors and type are DESIGN.md tokens, not a second palette                                                                                                                                                                                                                                                                                                   | Raw hex in markup; extra fonts                                                                                                                                                             |
| 7   | Scope is the asked surface                                                                                                                                                                                                                                                                                                                                   | Extra pages, auth, or dashboard not requested                                                                                                                                              |
| 8   | Copy is real draft, not lorem / Jane Doe / gray boxes as photos. Marketing: H1, sub, and CTA *divide* ([anti-slop.md](anti-slop.md#copy-tells)).                                                                                                                                                                                                             | Placeholders; H1/sub/CTA paraphrase; portable slogan; chrome-speak                                                                                                                         |

## Prioritize

Cluster duplicates. P0: Q1 fail, name, file split, DESIGN.md drift, missing primary action, contrast, scope creep. Marketing also: interchangeable first viewport; *break* that can leave without killing P0. App UI also: chrome overflow, duplicate filled CTA, work queue missing from `main`. P1: alternative from (c); Lock `theme=system` without a working chrome switch. P2: motion, radius.

Bikeshedding waits. Rank P0 before P1 before P2. Inside P0: functional (contrast, overflow, clipping, missing primary action) first, then structural (Q1 / Sketch / `tracks=`), then aesthetic tells. Suggested fix is the smallest change that closes the fail-if. Return the table. The parent resumes Implement to apply P0 (`tracks=` or `scale=` miss: CSS only, do not change `join=`), take or reject (c) with a user-goal reason (redesign: Aim/Keep/Scope), and drop P2 that fights the Lock. Q1 occupancy still failing after resume (wrong `See:`, missing Sketch): parent re-dispatches Direction. Feedback is data, not a vote.

## Return

Do not edit. Return the triad and the P0/P1 table (`#`, question, fail-if, finding, suggested fix). Pre-flight boxes attach after this file.

Done when the written triad exists, every applicable question was scanned, and the table names each P0/P1. Optional column `rule=` holds an [anti-slop.md](anti-slop.md#rule-ids) id when the finding is a listed tell. Q1 is the ship gate for the parent after Implement resume — not a license for QA to patch. The gate does **not** close on praise.
