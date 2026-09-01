# Pipeline — Correctness

Hunt logical errors, edge cases, and type issues.

## Hunt for

- Off-by-one errors, null/undefined access, race conditions, state inconsistencies
- Unhandled error cases, missing return statements, swallowed errors
- Error contracts: wrong status, empty catch, or success path when the operation failed
- Idempotency gaps on retries for side-effecting operations that claim to be safe to retry
- Incorrect logic (wrong operator, inverted condition, missing edge case)
- Type mismatches or unsafe coercions
- Spec mismatch: does the code match the stated behavior? Are error flows handled?
- Missing tests for a behavior change in this diff (trivial getter/reexport earns none). Use Phase 1 `Tests observed`. Quality does not emit this.
- Framework behavior: verify before asserting (e.g. does this API throw or return `{ data, error }`?)

## Pass A reminders

- Note `regression_risk` for callers and error contracts
- Suggested fix preserves error paths
