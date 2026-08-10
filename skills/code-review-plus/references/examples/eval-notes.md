# Eval notes (optional calibration)

Orchestrator-only pattern. Do not preload during review. Do not give this path to hunters. Do not write this file into the reviewed target repository unless the user asks.

Use after the report when the user wants calibration feedback. Fill in the conversation (or a file they request).

```txt
## code-review-plus eval notes

Candidates: N total → kept: … / dropped: … / downgraded: …
Pipelines: …
Tier: trivial | normal | large/sensitive
Shapes: … | none
P0 verifier: ran | skipped (reason: …)

False positive that survived Pass B? (one line or "none")
True positive wrongly dropped/downgraded? (one line or "none")
```

No CI, harness, or scripts. Counts and one-line miss notes are enough.
