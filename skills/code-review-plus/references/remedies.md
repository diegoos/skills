# Structural remedies

When a finding is structural, name the move in `suggested_fix`. Prefer the smallest move that reduces the number of ideas a reader tracks in this file. Broad refactors → follow-up + high `regression_risk`.

## Named moves

- Replace a chain of conditionals with a typed model or explicit dispatcher
- Collapse duplicate branches into one clearer flow
- Separate orchestration from domain logic
- Move feature-specific logic out of a shared module into the owning package
- Reuse the canonical helper instead of a near-duplicate
- Make a type boundary explicit so downstream branching disappears
- Delete a pass-through wrapper that adds no API clarity
- Extract a helper or split a large file into focused modules

## Rules

- Name the remedy; do not only say "too complex"
- Match existing codebase patterns over textbook structure
- One local move beats a cross-cutting redesign unless breakage is demonstrable today
