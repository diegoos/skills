# Pipeline — Architecture

Hunt structural alignment, boundaries, and pattern consistency only.

## Hunt for

- Unbounded loops or unrestricted data fetches with structural impact
- Deviation from existing codebase patterns without justification
- Unclean module boundaries, circular dependencies
- Business logic in the wrong layer (controller/view/utility when the codebase places it elsewhere)
- Inappropriate abstraction level (premature or missing abstractions with concrete cost)
- Duplication that should be shared; coupling that should be loosened
- Wrong dependency direction
- Proposed fixes that would break documented intentional design

## Pass A reminders

- Architecture findings need a concrete boundary or pattern break visible **today**
- Prefer the codebase's existing patterns over ideal textbook structure
- `evidence_level` must be `proven` or `likely`
- Suggested fix: minimal and local; structural refactors carry high `regression_risk` — prefer follow-up unless breakage is demonstrable
