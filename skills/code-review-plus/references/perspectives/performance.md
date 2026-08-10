# Pipeline — Performance

Hunt hot-path cost, unbounded work, and UI churn.

For profiling guidance, use `performance-optimization` when available.

## Hunt for

- N+1 queries, missing indexes, unbounded loops or data fetches, only with a demonstrated hot path or clear production-scale path
- Synchronous operations that should be async on a critical path
- Unnecessary re-renders or render churn in UI components
- Missing pagination on list endpoints
- Large object creation in critical paths
- N instances with N listeners is optimization, not a leak, when cleanup exists

## Pass A reminders

- Prefer demonstrated hot paths or clear production-scale breakage over theoretical cost
- Note `regression_risk` for caching semantics and pagination contracts
