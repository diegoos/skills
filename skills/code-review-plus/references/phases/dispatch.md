# Phase 2 — Dispatch

Dispatch five pipelines in parallel. Orchestrator reads this file to build prompts; each subagent receives exactly one perspective path.

## Dispatch

- Always: Correctness, Security, Architecture, Quality, Performance — **in parallel**
- No shared findings until Phase 2.5
- Pass: scope summary (compact) + exact perspective path
- Subagents assign no final P0–P3

## Perspective paths

| Pipeline     | Path                                        |
| ------------ | ------------------------------------------- |
| Correctness  | `./references/perspectives/correctness.md`  |
| Security     | `./references/perspectives/security.md`     |
| Architecture | `./references/perspectives/architecture.md` |
| Quality      | `./references/perspectives/quality.md`      |
| Performance  | `./references/perspectives/performance.md`  |

## Subagent prompt template

```txt
Review [files/diff] from the [PIPELINE] perspective only.

Context (from Phase 1):
[1-2 sentences: intent + what must NOT change]

Reference (read ONLY this file, then review code):
- [perspective path]

Before flagging anything (Pass A — hunter self-check):
- Read the entire cited file, not just the diff snippet.
- Read middleware / modules / utils / global layers before flagging individual routes.
- Trace the full pipeline to the final output, not one step in isolation.
- Read comments explaining intentional design before calling it a bug.
- Verify all consumers before calling code dead or redundant.
- Raise a candidate only when evidence_level is proven or likely (never speculative).
- Point to the exact line that makes the problem exploitable or broken TODAY.

Return CandidateFinding list (YAML or bullets):
- location: file:line
- pipeline: Correctness | Security | Architecture | Quality | Performance
- title: short title
- category_hint: vulnerability | hardening | maintainability
- exploit_or_break_path: why it breaks or is exploitable TODAY (concrete path)
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

## Completion criterion

Every dispatched pipeline has returned. Each candidate includes `location`, `exploit_or_break_path`, and `evidence_level` (`proven` or `likely`).
