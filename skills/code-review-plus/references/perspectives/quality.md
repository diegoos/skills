# Pipeline — Quality

Hunt readability, naming, complexity, dead code, and tool violations only.

## Hunt for

- Descriptive, consistent naming (avoid `temp`, `data`, `result` without context)
- Straightforward control flow (deep nesting, nested ternaries)
- Functions doing too many things (>30 lines is a smell, not a rule)
- Unnecessary complexity, "clever" tricks
- Abstractions justified by actual reuse (do not generalize before a third use case)
- Comments only for non-obvious business logic — not for self-explanatory code
- Project test, lint, typecheck, and format rules — if present, run them and report violations

## Dead code / redundancy

- Before calling code dead or redundant, confirm **all consumers** — including alternate routes, library-internal fetches, and defensive helpers that handle raw envelopes outside the main helper
- "Redundant" functions are often small security validations — verify before proposing removal
- List candidates and ask; never suggest blind deletion

## Pass A reminders

- Style-only prefs without consistency or clarity win are not candidates
- `evidence_level` must be `proven` or `likely`
- Suggested fix: minimal and local; note `regression_risk` for public names and shared helpers
