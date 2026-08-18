# Crit

Run after markup, before pre-flight. Unanswered blanks: [briefing.md](briefing.md). Three hats in order: **frame** (presenter) → **silent written crit** (no edits) → **rank and fix**. Critique the files, not the prompt. Praise is a keep-list, not a ship signal.

If you have not framed, you must not critique. If you have not written and ranked, you must not edit.

## Frame (write this from the briefing, then stop)

Fill from the **brief and DESIGN.md**, not from the markup you just wrote. A missing line means ask or shrink the job; do not invent users.

```txt
User: <audience + job>
Goal: <user outcome; product outcome>
Constraints: <DESIGN.md, stack split, a11y, origin greenfield|redesign|polish>
Looking for / not: <hierarchy, path to CTA, file split> / <radius trivia, extra pages, new product name>
```

Done when a *cold reader* could judge the work against those four lines. A *context vacuum* ("what do you think of this page?") fails this step.

## Silent written crit

Zero markup/CSS/JS edits in this step. Walk the primary task, not a visual tour. Findings name a **user problem** (`this may cause trouble because…`), not a widget recipe. Ban "I like."

Write the triad, then the table. Empty failures are allowed only after an explicit scan of: first-viewport primary action, hierarchy, distinctive composition, logo-swap, three competing blocks, empty grid tracks, 320 / 768 / 1024 viewports, form error row when a form exists, structural a11y. "No issues" without that scan fails the gate.

**(a) What works** — one keep, tied to the user or business goal.

**(b) User-goal failures** — named risks. Unlinked taste is invalid.

**(c) One alternative layout family** — a different composition (editorial split vs three cards; sticky task chrome vs stacked marketing), not a color or 8px nudge. This is the answer to **How would a UX expert improve this?** Origin `polish`: (c) is an in-place craft fix or a named deletion that keeps the current family. "More polish" as empty praise still fails.

| #   | Question                                                                                                                                                                                                              | Fail if                                                                                             |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| 1   | **Is this a common AI-generated layout?** Category-reflex + second-order + interchangeability ([anti-slop.md](anti-slop.md#the-slop-test)). Name the scaffold (centered hero, three cards, purple glow, cream craft). | Yes, unless the brief named that scaffold, or origin is polish and the scaffold was already on disk |
| 2   | **(c) above** — layout family on greenfield/redesign; in-place craft or deletion on polish                                                                                                                            | Empty, pixel tweak, or "more polish"; new family on origin=polish                                   |
| 3   | First viewport states the job and shows the primary action. A logo-swap must break the read.                                                                                                                          | Hero is vibe-only; swapping the wordmark still reads as the same site                               |
| 4   | Wordmark and copy use the briefing name                                                                                                                                                                               | Invented startup or handle (Nexus, Cloudly, swe-13) without invent-all                              |
| 5   | Files follow [file-architecture.md](file-architecture.md); Lock `stack=` matches what is on disk                                                                                                                      | One-file HTML+CSS on the default stack; React Lock + vanilla dump                                   |
| 6   | Colors and type are DESIGN.md tokens, not a second palette                                                                                                                                                            | Raw hex in markup; extra fonts                                                                      |
| 7   | Scope is the asked surface                                                                                                                                                                                            | Extra pages, auth, or dashboard not requested                                                       |
| 8   | Copy is real draft, not lorem / Jane Doe / gray boxes as photos                                                                                                                                                       | Placeholders                                                                                        |

## Prioritize

Cluster duplicates. P0: name, file split, DESIGN.md drift, AI scaffold, interchangeable first viewport, missing primary action, contrast, scope creep. P1: layout family from (c). P2: motion, radius.

Bikeshedding waits. Owner synthesizes: implement P0, take or reject (c) with a user-goal reason, drop P2 that fights the Lock. Feedback is data, not a vote.

## Fix

Only now edit. Solve named user problems. Close the loop: implemented vs discarded and why. Re-run questions 1–2. Then pre-flight.

Done when the written triad exists, every P0 is fixed, question 1 is **no** (or the brief named that scaffold), question 3's logo-swap breaks the read, (c) is in the DOM or rejected with a user-goal reason, and the gate does **not** close on praise.
