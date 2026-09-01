# Constraints

> Example rows are not defaults. Replace every placeholder from evidence, or cut the row or section.
> Numbers and policies the system must meet. Cut any section the survey did not earn. Prefer measurable targets over adjectives. A number lands only when config, a test, or a comment states it.

## Runtime

| Target | Baseline |
| ------ | -------- |
| Language / runtime | `{from go.mod / package.json / similar}` |
| Platforms | `{OS, arch, container base from this repo}` |

## Performance

| Metric | Target | Condition |
| ------ | ------ | --------- |
| `{metric named in this repo}` | `{number from config, test, or comment}` | `{load, endpoint or path}` |

Cut this section when no metric has a source.

## Security

| Policy | Value |
| ------ | ----- |
| Transport | `{what this repo enforces}` |
| Secrets | `{what this repo enforces}` |
| Authn / Authz | `{mechanism and enforcement point, or cut row}` |

## Resource budget

| Resource | Budget |
| -------- | ------ |
| Memory | `{limit from Dockerfile, compose, or similar; else cut}` |
| CPU | `{limit from this repo; else cut}` |
| Artifact size | `{limit from this repo; else cut}` |

Cut this section when no budget is stated.

## Technical

> Cut any rule the survey did not earn. Replace with what the codebase actually enforces.

- `{rule with a path that enforces it}`

## Quality goals

| Goal | Scenario | Target |
| ---- | -------- | ------ |
| `{goal named in this repo}` | `{window or condition from this repo}` | `{number from this repo}` |

Cut this section when no quality target has a source.
