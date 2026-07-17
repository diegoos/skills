# Patterns

> Architectural or design patterns the code actually uses. Problem, where, > cost — skip patterns that are only aspirational.

| Pattern | Problem | Where | Cost |
| ------- | ------- | ----- | ---- |
| Hexagonal | Isolate domain from drivers. | `internal/` | Port boilerplate. |
| Outbox | Reliable publish after commit. | `pkg/outbox/` | Extra storage + poller. |
