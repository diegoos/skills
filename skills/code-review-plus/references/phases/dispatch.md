# Phase 2 — Dispatch

Dispatch pipelines per Phase 1 tier. Orchestrator builds prompts; each hunter receives exactly one perspective and optionally one shape.

Same model as the orchestrator. Read-only. One hunter per perspective.

## Serial fallback (no subagent)

If the harness has no subagent, run the tier's pipelines **in series** (one perspective at a time). Record `serial: yes` under Verification.

**Carry list.** After each pipeline returns, append its CandidateFinding list to a running carry list (YAML or bullets). Restate the **full** carry list (every pipeline finished so far, including the one just completed) before starting the next pipeline. Auto-compact drops earlier hunts: restore from that restated list first, then continue. Mid-series with an empty carry list is a failed dispatch; rebuild from the last restated block before the next hunt.

Carry is orchestrator storage. The next hunter still receives only its own perspective (prompt template below). Deduplicate in Phase 2.5.

## Dispatch by tier

| Tier            | Pipelines to run                                                        | Shapes                                              |
| --------------- | ----------------------------------------------------------------------- | --------------------------------------------------- |
| trivial         | Correctness + Quality (+ Security only per Scope rule)                  | None                                                |
| normal          | Correctness, Security, Architecture, Quality, Performance (in parallel) | At most **1** per hunter (priority below)           |
| large/sensitive | All five (in parallel)                                                  | At most **1** per hunter (same as `normal`)         |

- No shared findings until Phase 2.5 (serial carry list is orchestrator memory, not hunter input)
- Each prompt includes: scope summary (compact) + perspective path + optional shape path
- Quality also receives `./references/test-quality.md` when Phase 1 marked **tests in source**
- Hunters assign no final P0–P3
- Report which shapes were attached (for the report `shapes:` line), including on `normal`

## Perspective paths

| Pipeline     | Path                                        |
| ------------ | ------------------------------------------- |
| Correctness  | `./references/perspectives/correctness.md`  |
| Security     | `./references/perspectives/security.md`     |
| Architecture | `./references/perspectives/architecture.md` |
| Quality      | `./references/perspectives/quality.md`      |
| Performance  | `./references/perspectives/performance.md`  |

## Shape selection

Pick at most one shape for a hunter from Phase 1 stack tags:

| Tag | Path                                                |
| --- | --------------------------------------------------- |
| web | `./references/shapes/web.md`                        |
| api | `./references/shapes/api.md`                        |
| ts  | `./references/shapes/typescript-javascript-node.md` |
| py  | `./references/shapes/python.md`                     |
| go  | `./references/shapes/go.md`                         |
| rs  | `./references/shapes/rust.md`                       |
| llm | `./references/shapes/llm.md`                        |

### Tier `trivial`

Omit shapes.

### Tiers `normal` and `large/sensitive` (priority)

Count changed paths (or lines on a language tie). At most **one** shape per hunter:

1. **Security / Quality:** `llm` if that tag is present, else `web`, else `api`, else the majority language tag (`ts` \| `py` \| `go` \| `rs`). Omit when none apply.
2. **Correctness / Architecture / Performance:** language tags only (`ts` \| `py` \| `go` \| `rs`). Majority of changed paths. If two languages tie, pick the one with more changed lines. Omit when none apply. Do **not** attach `web`, `api`, or `llm`.

## Subagent prompt template

```txt
Review [files/diff] from the [PIPELINE] perspective only.

Context (from Phase 1):
[context summary block]

Reference (read ONLY these paths, then review code):
- [perspective path]
- [shape path or omit this line]
- [Quality + tests in source only: ./references/test-quality.md]

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
Read-only. Same model as the orchestrator.
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
- `./references/examples/*` are orchestrator-only (Pass B doubt, optional eval notes, report sample). Never give them to hunters.
- `./references/phases/persist.md` is orchestrator-only (Phase 4.5). Never give it to hunters.
- `./references/phases/knowns.md` is orchestrator-only (user dismiss). Never give it to hunters.

Quality extra path (not orchestrator-only): `./references/test-quality.md` when tests are in the review source.

## Completion criterion

Every pipeline required by the tier has returned. Each candidate includes `location`, `exploit_or_break_path`, and `evidence_level` (`proven` or `likely`). Record which pipelines ran and which shapes were attached for the report summary. Serial fallback: the carry list holds every CandidateFinding from finished pipelines (including the current one) before the next hunt starts.
