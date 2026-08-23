# Visual quality rubric

Open from QA after [crit.md](crit.md) and before the final ship decision. Score the rendered surface, DOM, or source evidence that exists, not the Packet's intention. Use [quality-cases.md](quality-cases.md) only when a score is ambiguous.

## Score

Give every applicable criterion `0`, `1`, or `2` and write one evidence sentence.

| Criterion | `0` | `1` | `2` |
| --- | --- | --- | --- |
| Job legibility | A cold reader cannot tell what to do | The task is inferable only after reading several blocks | The first viewport states the task and primary action |
| Domain specificity | The surface could belong to any product | Copy names the domain but layout stays portable | Objects, content, and composition make the domain necessary |
| Structural necessity | The layout is a default scaffold or decoration | The layout is plausible but one mass could be swapped without consequence | The chosen topology follows the objects and changing the lead object breaks the composition |
| Hierarchy and action | CTA, P0, or reading order is unclear | Hierarchy exists but competing blocks dilute it | P0, supporting object, and action are immediately ranked |
| Visual language | Style is a catalog costume or a random mixture | One register is present with weak justification | Type, material, color, motion, and shape form one justified register |
| Restraint | Decorative extras compete with the job | Some extras are harmless but unexplained | Every memorable detail supports the job, object, or interaction |
| Responsive integrity | Layout breaks or loses the job on small screens | Layout survives with visible compromises | Hierarchy and action survive at all required viewports |
| Evidence honesty | Claims pass without evidence or gaps are hidden | Evidence exists but important checks are unverified | Claims, measurements, screenshots, and gaps agree |

## Thresholds

Score only applicable criteria, then calculate the percentage of available points. Any `0` in Job legibility, Domain specificity, Structural necessity, Hierarchy and action, or Evidence honesty is P0. A result below 75% is not ready. A result from 75% to 87% needs a P1 decision. A result of 88% or higher may ship only when all required pre-flight and verification gates pass.

For app UI, Domain specificity means domain objects in the work plane, not novelty in chrome. For isolated components, skip Structural necessity and Domain specificity when the component has no product context.

## Distinctness check

Name three category defaults that the surface could have become. Then point to one visible decision that makes each default fail. The decision must be a markup or CSS fact on the rendered surface (object, topology, reading order, material, or interaction). “It uses a different color” is not evidence. QA accepts Distinctness only when those facts exist in the Implement `distinct=` block or can be pointed at in the DOM.

## Return

```txt
Rubric: <score>/<available> (<percentage>%)
Job=<0|1|2> — <evidence>
Domain=<0|1|2|n/a> — <evidence>
Structure=<0|1|2|n/a> — <evidence>
Hierarchy=<0|1|2> — <evidence>
Language=<0|1|2> — <evidence>
Restraint=<0|1|2> — <evidence>
Responsive=<0|1|2> — <evidence>
Honesty=<0|1|2> — <evidence>
Distinctness=<three defaults and one visible rejection for each>
```

## Done

Every applicable criterion has a score and evidence, the distinctness check names three defaults, and any P0 or threshold failure is in the QA table.
