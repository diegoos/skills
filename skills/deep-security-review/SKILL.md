---
name: deep-security-review
description: >-
  Deep security review with parallel domain hunts and a prioritized findings table (P0–P3). Branches: review (default), fix / apply / implement (apply findings without new P0/P1). Invoke by name only (e.g. /deep-security-review, /deep-security-review fix).
disable-model-invocation: true
metadata:
  version: 0.2.0
  author: "Diego Oliveira"
  tags:
    - security
    - security review
    - threat modeling
    - deep review
---

# Deep Security Review

**Branches:** review (default) → plan → parallel domain hunts → verify & synthesize → report. Fix branch applies findings with a **fix acceptance gate**.

**Invariants:** Each domain runs as a separate subagent. Every finding must be reproducible by reading the code. Keep only `proven` or `likely` issues with a pointable line today; reject false positives in Phase 3 before severity. Prefer proven exploit paths over speculative Mediums. Leading question: what can an attacker do from the lowest practical privilege?

**Reference budget:** The orchestrator selects paths; subagents read them. Never preload `references/`. Each hunter gets at most **1 domain + 1 shape**. Orchestrator-only `examples/` (gates / FPs / worked cases) are not hunter paths.

## Commands

| Invocation                        | Branch     | Behavior                          |
| --------------------------------- | ---------- | --------------------------------- |
| `/deep-security-review`           | **review** | Phases 1→4 only                   |
| `/deep-security-review fix`       | **fix**    | `./references/phases/fix.md` only |
| `/deep-security-review apply`     | **fix**    | Alias of `fix`                    |
| `/deep-security-review implement` | **fix**    | Alias of `fix`                    |

`fix`, `apply`, and `implement` are synonyms. Without a subcommand, never open `fix.md`. The fix branch never re-dispatches domain hunters.

## Definition of Done

### Branch review

| Phase    | Done when                                                                                     | READ                                           |
| -------- | --------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| 1 Plan   | Threat model (incl. hotspots, bypasses, auth_model) + tags + manifest paths written           | `./references/phases/plan.md`                  |
| 2 Hunt   | All domains returned; each candidate has location, domain, exploit path, provenance, evidence | `./references/phases/hunt.md`                  |
| 3 Verify | Disprove done; FPs dropped; P0–P3 set (CRITICAL–LOW 1:1); counts; re-verify ran or skipped    | `./references/phases/verify-and-synthesize.md` |
| 4 Report | Findings + Hardening notes + Verification Gaps + verdict delivered                            | `./references/templates/report.md`             |

Do not open a later phase file until the current phase completion criterion is met.

### Branch fix (`fix` \| `apply` \| `implement`)

| Phase | Done when                                                   | READ                         |
| ----- | ----------------------------------------------------------- | ---------------------------- |
| Fix   | Findings applied or deferred without new demonstrable P0/P1 | `./references/phases/fix.md` |

Prerequisite: a prior report in this conversation (or an explicit finding list). If missing, ask; do not invent findings.

## Branch review — phases

### Phase 1 — Plan

**READ:** `./references/phases/plan.md`

Capture threat model (assets, actors, entry points, trust boundaries, abuse_goals, auth_model, hotspots, bypasses), detect shape tags, build the Reference Plan (`DispatchManifest`). Orchestrator may open **only** that file from `references/` in this phase — not `domains/` or `shapes/`.

**Completion criterion:** Manifest lists every dispatched domain with exact paths (`domain` + optional `shape`, or `"none"`); hotspots (1–15), bypasses (or `none found`), and auth_model are filled.

### Phase 2 — Hunt

**READ:** `./references/phases/hunt.md`

Dispatch **four** subagents in parallel (AuthZ, Injection, Secrets, Infra). Add BusinessLLM when any dispatch signal below is true (see Phase 2).

Each subagent prompt includes: scope, threat-model summary, hotspots, bypasses, auth_model, and the **exact** paths from the manifest. Subagents assign no final P0–P3.

**Completion criterion:** Every dispatched domain returned; each candidate has `file:line`, `domain`, exploit path, provenance, and evidence level.

### Phase 3 — Verify & Synthesize

**READ:** `./references/phases/verify-and-synthesize.md`

Disprove and verify every candidate against code, drop/downgrade false positives (Pass A intake, checklist, gates/FP file when needed), dedupe, categorize, assign P0–P3 to kept vulns (CRITICAL–LOW follows 1:1), run re-verify when its triggers fire.

**Completion criterion:** Every candidate has `status` + `verification_note` (`drop_reason` when dropped/downgraded); surviving Findings have required fields (P0/P1 include `trace`, `intended_behavior`, `trigger_sketch`); `{kept, downgraded, dropped}` recorded; re-verify ran or skipped.

### Phase 4 — Report

**READ:** `./references/templates/report.md`

Render the security review report. Skip empty severity sections. Keep Findings, Hardening notes, and Verification Gaps mutually exclusive.

**Completion criterion:** Findings Overview (kept only; empty table when kept is 0 and the summary states that nothing was found), Hardening notes or explicit none, Verification Gaps, verdict, and counts are present.

## Branch fix

**READ:** `./references/phases/fix.md`

**Completion criterion:** Every targeted finding is closed (gate passed) or explicitly deferred. No new demonstrable P0/P1 left by the fixes.

## Rules

- Orchestrator opens phase/template files only when that phase or branch starts
- Subagents open only the paths in their manifest slot (≤2)
- Every P0/P1 cites `file:line` and a concrete attacker path readable today
- Findings keep only `proven`/`likely` with a pointable line today; route `needs-runtime` to Verification Gaps (never P0–P3)
- Prefer drop/downgrade when middleware, schema, allowlists, or encoders already block the path
- Zero kept findings → Approve with an empty Findings Overview; omit empty severity sections; report only what survived verify
- State unverified claims explicitly
- Stop and ask when legal scope or testing boundaries are unclear
- Report secrets as `file:line` + type only; redact values in the report and in fixes
- Fix branch: close exploit paths fail-closed; keep auth, validation, CSRF, and rate limits intact
- Re-verify: at most one subagent when its triggers fire; skips otherwise; never reopens domain hunts; does not assign final severity

## Limitations

Code/architecture review — not a substitute for penetration testing. Runtime claims need logs, deployed config, or test access before definitive language.

## Relation to `code-review-plus`

Both skills are user-invoked. Use `/code-review-plus` for multi-perspective PR/diff review (including `/code-review-plus fix`). Use this skill when security is the primary goal. Do not run both Security perspectives on the same scope in parallel — this skill **replaces** the shallow security pass.
