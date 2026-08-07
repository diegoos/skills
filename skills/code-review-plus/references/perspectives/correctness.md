# Pipeline — Correctness

Hunt logical errors, edge cases, and type issues only.

## Hunt for

- Off-by-one errors, null/undefined access, race conditions, state inconsistencies
- Unhandled error cases, missing return statements, swallowed errors
- Incorrect logic (wrong operator, inverted condition, missing edge case)
- Type mismatches or unsafe coercions
- Spec mismatch: does the code match the stated behavior? Are error flows handled?
- Framework behavior: verify before asserting (e.g. does this API throw or return `{ data, error }`?)

## Pass A reminders

- Point to the exact line that breaks **today**
- `evidence_level` must be `proven` or `likely`
- Suggested fix: minimal and local; note `regression_risk` for callers and error contracts
