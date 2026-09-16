# Phase 2 — Dispatch

Dispatch each name in Phase 1 `Pipelines`. Orchestrator builds prompts; each hunter receives exactly one perspective and optionally one shape. Quality chooses `make-code` or `quality.md` from the prompt; the orchestrator does not detect which skill is installed.

Same model as the orchestrator. Hunters return CandidateFinding lists. Project lint / complexity / test commands that do not write are allowed. One hunter per perspective. **silence** is success; an empty list is valid.

## Serial fallback (no subagent)

If the harness has no subagent, run the names **in series** (one perspective at a time). Record `serial: yes` in persist Notes only when **two or more** pipelines ran in series. One hunter: omit `serial:`.

**Carry list.** After each pipeline returns, append `location`, `title`, and `pipeline` (Quality also `quality_source`) to a running carry list. Restate that compact list before starting the next pipeline. Auto-compact drops earlier hunts: restore from that restated list first, then continue. Mid-series with an empty carry list is a failed dispatch; rebuild from the last restated block before the next hunt.

Carry is orchestrator storage. The next hunter still receives only its own perspective (prompt template below). Deduplicate in Phase 2.5.

Run each name in Phase 1 `Pipelines` (one prompt per name).

- No shared findings until Phase 2.5 (serial carry list is orchestrator memory, not hunter input)
- Each prompt includes: scope summary (compact) + perspective path + optional shape path
- Quality also receives `./references/test-quality.md` when Quality is in `Pipelines` and Phase 1 marked **tests in source**
- Quality prompt includes the Quality bar block below; other hunters omit it
- Hunters assign no final P0–P3
- Report which shapes were attached (for the report `shapes:` line), including on `normal`

## Perspective paths

| Pipeline     | Path                                        |
| ------------ | ------------------------------------------- |
| Correctness  | `./references/perspectives/correctness.md`  |
| Security     | `./references/perspectives/security.md`     |
| Architecture | `./references/perspectives/architecture.md` |
| Quality      | hunter chooses (Quality bar)                |
| Performance  | `./references/perspectives/performance.md`  |

Quality fallback path (named in the Quality bar, not auto-opened by the orchestrator): `./references/perspectives/quality.md`.

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

1. **Security / Quality:** `llm` if that tag is present, else the majority language tag (`ts` \| `py` \| `go` \| `rs`). Omit when none apply. Do **not** attach `web` or `api` (the Security perspective already hunts that surface).
2. **Correctness / Architecture / Performance:** language tags only (`ts` \| `py` \| `go` \| `rs`). Majority of changed paths. If two languages tie, pick the one with more changed lines. Omit when none apply. Do **not** attach `web`, `api`, or `llm`.

## Subagent prompt template

```txt
Review [files/diff] from the [PIPELINE] perspective only.

Context (from Phase 1):
[context summary block]

Reference (read ONLY these paths, then the changed hunks and callees; the whole file only when the path requires it):
- [perspective path — omit this line for Quality]
- [shape path or omit this line]
- [Quality + tests in source only: ./references/test-quality.md]

[Quality only — paste this block; omit for other hunters]
Quality bar: if the make-code skill is available in this environment, READ it and hunt its Floor on this diff (KISS, DRY, YAGNI, Match, Balance). For **CC**, use this skill's review cap **20** on new or rewritten functions (or the project's bar), not make-code's write cap. Do not Apply, Prove, or edit.
Else READ ./references/perspectives/quality.md and hunt that Floor (CC cap **20** unless the project sets another bar).
Read exactly one. Return quality_source: make-code | slim-fallback with the candidate list.

Emit a candidate when the break, exploit, or today's quality cost is proven with file:line. Empty list is success.
suggested_fix is local; regression_risk is one line.

Return CandidateFinding list (YAML or bullets):
- location: file:line
- pipeline: Correctness | Security | Architecture | Quality | Performance
- title: short title
- category_hint: vulnerability | hardening | maintainability
- exploit_or_break_path: why it breaks, is exploitable, or costs today (concrete path)
- data_provenance: user | llm | backend | n/a
- evidence_level: proven | likely
- suggested_fix: minimal, local when possible
- regression_risk: callers / contracts / tests / what-must-not-change that the fix could touch
- [Quality only] quality_source: make-code | slim-fallback

Do not open other files under references/. Do not review outside your pipeline.
Do not assign final P0/P1/P2/P3 severity.
No writes to the reviewed repo. Same model as the orchestrator.
```

On `Mode: delta`, hunt hunks since the prior HEAD. Skip listed `file:line` unless that path's behavior changed.

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

Hunters receive only the prompt template paths (Quality also may open `make-code` from the environment). Open these in the named phase:

- `./references/dependency-review.md` during Phase 3 (gate in synthesize.md)
- `./references/remedies.md` during Phase 3 when a kept finding is structural. Name the move from that file on `suggested_fix`
- `./references/complexity.md` during Phase 2.5 when a candidate is about branching, nesting, a complexity score, or YAGNI
- `./references/examples/*` during validator doubt, optional eval notes, or report sample
- `./references/phases/persist.md` during Phase 4.5
- `./references/phases/knowns.md` when the user dismisses a finding

Quality extra path (not orchestrator-only): `./references/test-quality.md` when Quality is in `Pipelines` and tests are in the review source.

## Completion criterion

Every name in Phase 1 `Pipelines` has returned (an empty CandidateFinding list is valid). Each candidate includes `location`, `exploit_or_break_path`, and `evidence_level` (`proven` or `likely`). When Quality ran, the return includes `quality_source: make-code | slim-fallback`. Record which pipelines ran and which shapes were attached for the report summary. Serial fallback with two or more pipelines: the compact carry list holds every finished pipeline before the next hunt starts.
