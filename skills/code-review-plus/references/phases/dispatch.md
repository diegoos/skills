# Phase 2 — Dispatch

Dispatch each name in Phase 1 `Pipelines`, one prompt per name. Orchestrator builds prompts; each hunter receives exactly one perspective and optionally one shape. Quality reads `./references/perspectives/quality.md`, which opens `make-code` when that skill is installed; the orchestrator does not detect it.

Same model as the orchestrator. Hunters return CandidateFinding lists. Project lint / complexity / test commands that do not write are allowed. One hunter per perspective.

## Contents

- [Hunt bar](#hunt-bar)
- [Serial fallback (no subagent)](#serial-fallback-no-subagent)
- [Perspective paths](#perspective-paths)
- [Shape selection](#shape-selection)
- [Subagent prompt template](#subagent-prompt-template)
- [CandidateFinding schema](#candidatefinding-schema)
- [Orchestrator-only refs (not hunter paths)](#orchestrator-only-refs-not-hunter-paths)
- [Completion criterion](#completion-criterion)

## Hunt bar

Cover the perspective (and shape) as a **floor** (Security's floor is its Method), then emit any other issue in this hunter's scope when **today**'s cost is pointable at `file:line`. When a hunter sees a clear issue whose owner is not in `Pipelines`, it reports the issue with `pipeline` set to that owner and does not hunt for more. With `Isolated: yes`, it reports only a P0/P1-level break. `likely` is allowed at hunt time; **Pass B** confirms. P0/P1 require **proven**. An empty list is valid when this hunter found nothing.

## Serial fallback (no subagent)

If the harness has no subagent, run the names **in series** (one perspective at a time). Record `serial: yes` in persist Notes only when **two or more** pipelines ran in series. One hunter: omit `serial:`.

**Carry list.** After each pipeline returns, append each candidate's `location`, `title`, and `pipeline` (Quality also `quality_source`). A pipeline with no candidates still records `pipeline: … (none)` (Quality: also `quality_source`). Restate that compact list before starting the next pipeline. Auto-compact drops earlier hunts: restore from that restated list first, then continue. Mid-series with no restated block for a finished pipeline is a failed dispatch; rebuild from the last restated block before the next hunt.

Carry is orchestrator storage. The next hunter still receives only its own perspective (prompt template below). Deduplicate in Phase 3.

Prompt rules:

- No shared findings until Phase 2.5 (serial carry list is orchestrator memory, not hunter input)
- Each prompt includes: scope summary (compact; leave out `Save`, `Prior findings`, and `Closed paths`) + perspective path + optional shape path
- Quality also receives `./references/test-quality.md` when Quality is in `Pipelines` and Phase 1 marked **tests in source**
- Quality prompt includes the Quality bar block below; other hunters omit it
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
| ts  | `./references/shapes/typescript-javascript-node.md` |
| py  | `./references/shapes/python.md`                     |
| go  | `./references/shapes/go.md`                         |
| rs  | `./references/shapes/rust.md`                       |
| llm | `./references/shapes/llm.md`                        |

### Tier `trivial`

Omit shapes.

### Tiers `normal` and `large/sensitive` (priority)

Count changed paths (or lines on a language tie). At most **one** shape per hunter:

1. **Security:** `llm` if that tag is present. Otherwise omit.
2. **Quality / Correctness / Architecture / Performance:** language tags only (`ts` \| `py` \| `go` \| `rs`). Majority of changed paths. If two languages tie, pick the one with more changed lines. Omit when none apply. `llm` stays off.

## Subagent prompt template

```txt
Review [files/diff] from the [PIPELINE] perspective only.

Context (from Phase 1):
[context summary block]

Reference (read these skill paths, then the changed hunks, callees, and enough of each file to prove or drop):
- [perspective path — omit this line for Quality]
- [shape path or omit this line]
- [Quality + tests in source only: ./references/test-quality.md]

[Quality only — paste this block; omit for other hunters]
Quality bar: READ ./references/perspectives/quality.md and follow it. It opens the make-code skill when that skill is in this environment; otherwise it hunts its default Floor. Hunt (no Apply, Prove, or edit).
For **CC**, use the cap that the Floor you hunt names (**20** on new or rewritten functions unless the project sets another bar).
Always cover: the Floor; docs sync when Documentable surface is yes; dead code after a full consumer search; test-quality.md when that path is in this prompt; plus any other quality cost in this diff with today's pointable line.
Return quality_source: make-code | slim-fallback with the candidate list.

Cover the **floor**. Also emit other issues in this hunter's scope when today's cost is pointable at file:line. A clear issue whose owner hunter is not in Pipelines: report it with pipeline set to that owner; do not hunt for more. Isolated: yes → only a P0/P1-level break. An empty list is valid when this hunter found nothing.
suggested_fix is minimal and local when possible. regression_risk names each caller, contract, or test the fix can break, or none after you checked.

Return CandidateFinding list (YAML or bullets):
- location: file:line
- pipeline: Correctness | Security | Architecture | Quality | Performance
- title: short title
- category_hint: vulnerability | bug | hardening | maintainability
- exploit_or_break_path: why it breaks, is exploitable, or costs today (concrete path)
- data_provenance: user | llm | backend | n/a
- evidence_level: proven | likely
- suggested_fix: minimal, local when possible
- regression_risk: callers / contracts / tests / what-must-not-change that the fix could touch
- [Quality only] quality_source: make-code | slim-fallback

From this skill, read only the paths listed above. Read any project file you need (code, docs, AGENTS.md, security notes).
Leave P0–P3 to synthesize.
Review is read-only. Same model as the orchestrator.
```

On `Mode: delta`, hunt hunks since the prior HEAD. Skip listed `file:line` unless that path's behavior changed. Check each `Fix risks` entry in this hunter's scope, even outside those hunks.

## CandidateFinding schema

```yaml
location: path/file.ts:42
pipeline: Correctness
title: Unhandled JSON.parse crash
category_hint: bug
exploit_or_break_path: Malformed HTTP body → JSON.parse throws → worker process exits
data_provenance: user
evidence_level: proven
suggested_fix: Wrap parse in try/catch; return 400
regression_risk: Error response shape for this route; existing happy-path tests
```

## Orchestrator-only refs (not hunter paths)

Hunters receive only the prompt template paths (Quality also may open `make-code` from the environment). Open these in the named phase:

- `./references/dependency-review.md` during Phase 3 when Phase 1 marked lockfile in source (gate in synthesize.md)
- `./references/remedies.md` during Phase 3 when a kept finding is structural. Name the move from that file on `suggested_fix`
- `./references/complexity.md` during Phase 2.5 when a candidate is about branching, nesting, a complexity score, or YAGNI
- `./references/examples/*` during Pass B doubt, optional eval notes, or report sample
- `./references/phases/persist.md` during Phase 4.5
- `./references/phases/knowns.md` when the user dismisses a finding

## Completion criterion

Every name in Phase 1 `Pipelines` has returned (an empty CandidateFinding list is valid when that pipeline found nothing). Each candidate includes `location`, `exploit_or_break_path`, and `evidence_level` (`proven` or `likely`). When Quality ran, the return includes `quality_source: make-code | slim-fallback`. Record which pipelines ran and which shapes were attached for the report summary. Serial fallback with two or more pipelines: the compact carry list holds every finished pipeline before the next hunt starts.
