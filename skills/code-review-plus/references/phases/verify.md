# Phase 2.5 — Double verify

Reject false positives after all pipelines return. Only candidates that survive Pass B enter synthesis.

When keep/drop is unclear, read `../examples/kept-vs-dropped.md` (do not preload).

## Pass A — hunter (already done in dispatch)

Confirm each candidate still carries:

- `evidence_level: proven | likely`
- `exploit_or_break_path` with a pointable line today
- `suggested_fix` that is minimal and local when possible

Drop immediately if Pass A fields are missing or speculative.

## Pass B — orchestrator verify

Re-open `file:line` plus callers, middleware, shared helpers, and consumers as needed. Run this checklist on **every** remaining candidate:

```txt
- [ ] Did I read the entire cited file (not just the diff snippet)?
- [ ] Did I read middleware / global layer before flagging a route?
- [ ] What is the data provenance (user input / LLM / backend / n/a)?
- [ ] Did I trace the full pipeline to the final output?
- [ ] Is there a comment explaining intentional design? Did I respect it?
- [ ] Did I verify framework behavior before asserting failure modes?
- [ ] Did I verify all call paths before calling something dead/redundant?
- [ ] Can I reproduce the break/exploit by reading the code without "if in the future"?
- [ ] Does this contradict another candidate or a likely "What Looks Good" strength? (self-consistency)
- [ ] Would the suggested fix pass the regression gate (minimal, local, respects what-must-not-change)?
- [ ] Does suggested_fix preserve error behavior and side effects (no over-simplify)?
- [ ] Can I point to the exact line that makes this exploitable or broken today?
```

Drop or downgrade any item that fails. Future-only risks become hardening (downgrade), not blockers.

### P0 bar

A candidate may become P0 in synthesize only if Pass B is complete and the exploit/break path is reconfirmed today with a pointable `file:line`. Claims that need deployed config or runtime observation (`needs-runtime`) are never P0 without proof in code; mark them unverified or hardening.

## Verification artifact (required per candidate)

```yaml
status: kept | dropped | downgraded
drop_reason: # required when dropped or downgraded
verification_note: # why it survived or failed
# keep original CandidateFinding fields when kept/downgraded
```

**Report bar:** only `kept` and `downgraded` (with severity already adjusted in Phase 3) enter the report. Record verified vs dropped/downgraded counts for the summary.

## Recurring false positives

| Pattern                                                                     | Why it is usually wrong                                                                                                                                |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `credentials: "include"` leaks cookies cross-origin                         | Browser sends cookies only for the destination origin. Relative-path guards are defense-in-depth, not an active vuln.                                  |
| Route "without CSRF" when global middleware covers it                       | Check `middleware.ts` (or equivalent) first. Never praise global CSRF in "What Looks Good" and flag a route below — self-consistency check.            |
| XSS in a pipeline that escapes everything and unescapes only fixed literals | If final step escapes `&<>` and `replaceAll` uses only literal strings, attribute/event injection is not possible today. Classify as future hardening. |
| Memory leak on listener with cleanup                                        | `onMount` returning cleanup (or `onDestroy`) does not leak. At most P2 optimization.                                                                   |
| Dead/redundant code without checking all consumers                          | Defensive helpers often handle raw fetch envelopes or alternate library paths. Verify before removal.                                                  |
| P0 from "if in the future" or "any evolution could"                         | Future risk is hardening (P2), not a blocker.                                                                                                          |
| "Missing abstraction" / "should extract helper" on first or second use      | Prefer duplication until a third real use case. Maintainability, not a bug.                                                                            |
| Pattern mismatch that is an intentional local exception with a comment      | Respect documented intentional design; at most P3 nit.                                                                                                 |
| "Wrong layer" when the codebase already places similar logic there          | Follow existing codebase patterns; architecture findings need a concrete boundary break.                                                               |
| Style-only rename with no readability or consistency win                    | Skip; established local style wins.                                                                                                                    |
| Configured formatter/linter owns style (gofmt, rustfmt, clippy, PEP8…)      | Tool owns style; drop unless the line is broken or unsafe today.                                                                                       |
| Type mismatch that the compiler/typechecker already accepts correctly       | Verify actual types before asserting; framework return shapes often differ from intuition.                                                             |
| N+1 or missing index without a hot path or measured cost                    | Likely P2 hardening; not P0 unless demonstrated breakage or clear production scale path.                                                               |
| suggested_fix that removes or weakens error handling "for clarity"          | Over-simplify. Preserve error paths; drop or rewrite the fix.                                                                                          |
| "Unnecessary abstraction" without callers, intent, and reason it exists     | Understand why it exists before removing.                                                                                                              |
| "Fewer lines = simpler" / nested ternary one-liner as an improvement        | Clarity is comprehension speed, not LOC.                                                                                                               |
| Inline a helper that named a useful concept                                 | Keep the name unless the inline form is clearly clearer in context.                                                                                    |
| Merge/extract with only 1–2 aesthetic uses                                  | Respect third-use; skip or P3.                                                                                                                         |
| Layout "exports first" against local repo convention                        | Follow the codebase's file order.                                                                                                                      |
| "Unshipped compat" without checking main/release                            | May be real BC; verify history before proposing delete.                                                                                                |
| "Missing docs" without a documentable surface change or docs in scope       | Do not invent tutorials.                                                                                                                               |
| Reviewer bias: "tests pass => good", "agent code => fine", "clean later"    | Still verify the path today.                                                                                                                           |
| "Refactor is cleaner" when it only relocated the same concept count         | Relocate != reduce.                                                                                                                                    |

## Completion criterion

Every candidate has `status` and `verification_note`. Dropped/downgraded counts are recorded for the summary. P0 candidates that fail the P0 bar are downgraded or marked unverified.
