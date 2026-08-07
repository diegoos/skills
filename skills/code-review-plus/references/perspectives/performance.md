# Pipeline — Performance

Hunt hot-path cost, unbounded work, and UI churn only.

For profiling guidance, use `performance-optimization` when available.

## Hunt for

- N+1 queries, missing indexes, unbounded loops or data fetches
- Synchronous operations that should be async
- Unnecessary re-renders in UI components
- Missing pagination on list endpoints
- Large object creation in critical paths
- N instances with N listeners is optimization, not a leak, when cleanup exists

## Pass A reminders

- Prefer demonstrated hot paths or clear production-scale breakage over theoretical cost
- `evidence_level` must be `proven` or `likely`
- Suggested fix: minimal and local; note `regression_risk` for caching semantics and pagination contracts
