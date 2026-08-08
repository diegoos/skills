# Shape — API (PR review)

Hunt HTTP/API surface issues. Not a full threat model; deeper pass → `/deep-security-review`.

## Hunt for

- Authz missing on sensitive routes (check global middleware first)
- Input validation at the boundary (body, query, path) before use in logic or queries
- Pagination or hard limits missing on list endpoints that can return unbounded sets
- Error responses that leak internals (stack traces, SQL, paths) to clients
- Mass assignment / unexpected fields accepted into privileged updates

## Pass A

- Hardening (future caller) stays category hardening
- Suggested fix stays local to the route or shared validator already in the codebase
