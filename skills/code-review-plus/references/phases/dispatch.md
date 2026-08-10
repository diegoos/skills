# Phase 2 — Dispatch

Dispatch pipelines per Phase 1 tier. Orchestrator builds prompts; each hunter receives exactly one perspective and optionally one shape.

## Dispatch by tier

| Tier            | Pipelines to run                                                        | Shapes                                       |
| --------------- | ----------------------------------------------------------------------- | -------------------------------------------- |
| trivial         | Correctness + Quality (+ Security only per Scope rule)                  | None                                         |
| normal          | Correctness, Security, Architecture, Quality, Performance (in parallel) | None                                         |
| large/sensitive | All five (in parallel)                                                  | At most **1** shape per hunter if tags match |

- No shared findings until Phase 2.5
- Each prompt includes: scope summary (compact) + perspective path + optional shape path
- Hunters assign no final P0–P3

## Perspective paths

| Pipeline     | Path                                        |
| ------------ | ------------------------------------------- |
| Correctness  | `./references/perspectives/correctness.md`  |
| Security     | `./references/perspectives/security.md`     |
| Architecture | `./references/perspectives/architecture.md` |
| Quality      | `./references/perspectives/quality.md`      |
| Performance  | `./references/perspectives/performance.md`  |

## Shape selection (large/sensitive only)

Pick at most one shape for a hunter from Phase 1 stack tags:

| Tag | Path                                                |
| --- | --------------------------------------------------- |
| web | `./references/shapes/web.md`                        |
| api | `./references/shapes/api.md`                        |
| ts  | `./references/shapes/typescript-javascript-node.md` |
| py  | `./references/shapes/python.md`                     |
| go  | `./references/shapes/go.md`                         |
| rs  | `./references/shapes/rust.md`                       |

Count changed paths per tag. At most **one** shape per hunter:

1. **Security / Quality:** if `web` or `api` is present, pick the majority between those two; else pick the majority among language tags (`ts` \| `py` \| `go` \| `rs`).
2. **Correctness / Architecture / Performance:** pick the majority among language tags only; omit when none apply (do not attach `web`/`api`).
3. **Tie** on the eligible set → omit the shape.

## Subagent prompt template

```txt
Review [files/diff] from the [PIPELINE] perspective only.

Context (from Phase 1):
[context summary block]

Reference (read ONLY these paths, then review code):
- [perspective path]
- [shape path or omit this line]

Before flagging anything (Pass A — hunter self-check):
- Read the entire cited file, not just the diff snippet.
- Read middleware / modules / utils / global layers before flagging individual routes.
- Trace the full pipeline to the final output, not one step in isolation.
- Read comments explaining intentional design before calling it a bug.
- Verify all consumers before calling code dead or redundant.
- Raise a candidate only when evidence_level is proven or likely (never speculative).
- Point to the exact line that makes the problem exploitable or broken today.
- suggested_fix is minimal and local when possible; preserves error behavior and side effects; note regression_risk for callers / contracts / tests / what-must-not-change.

Return CandidateFinding list (YAML or bullets):
- location: file:line
- pipeline: Correctness | Security | Architecture | Quality | Performance
- title: short title
- category_hint: vulnerability | hardening | maintainability
- exploit_or_break_path: why it breaks or is exploitable today (concrete path)
- data_provenance: user | llm | backend | n/a
- evidence_level: proven | likely
- suggested_fix: minimal, local when possible
- regression_risk: callers / contracts / tests / what-must-not-change that the fix could touch

Do not open other files under references/. Do not review outside your pipeline.
Do not assign final P0/P1/P2/P3 severity.
```

## CandidateFinding schema

```yaml
location: path/file.ts:42
pipeline: Correctness
title: Unhandled JSON.parse crash
category_hint: vulnerability
exploit_or_break_path: Malformed HTTP body → JSON.parse throws → worker process exits
data_provenance: user
evidence_level: proven
suggested_fix: Wrap parse in try/catch; return 400
regression_risk: Error response shape for this route; existing happy-path tests
```

## Orchestrator-only refs (not hunter paths)

- If `package.json` / lockfile is in the review source, read `./references/dependency-review.md` during Phase 3 synthesize (after hunters return).
- Structural `suggested_fix` values may name a move from `./references/remedies.md` (orchestrator / Architecture / Quality authors may open it; hunters need not).

## Completion criterion

Every pipeline required by the tier has returned. Each candidate includes `location`, `exploit_or_break_path`, and `evidence_level` (`proven` or `likely`). Record which pipelines ran for the report summary.
