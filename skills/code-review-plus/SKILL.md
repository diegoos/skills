---
name: code-review-plus
description: >-
  Multi-perspective code review with parallel subagents, adaptive pipeline tiers, optional stack shapes (including llm; shapes on normal when the stack is a single obvious tag), optional P0 verifier, and a prioritized P0–P3 report. Branches: review (default), fix / apply / implement (apply findings without regressions). Invoke by name only (e.g. /code-review-plus, /code-review-plus fix).
disable-model-invocation: true
metadata:
  version: 0.4.1
  author: "Diego Oliveira"
  tags:
    - code
    - code review
    - security review
    - pr
    - review
---

# Code Review Plus

**Branches:** review (default) → parallel pipelines → double verify → synthesize → report. Fix branch applies findings with a **regression gate**.

**Invariants:** Each pipeline runs as a separate hunter (subagent). Every finding is reproducible from the code. Keep only `proven` or `likely` issues with a pointable line today. Prefer a minimal local fix over a broad refactor.

**Reference budget:** The orchestrator selects paths; never preload `references/`. Each hunter gets exactly **1** perspective plus **0 or 1** shape (`≤2` paths). Orchestrator-only refs (`dependency-review`, `remedies`, `examples`) are not hunter paths.

## Commands

| Invocation                    | Branch     | Behavior                          |
| ----------------------------- | ---------- | --------------------------------- |
| `/code-review-plus`           | **review** | Phases 1→4 only                   |
| `/code-review-plus fix`       | **fix**    | `./references/phases/fix.md` only |
| `/code-review-plus apply`     | **fix**    | Alias of `fix`                    |
| `/code-review-plus implement` | **fix**    | Alias of `fix`                    |

`fix`, `apply`, and `implement` are synonyms. Without a subcommand, never open `fix.md`. The fix branch never re-dispatches review pipelines.

## Definition of Done

### Branch review

| Phase        | Done when                                                                                   | READ                                |
| ------------ | ------------------------------------------------------------------------------------------- | ----------------------------------- |
| 1 Scope      | Scope + intent + tier + stack tags + context summary ready                                  | `./references/phases/scope.md`      |
| 2 Dispatch   | Tier pipelines returned candidates; shapes recorded when attached                           | `./references/phases/dispatch.md`   |
| 2.5 Verify   | Every candidate has kept/dropped/downgraded + note; optional P0 verifier applied or skipped | `./references/phases/verify.md`     |
| 3 Synthesize | Surviving findings have required fields + severity                                          | `./references/phases/synthesize.md` |
| 4 Report     | Skeleton fill of `report.md` (Findings Overview pipe table + verdict + drop counts)         | `./references/templates/report.md`  |

Do not open a later phase file until the current phase completion criterion is met.

### Branch fix (`fix` \| `apply` \| `implement`)

| Phase | Done when                                                   | READ                         |
| ----- | ----------------------------------------------------------- | ---------------------------- |
| Fix   | Findings applied or deferred without new demonstrable P0/P1 | `./references/phases/fix.md` |

Prerequisite: a prior report in this conversation (or an explicit finding list). If missing, ask; do not invent findings.

## Branch review — phases

### Phase 1 — Scope

**READ:** `./references/phases/scope.md`

**Completion criterion:** Scope answers written; review source, tier, and stack tags identified; context summary ready.

### Phase 2 — Dispatch

**READ:** `./references/phases/dispatch.md`

**Completion criterion:** Every dispatched pipeline returned; each candidate has `file:line`, `exploit_or_break_path`, and `evidence_level`.

### Phase 2.5 — Double verify

**READ:** `./references/phases/verify.md`

**Completion criterion:** Every candidate has status + `verification_note`; drop/downgrade counts recorded; optional P0 verifier ran or skipped per its triggers.

### Phase 3 — Synthesize

**READ:** `./references/phases/synthesize.md`

**Completion criterion:** Every surviving finding has all required fields; P2/P3 capped per calibration.

### Phase 4 — Report

**READ:** `./references/templates/report.md`

**Completion criterion:** User-facing reply is a skeleton fill of that template — English heading strings, Findings Overview as a Markdown pipe table (`ID | Severity | Category | Perspective | File | Issue`), verdict, pipelines line (shapes when used), verified-vs-dropped counts, and explicit unverified claims. Zero kept findings is valid (state that nothing was found; table header only).

## Branch fix

**READ:** `./references/phases/fix.md`

**Completion criterion:** Every targeted finding is closed (gate passed) or explicitly deferred. No new demonstrable P0/P1 left by the fixes.

## Rules

- Orchestrator opens phase/template files only when that phase or branch starts
- Hunters open only their assigned perspective and optional shape (`≤2` paths)
- File:line required; concrete break/exploit path for every P0/P1
- Clarity findings measure comprehension speed; a valid fix preserves behavior and error paths
- Preference without a codebase inconsistency → skip (not a finding)
- Report secrets as `file:line` + secret type only; redact values in the report and in fixes
- When verification yields zero kept findings, say so and Approve — Findings Overview keeps header + separator only; skip empty severity sections; do not fabricate issues to fill the report
- Phase 4 deliverable is a skeleton fill of `report.md`: keep its English headings; Findings Overview is always the six-column pipe table (detail sections expand rows, they do not replace the table); translate prose inside sections when the user language differs
- Ask before deleting dead code; never recommend blind removal
- State unverified claims explicitly
- Verdict needs evidence; do not soften a verified bug
- Optional P0 verifier: at most one subagent after Pass B; never reopens the five pipelines; does not assign final severity

## Relation to `deep-security-review`

Both skills are user-invoked. Use this skill for multi-perspective PR/diff review (optional stack shapes, including `llm`). Use `/deep-security-review` when security is the primary goal. Do not run both Security perspectives on the same scope in parallel; that skill replaces this skill's shallow security pass. Tell the user to invoke it; do not auto-start it.
