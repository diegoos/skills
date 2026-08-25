# Execution modes

Open this file from [after-briefing.md](after-briefing.md) or [dispatch.md](dispatch.md) after the Briefing card exists. In `solo`, reopen it only when the current slot needs the close-file contract. Do not open this file at Classify or while scoring [briefing.md](briefing.md).

The mode changes orchestration, not the quality bar. A mode is a capability contract, not a reason to skip a required decision. Mode choice itself is the three lines in [SKILL.md](../SKILL.md#execution-mode).

## Modes

| Mode | Use when | Contract |
| --- | --- | --- |
| `full` | A page or app UI needs the complete workflow and the harness supports hand-offs | Briefing questions already ran. Run Direction, Implement, QA as separate workers. Parent holds card + Packet + return blocks only. |
| `solo` | The harness has no worker or child-agent capability | Same slot order as `full` in one window. Read only the current slot's references, close them before moving to the next slot, and preserve the Packet as the hand-off. |
| `fast` | Isolated component, `origin=polish`, or a complete low-risk prompt | Greenfield/redesign: same Direction → Implement → QA order as `full`. Polish skips Direction ([polish.md](polish.md)). Also stay closed: the Fast list in [load-map.md](load-map.md#fast). Isolated component still skips this file's Direction ([after-briefing.md](after-briefing.md#isolated-component)). |

`full` is the default for marketing and app UI. Use `solo` when `full` cannot be executed. Use `fast` for isolated components, polish, or a prompt that already owns every field that changes the surface. `fast` does not skip Direction on greenfield or redesign marketing or app UI and does not skip quality gates. `origin=polish` skips Direction ([polish.md](polish.md)). `fast` stay-closed files: [load-map.md](load-map.md#fast). Polish stay-closed: [load-map.md](load-map.md#polish).

## Capability fallback

Use the best available interface and record the fallback in the return block.

| Capability | Preferred | Fallback | What must remain true |
| --- | --- | --- | --- |
| Question interface | Host structured tool that accepts multiple questions in one call | One question per call (`questions=serial`) | Options remain mutually useful; no silent invention of an owner. |
| Worker interface | Child agent or task worker | Same-window slot hand-off | Direction, Implement, and QA stay sequential. |
| Browser interface | Browser or DevTools inspection | DOM measurements and static inspection | The result declares visual checks as `unverified` when no render was inspected. |
| Accessibility interface | Automated checker plus keyboard pass | Semantic and source inspection | The result says whether an automated check ran. |

Do not name a tool that the host did not provide. Name the capability and its evidence instead.

## Question budget

This file does not reopen [briefing.md](briefing.md) or [catalog.md](catalog.md). Questions already ran in briefing. Preserve `questions=serial` on the Lock when the briefing declared it.

A numbered list of questions in the chat message still fails if a leftover blank appears after the card. An eight-field dump fails. A structured A/B call is not a dump.

`fast` may omit fields the prompt or disk already own. Never put task type or origin in the same **option list** as another field.

## Declaration

The parent prints `mode=<full|solo|fast>` in the Lock. When the host could not batch, also print `questions=serial`. The Implement and QA returns preserve those values and add the verification level. A missing mode is a routing failure, not a visual failure.

## Done

The selected mode is declared, its capability fallbacks are honest, `questions=serial` is present when the host could not batch, and the same quality gates apply. Direction → Implement → QA holds on greenfield and redesign. Polish skips Direction ([polish.md](polish.md)).
