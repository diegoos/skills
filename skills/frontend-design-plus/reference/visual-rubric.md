# Visual quality rubric

Open from QA after [crit.md](crit.md) and before the final ship decision, or from [polish.md](polish.md) after anti-slop (no crit). Score the rendered surface, DOM, or source evidence that exists, not the Packet's intention. Domain or Language `2` requires a screenshot or browser walk this run. Without it, those criteria max `1`. Honesty `0` if a visual pass is claimed without that evidence. When a score is ambiguous, calibrate against [quality-cases.md](quality-cases.md) (attached in this slot).

## Score

Give every applicable criterion `0`, `1`, or `2` and write one evidence sentence.

| Criterion | `0` | `1` | `2` |
| --- | --- | --- | --- |
| Job legibility | A cold reader cannot tell what to do | The task is inferable only after reading several blocks | The first viewport states the task and primary action |
| Domain specificity | The surface could belong to any product, or it wears `first-character-costume=` | Copy names the domain but layout stays portable | Objects and copy make the domain necessary; the category outfit fails in the DOM |
| Structural necessity | The layout is a default scaffold, decoration, or equal bands with no enter contrast | Hierarchy exists but the Sketch masses are weak | First viewport matches Sketch; enter is louder; CTA sits on the `scan=` path |
| Hierarchy and action | CTA, P0, or reading order is unclear | Hierarchy exists but competing blocks dilute it | P0, supporting object, and action are immediately ranked |
| Visual language | Style is a catalog costume or a random mixture | One register is present with weak justification | Type, material, color, motion, and shape form one justified register; `style=custom`: the render shows the signature |
| Restraint | Decorative extras compete with the job | Some extras are harmless but unexplained | Every memorable detail supports the job, object, or interaction |
| Responsive integrity | Layout breaks or loses the job on small screens | Layout survives with visible compromises | Hierarchy and action survive at all required viewports |
| Evidence honesty | Claims pass without evidence or gaps are hidden | Evidence exists but important checks are unverified | Claims, measurements, screenshots, and gaps agree |

## Thresholds

Score only applicable criteria, then calculate the percentage of available points. Any `0` in Job legibility, Domain specificity, Structural necessity, Hierarchy and action, or Evidence honesty is P0. A result below 75% is not ready. A result from 75% to 87% needs a P1 decision. A result of 88% or higher may ship only when all required pre-flight and verification gates pass.

For app UI, Domain specificity means domain objects in the work plane, not novelty in chrome. For isolated components and origin `polish`, skip Structural necessity and Domain specificity when the component has no product context, or when polish kept the current family ([polish.md](polish.md)).

## Distinctness check

Name Packet `first-character-costume=` when it exists. Point to one markup or CSS fact on the rendered surface (object, *join*, reading order, material, or interaction) that still kills that outfit after the wordmark is removed. `data-mass`, a utility class name, and a color token are not facts. Domain `2` requires that the category outfit fails in the DOM, not only in the Packet. QA accepts Distinctness only when that fact exists in the Implement `distinct=` block or can be pointed at in the DOM. Originality of *join* is not a rubric gate.

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
Distinctness=<costume and one visible rejection>
```

## Done

Every applicable criterion has a score and evidence, Distinctness names the costume and one DOM fact, and any P0 or threshold failure is in the QA table.
