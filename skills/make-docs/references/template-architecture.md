> How the system is structured. Draw what the code earns; cut the rest.

## Overview

**Purpose:** <what the system does in one sentence>
**Stack:** <languages, frameworks, runtimes>
**Entry points:** <CLI, HTTP server, worker, library API, …>

## Structural views

> C4 context (system + actors + external systems), container (separately > deployable units), and component (only where internals are load-bearing).
> Code is the source of truth — diagrams summarize, they do not invent.
> Draw each as a Mermaid graph. Example container view:

```mermaid
graph LR
  subgraph <system>
    App[Application]
    API[API]
    DB[(Database)]
    Worker[Worker]
  end
  Client[Client] --> App
  App --> API
  API --> DB
  API --> Worker
```

## Dependency rule

> Only when the codebase uses layered architecture with dependency inversion > (Clean/Hexagonal). Otherwise cut this entire section.

Dependencies point inward toward the domain. The seam sits between adapters and use cases (dependency inversion).

- Domain → depends on nothing inward
- Use cases → depend on domain ports
- Adapters → implement ports, depend outward on drivers and frameworks
- Frameworks → outermost

## Runtime view

> Key flows as Mermaid sequence diagrams. Trace the full round-trip for each > load-bearing path (request, job, event, command).

## Deployment view

> Where containers and processes run. Mermaid graph: hosts, networks, stores, > and how artifacts reach production.

## State

**Owned state:** <what this system persists or caches>
**External state:** <what it reads from other systems>
**Ephemeral state:** <in-memory, session, queue buffers>
**Synchronization:** <how consistency is maintained across boundaries>

## Auth

> Cut if the system has no authentication or authorization.

**Mechanism:** <tokens | sessions | mTLS | API keys | IAM roles | …>
**Flow:** <how identity is established and checked; credential lifecycle>
