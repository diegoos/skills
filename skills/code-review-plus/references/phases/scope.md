# Phase 1 — Scope

Establish intent, review source, dispatch tier, and stack tags before any pipeline runs.

## Intent questions

Answer before dispatching:

```txt
- What is this change trying to accomplish?
- Which specification, task, or PR does it implement?
- What is the expected behavior change?
- What should NOT change?
```

Record `What should NOT change` in concrete terms (APIs, contracts, UX, callers). The fix branch uses it as the **regression gate**.

If a PR/commit description exists in context, note whether the first line stands alone as a summary of the change.

## Identify what to review

| Source              | Action                                                       |
| ------------------- | ------------------------------------------------------------ |
| Specific files      | Review those files in full context                           |
| Uncommitted changes | `git diff`                                                   |
| Feature branch      | `git diff <base>...HEAD` (use repo's default base)           |
| Pasted code         | Review directly                                              |
| Large diff          | Prioritize: new files → modified logic → config → formatting |

## Change sizing

Estimate logic lines changed (ignore pure formatting noise when counting):

| Size   | Rough bar               | Scope note                                                                                        |
| ------ | ----------------------- | ------------------------------------------------------------------------------------------------- |
| Small  | ~100 lines              | Reviewable in one pass                                                                            |
| Medium | ~300 lines              | OK if one logical change                                                                          |
| Large  | ~1000+ or many concerns | Ask for split: stack / horizontal / vertical / by file group; keep refactor separate from feature |

Also watch **file size**: a small diff that grows an already-huge file may need extract-before-add. Record oversized in the context summary so the report can ask for a split.

## Dispatch tier (checkable)

Pick exactly one tier:

| Tier                | When                                                                 | Pipelines                                                                                                   |
| ------------------- | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **trivial**         | Docs-only, formatting-only, or rename with no logic                  | Correctness + Quality; add Security only if auth, input boundary, secrets, deps, or security config touched |
| **normal**          | Default feature/bugfix/refactor                                      | All five: Correctness, Security, Architecture, Quality, Performance                                         |
| **large/sensitive** | ≥~300 logic lines, or touches auth, payments, secrets, raw user HTML | All five + up to one shape per hunter when stack tags match                                                 |

## Stack tags

From paths/extensions in the review source, record zero or more: `web`, `api`, `ts` (TypeScript/JavaScript/Node), `py` (Python), `go` (Go), `rs` (Rust). These select optional shapes in Phase 2.

Also note if the diff touches a **documentable surface** (public API, CLI, contract, build/test/release, user-facing behavior) so Quality can check docs sync.

## Tests first

Tests reveal intent and coverage gaps:

- Are there tests for the change?
- Do they test behavior, not implementation details?
- Are edge cases covered?
- Would tests catch a regression?

If the repo documents test/lint scripts, the orchestrator may run them readonly and record results; never claim they passed if they did not run.

## Context summary (required for Phase 2)

Compact block for every hunter prompt:

```txt
Intent: …
Must NOT change: …
Source: …
Tier: trivial | normal | large/sensitive
Stack tags: web | api | ts | py | go | rs | (none)
Documentable surface: yes | no
Tests observed: …
Sizing: small | medium | large
```

## Completion criterion

Scope answers written; review source, tier, and stack tags identified; sizing noted; context summary ready for Phase 2.
