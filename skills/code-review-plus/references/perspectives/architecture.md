# Pipeline — Architecture

Hunt structural alignment, boundaries, and pattern consistency.

Name the structural move in `suggested_fix` when the finding is structural (guard clauses, dispatcher, extract, collapse branches, move feature logic out of a shared module, delete a pass-through wrapper).

## Hunt for

- Unbounded loops or unrestricted data fetches with structural impact
- Deviation from existing codebase patterns without justification
- Unclean module boundaries, circular dependencies, wrong dependency direction
- Business logic in the wrong layer (controller/view/utility when the codebase places it elsewhere)
- Refactor that relocates complexity without reducing the concepts a reader must hold
- Feature logic leaking into a shared module; near-duplicate of an existing canonical helper
- Fragile type boundaries (`any` / unchecked cast / silent fallback) that hide an unclear invariant today
- Two overlapping types/functions/constants in the diff with a concrete cost to keep both
- Compat path, alias, or shape that exists only on this branch and never shipped; confirm against main/release before proposing removal
- Inappropriate abstraction level (premature or missing abstractions with concrete cost)
- Proposed fixes that would break documented intentional design

## Pass A reminders

- Architecture findings need a concrete boundary or pattern break visible today
- Prefer the codebase's existing patterns over ideal textbook structure
- Broad refactors → high `regression_risk` / follow-up
