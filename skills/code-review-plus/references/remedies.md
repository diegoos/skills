# Structural remedies

When a finding is structural, name the move in `suggested_fix`. Prefer the smallest move that reduces the number of ideas a reader tracks in this file. Broad refactors → follow-up + high `regression_risk`.

## Named moves

- Invert conditions and return early (guard clauses) so the happy path stays flat
- Replace a boolean soup with a named predicate (`isEligibleForRefund(order)`)
- Replace a chain of conditionals with a typed model or explicit dispatcher
- Collapse duplicate branches into one clearer flow
- Separate orchestration from domain logic
- Move feature-specific logic out of a shared module into the owning package
- Reuse the canonical helper instead of a near-duplicate
- Make a type boundary explicit so downstream branching disappears
- Delete a pass-through wrapper that adds no API clarity
- Extract a helper or split a large file into focused modules

## Rules

- Name the remedy; do not only say "too complex" or cite a score. Tie the keep to nesting or load today
- Prefer the smallest move: guard clauses, then extract with a responsibility name, then lookup/dispatcher, then named predicate. Polymorphism only when the same switch appears in 2+ places
- Match existing codebase patterns over textbook structure
- One local move beats a cross-cutting redesign unless breakage is demonstrable today
