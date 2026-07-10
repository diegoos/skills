# Constraints

> Numbers and policies the system must meet. Cut any section the survey did
> not earn. Prefer measurable targets over adjectives.

## Runtime

| Target | Baseline |
| ------ | -------- |
| Language / runtime | <e.g. Go 1.22+, Node 20+, JVM 21> |
| Platforms | <OS, arch, container base> |

## Performance

| Metric | Target | Condition |
| ------ | ------ | --------- |
| Latency | <e.g. p99 < 200ms> | <load, endpoint or path> |
| Throughput | <e.g. 1000 RPS> | <hardware / env> |

## Security

| Policy | Value |
| ------ | ----- |
| Transport | <e.g. TLS 1.2+ required> |
| Secrets | <e.g. env / secret manager; never in repo> |
| Authn / Authz | <mechanism and enforcement point> |

## Resource budget

| Resource | Budget |
| -------- | ------ |
| Memory | <e.g. < 512 MB RSS> |
| CPU | <e.g. 1 vCPU steady> |
| Artifact size | <e.g. container < 150 MB> |

## Technical

> Cut any rule the survey did not earn. Examples only — replace with what
> the codebase actually enforces:

- <e.g. parameterized queries; no string-built SQL>
- <e.g. secrets via env / secret manager; `.env.example` checked in, never `.env`>

## Quality goals

| Goal | Scenario | Target |
| ---- | -------- | ------ |
| Availability | Rolling 30-day window | 99.9% |
| Durability | <e.g. acknowledged writes> | <target> |
