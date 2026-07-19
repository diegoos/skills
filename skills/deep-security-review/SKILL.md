---
name: deep-security-review
description: >-
  Deep security review with parallel domain hunts and a prioritized findings table (P0–P3). Invoke by name only (e.g. /deep-security-review).
disable-model-invocation: true
metadata:
  version: 0.1.0
  author: "Diego Oliveira"
  tags:
    - security
    - security review
    - threat modeling
    - deep review
---

# Deep Security Review

**Phases:** plan → parallel domain hunts → verify & synthesize → report.

**Invariants:** Each domain runs as a separate subagent. Every finding must be reproducible by reading the code. Prefer proven exploit paths over speculative Mediums. Leading question: what can an attacker do from the lowest practical privilege?

**Reference budget:** The orchestrator selects paths; subagents read them. Never preload `references/`. Each hunter gets at most **1 domain + 1 shape**.

## Definition of Done

| Phase    | Done when                               | READ                                           |
| -------- | --------------------------------------- | ---------------------------------------------- |
| 1 Plan   | Threat model + tags + manifest written  | `./references/phases/plan.md`                  |
| 2 Hunt   | All domains returned candidates         | `./references/phases/hunt.md`                  |
| 3 Verify | Candidates verified + severity assigned | `./references/phases/verify-and-synthesize.md` |
| 4 Report | Findings table + verdict delivered      | `./references/templates/report.md`             |

Do not open a later phase file until the current phase completion criterion is met.

## Phase 1 — Plan

**READ:** `./references/phases/plan.md`

Capture threat model, detect shape tags, build the Reference Plan (`DispatchManifest`). Orchestrator may open **only** that file from `references/` in this phase — not `domains/` or `shapes/`.

**Completion criterion:** Manifest lists every dispatched domain with exact paths (`domain` + optional `shape`, or `"none"`).

## Phase 2 — Hunt

**READ:** `./references/phases/hunt.md`

Dispatch **four** subagents in parallel (AuthZ, Injection, Secrets, Infra). Add Business & LLM when tags include `llm` / `sensitive` or the threat model shows high-value flows.

Each subagent prompt includes: scope, threat-model summary, and the **exact** paths from the manifest. Subagents assign no final P0–P3.

**Completion criterion:** Every dispatched domain returned; each candidate has `file:line`, exploit path, provenance, and evidence level.

## Phase 3 — Verify & Synthesize

**READ:** `./references/phases/verify-and-synthesize.md`

Verify every candidate against code, drop/downgrade false positives, dedupe, categorize, assign P0–P3 + CRITICAL–LOW.

**Completion criterion:** Every surviving finding has all required fields; dropped count recorded for the summary.

## Phase 4 — Report

**READ:** `./references/templates/report.md`

Render the security review report. Skip empty severity sections.

**Completion criterion:** Findings Overview table, verdict, and explicit unverified claims are present.

## Rules

- Orchestrator opens phase/template files only when that phase starts
- Subagents open only the paths in their manifest slot (≤2)
- File:line required; concrete attacker path for every P0/P1
- `needs-runtime` is never P0; state unverified claims explicitly
- Stop and ask when legal scope or testing boundaries are unclear
- Never echo secrets found during the review

## Limitations

Code/architecture review — not a substitute for penetration testing. Runtime claims need logs, deployed config, or test access before definitive language.

## Relation to `code-review-plus`

Both skills are user-invoked. Use `/code-review-plus` for multi-perspective PR/diff review. Use this skill when security is the primary goal. Do not run both Security perspectives on the same scope in parallel — this skill **replaces** the shallow security pass.
