---
name: deep-security-review
description: Deep security review with domain hunts and a P0–P3 findings table; review (default); fix, fix all, or fix by id.
disable-model-invocation: true
metadata:
  version: 0.3.0
  author: "Diego Oliveira"
  tags:
    - security
    - security review
    - threat modeling
    - deep review
---

# Deep Security Review

**Branches:** review (default) → plan → hunt → verify → emit. Fix applies findings with a **regression gate**.

**Invariants:** Domain hunts in parallel (serial fallback in `hunt.md`). Skill files **complement** the model's security knowledge. **floor** and **today** live in the Hunt bar. **Pass B** confirms; P0/P1 require **proven**. **regression gate** on suggested fixes. Lowest practical privilege.

**Load:** Open a phase file when that phase starts. Hunter load: **1** domain + **0 or 1** shape (context; hunt in code after). More skill files still count as a valid pass. Orchestrator-only: `plan.md`; `examples/` in Phase 3/4. Fix reads `make-code` when that skill is in the environment.

## Commands

| Invocation                         | Branch     | Behavior                                  |
| ---------------------------------- | ---------- | ----------------------------------------- |
| `/deep-security-review`            | **review** | Phases 1→4                                |
| `/deep-security-review fix`        | **fix**    | P0 and P1; then remaining-ID hints        |
| `/deep-security-review fix all`    | **fix**    | every P0–P3 finding (hardening included)  |
| `/deep-security-review fix <ids>`  | **fix**    | those Findings IDs (`2,3,6` or `2 3 6`)   |

`apply` and `implement` are aliases of `fix` (same **selection** after the token).

Parse the text after `/deep-security-review` (first reserved token wins):

1. `fix` \| `apply` \| `implement` → **fix**; remainder is the **selection** (`all` \| finding IDs \| empty default). Open `fix.md`
2. Empty or no match → **review**

## Definition of Done

Done for each phase is the completion criterion in its READ file. Open the next phase file when that criterion is met. Emit the report when Phase 4 is done.

### Branch review

| Phase    | Done when                                                                                   | READ                                           |
| -------- | ------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| 1 Plan   | Threat model + tags + manifest paths written                                                | `./references/phases/plan.md`                  |
| 2 Hunt   | All domains returned; each candidate has location, domain, path, provenance, evidence       | `./references/phases/hunt.md`                  |
| 3 Verify | Pass B done; FPs dropped; P0–P3 set; counts; re-verify ran or skipped                       | `./references/phases/verify-and-synthesize.md` |
| 4 Report | Skeleton filled and emitted                                                                 | `./references/templates/report.md`             |

### Branch fix (`fix` \| `apply` \| `implement`)

| Phase | Done when                                                                                        | READ                         |
| ----- | ------------------------------------------------------------------------------------------------ | ---------------------------- |
| Fix   | Selected findings applied or deferred; default **selection** names leftover IDs                  | `./references/phases/fix.md` |

Prerequisite: a review report in this conversation or an explicit finding list. If none exist, ask. Leave the finding list empty until the user provides one.

## Rules

- Report secrets as `file:line` + type only; redact values in the report and in fixes
- Close exploit paths fail-closed; keep auth, validation, CSRF, and rate limits intact

## Limitations

Semantic review of assembled code (AuthZ, tenant isolation, business logic, tool/MCP chains). Deterministic SAST/SCA cover known classes; a clean scan is not a ship decision. Not a substitute for penetration testing. Runtime claims need logs, deployed config, or test access before definitive language.

## Skill links

When suggesting `make-code` or `code-review-plus`, include that GitHub URL. Catalog only when naming the collection.

| Skill                | URL                                                                       |
| -------------------- | ------------------------------------------------------------------------- |
| make-code            | <https://github.com/diegoos/skills/tree/main/skills/make-code>            |
| code-review-plus     | <https://github.com/diegoos/skills/tree/main/skills/code-review-plus>     |
| catalog              | <https://github.com/diegoos/skills/tree/main/skills>                      |

## Relation to `code-review-plus`

Both skills are user-invoked. `/code-review-plus` always uses its own slim Security hunter. Invoke this skill when security is the primary goal, or after a CRP report that ends with a `/deep-security-review` suggestion. Leave `code-review-plus` unstarted. When the conversation already has a CRP report, omit the CRP line. Else the review report ends with a `/code-review-plus` suggestion plus its Skill links URL (`report.md`).
