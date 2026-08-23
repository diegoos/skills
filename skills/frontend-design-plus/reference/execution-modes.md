# Execution modes

Open this file from [after-briefing.md](after-briefing.md) or [dispatch.md](dispatch.md) after the Briefing card exists. In `solo`, reopen it only when the current slot needs the close-file contract. Do not open this file at Classify or while scoring [briefing.md](briefing.md).

The mode changes orchestration, not the quality bar. A mode is a capability contract, not a reason to skip a required decision. Mode choice itself is the three lines in [SKILL.md](../SKILL.md#execution-mode).

## Modes

| Mode | Use when | Contract |
| --- | --- | --- |
| `full` | A page or app UI needs the complete workflow and the harness supports hand-offs | Batch remaining briefing blanks in one structured question call when the host tool allows, then run Direction, Implement, QA, and the verification pass as separate slots. |
| `solo` | The harness has no worker or child-agent capability | Same briefing question contract as `full`. Keep the slot order in one window. Read only the current slot's references, close them before moving to the next slot, and preserve the Packet as the hand-off. |
| `fast` | An isolated component or a complete, low-risk prompt does not benefit from repeated turns | Pack fields already owned by the prompt or disk. Ask only remaining blanks; independent low-risk blanks share the same structured call. Run Implement, Tier A, the rubric, and verification. |

`full` is the default for marketing and app UI. Use `solo` when `full` cannot be executed. Use `fast` for isolated components, polish with a named focus, or a prompt that already owns every field that changes the surface.

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

Score every applicable briefing field against the prompt and disk in one pass before any question. Then:

- Host tool accepts multiple questions in one call: send **every remaining blank** in briefing order in that one call, then end the turn. Do not rescore or reopen this file between those fields.
- Host tool accepts only one question per call: ask the first remaining blank, declare `questions=serial` on the Lock, and end the turn.
- Origin still unclear belongs to Classify, not this budget. Do not mix origin with briefing fields.

A numbered list of questions in the chat message fails. A structured multi-question tool call is not a dump.

`fast` may omit fields the prompt or disk already own. `full` and `solo` batch the same remaining set when the tool allows. Never put task type, origin, Scene, Success, or Stack in the same **option list** as another field; each field is its own question inside the one call.

## Declaration

The parent prints `mode=<full|solo|fast>` in the Lock. When the host could not batch, also print `questions=serial`. The Implement and QA returns preserve those values and add the verification level. A missing mode is a routing failure, not a visual failure.

## Done

The selected mode is declared, its capability fallbacks are honest, `questions=serial` is present when the host could not batch, and the same Direction → Implement → QA order and quality gates apply to every mode.
