# API contract

> Example rows are not defaults. Replace every placeholder from evidence, or cut the row or section.
> Cut this file if the project does not expose an API.

**Protocol:** {REST | GraphQL | gRPC | RPC | WebSocket; from this tree}
**Base URL / address:** `{scheme}://host/path or host:port from config or help text`
**Auth:** {mechanism and where credentials appear}
**Versioning:** {path | header | package; breaking-change policy if documented}

## Endpoints / methods

| Resource | Method | Path / RPC | Description |
| -------- | ------ | ---------- | ----------- |
| `{resource from this API}` | `{METHOD}` | `{path or RPC from this tree}` | `{observable}` |

## Error format

> Paste the error body this API actually returns. Cut this section when there is no shared error shape.

```json
{ "error": { "code": "...", "message": "..." } }
```
