---
name: code-review-plus
description: >-
  Multi-perspective code review with parallel subagents and a prioritized P0–P3 report. Branches: review (default), fix / apply / implement (apply findings without regressions). Invoke by name only (e.g. /code-review-plus, /code-review-plus fix).
disable-model-invocation: true
metadata:
  version: 0.2.0
  author: "Diego Oliveira"
  tags:
    - code
    - code review
    - security review
    - pr
    - review
---

# Code Review Plus

**Branches:** review (default) → parallel pipelines → **double verify** → synthesize → report. Fix branch applies findings with a **regression gate**.

**Invariants:** Each pipeline runs as a separate subagent. Every finding must be reproducible by reading the code. Keep only proven/likely issues with a pointable line **today**. Prefer minimal local fixes over broad refactors.

**Reference budget:** The orchestrator selects paths; subagents read them. Never preload `references/`. Each review subagent gets exactly **1** perspective file.

## Commands

| Invocation                    | Branch     | Behavior                          |
| ----------------------------- | ---------- | --------------------------------- |
| `/code-review-plus`           | **review** | Phases 1→4 only                   |
| `/code-review-plus fix`       | **fix**    | `./references/phases/fix.md` only |
| `/code-review-plus apply`     | **fix**    | Alias of `fix`                    |
| `/code-review-plus implement` | **fix**    | Alias of `fix`                    |

`fix`, `apply`, and `implement` are synonyms. Without a subcommand, never open `fix.md`. The fix branch never re-dispatches the five pipelines.

## Definition of Done

### Branch review

| Phase        | Done when                                                      | READ                                |
| ------------ | -------------------------------------------------------------- | ----------------------------------- |
| 1 Scope      | Scope + intent + what-must-not-change answered                 | `./references/phases/scope.md`      |
| 2 Dispatch   | Five subagents returned candidates                             | `./references/phases/dispatch.md`   |
| 2.5 Verify   | Every candidate has `kept` \| `dropped` \| `downgraded` + note | `./references/phases/verify.md`     |
| 3 Synthesize | Surviving findings have required fields + severity             | `./references/phases/synthesize.md` |
| 4 Report     | Report delivered with verdict + drop counts                    | `./references/templates/report.md`  |

Do not open a later phase file until the current phase completion criterion is met.

### Branch fix (`fix` \| `apply` \| `implement`)

| Phase | Done when                                                   | READ                         |
| ----- | ----------------------------------------------------------- | ---------------------------- |
| Fix   | Findings applied or deferred without new demonstrable P0/P1 | `./references/phases/fix.md` |

Prerequisite: a prior report in this conversation (or an explicit finding list). If missing, ask — do not invent findings.

## Branch review — phases

### Phase 1 — Scope

**READ:** `./references/phases/scope.md`

Answer intent, expected behavior, and what must not change. Identify the review source (files, diff, branch, paste).

**Completion criterion:** Scope answers written; review source identified.

### Phase 2 — Dispatch

**READ:** `./references/phases/dispatch.md`

Dispatch **five** subagents in parallel (Correctness, Security, Architecture, Quality, Performance). Each prompt includes scope context and exactly one `./references/perspectives/<name>.md` path. Subagents assign no final P0–P3.

**Completion criterion:** Every pipeline returned; each candidate has `file:line`, `exploit_or_break_path`, and `evidence_level`.

### Phase 2.5 — Double verify

**READ:** `./references/phases/verify.md`

Re-read cited code for every candidate. Assign `kept` \| `dropped` \| `downgraded` with notes. Only `kept` and adjusted `downgraded` enter synthesis.

**Completion criterion:** Every candidate has status + `verification_note`; drop/downgrade counts recorded.

### Phase 3 — Synthesize

**READ:** `./references/phases/synthesize.md`

Dedupe, categorize, assign P0–P3, attach `regression_risk` on every kept finding's suggested fix.

**Completion criterion:** Every surviving finding has all required fields; P2/P3 capped per calibration.

### Phase 4 — Report

**READ:** `./references/templates/report.md`

Render the review report. Skip empty severity sections. End with apply hint when findings remain.

**Completion criterion:** Findings Overview, verdict, verified-vs-dropped counts, and explicit unverified claims are present.

## Branch fix

**READ:** `./references/phases/fix.md`

Apply findings from the last report with the fix acceptance gate. Do not open scope, dispatch, or perspective files.

## Rules

- Orchestrator opens phase/template files only when that phase or branch starts
- Review subagents open only their one perspective path
- File:line required; concrete break/exploit path for every P0/P1
- Short approval is valid when warranted; skip empty sections
- Ask before deleting dead code; never recommend blind removal
- Fail loud on verification — state unverified claims explicitly
- For a deeper security pass, tell the user to invoke `/deep-security-review` (do not auto-start it)

## Relation to `deep-security-review`

Both skills are user-invoked. Use this skill for multi-perspective PR/diff review. Use `/deep-security-review` when security is the primary goal. Do not run both Security perspectives on the same scope in parallel — that skill **replaces** the shallow security pass.
