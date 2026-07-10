# API contract

> Cut this file if the project does not expose an API.

**Protocol:** <REST | GraphQL | gRPC | RPC | WebSocket | …>
**Base URL / address:** `<scheme>://host/path or host:port`
**Auth:** <mechanism and where credentials appear>
**Versioning:** <path | header | package; breaking-change policy>

## Endpoints / methods

| Resource | Method | Path / RPC | Description |
| -------- | ------ | ---------- | ----------- |
| Orders | GET | `/v1/orders` | List orders |
| Orders | POST | `/v1/orders` | Place order |

## Error format

```json
{ "error": { "code": "...", "message": "..." } }
```
