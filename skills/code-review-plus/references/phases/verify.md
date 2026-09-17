# Phase 2.5 — Validator

Reject false positives after all pipelines return. Only candidates that survive Pass B enter synthesis.

When keep/drop is unclear, read `../examples/kept-vs-dropped.md`. When a candidate is about branching, nesting, a complexity score, speculative abstraction, or YAGNI, also read `../complexity.md`.

## Intake

Confirm each candidate still carries:

- `evidence_level: proven | likely`
- `exploit_or_break_path` with a pointable line today (break, exploit, or cost)
- `suggested_fix` that is minimal and local when possible

Drop immediately if those fields are missing, speculative, or `location` is on Phase 1 `Skip` and that path's behavior did not change.

## Pass B — validator

Re-open `file:line` plus callers, middleware, shared helpers, and consumers as needed. Three questions on **every** remaining candidate:

1. Does the break, exploit, or today's cost hold on reading the code, with a pointable `file:line`?
2. Does this contradict another candidate or a likely "What Looks Good" strength?
3. Would the suggested fix pass the **regression gate** (minimal, local, respects what-must-not-change)?

Drop or downgrade any item that fails. Future-only risks become hardening, not blockers. Keep maintainability when today's cost is pointable, including Quality extras the Floor did not name. Keep a real issue when `pipeline` is a mismatch; synthesize assigns category. Dead-code after a full consumer search goes to Dead Code, not P0. Formatter/linter style stays unflagged unless the line is broken or unsafe today.

`likely` with a pointable line: re-read. Confirm → **proven**. Line holds but the path is still incomplete → keep as hardening (not P0/P1). No line today → drop.

On residual ambiguity (middleware vs route, framework return shape, `needs-runtime` borderline): downgrade or mark unverified. Pass B decides on this candidate set.

### P0 bar

P0 is an exploit/break path reconfirmed today with a pointable `file:line` after Pass B. Maintainability, YAGNI-without-a-hole, verified unused code, and `needs-runtime` without proof in code stay below P0 (unverified or hardening). P0 and P1 require `evidence_level: proven`.

## Verification artifact (required per candidate)

```yaml
status: kept | dropped | downgraded
drop_reason: # required when dropped or downgraded
verification_note: # files and callers/middleware re-read, then why it survived or failed
# keep original CandidateFinding fields when kept/downgraded
```

Pass B is complete only when `verification_note` cites what was re-read (`file` plus callers / middleware / helpers as needed). A note with no citation is not Pass B.

**Report bar:** only `kept` and `downgraded` enter Phase 3. Phase 3 assigns severity; those findings (with adjusted severity) enter the report. Record verified vs dropped/downgraded counts for the summary. Copy `quality_source` from the Quality hunter when Quality ran.

## Post-report calibration (optional)

If the user asks to calibrate this review, follow `../examples/eval-notes.md` in the conversation (write a file in the reviewed repo only if they ask).

## Completion criterion

Every candidate has `status` and a `verification_note` that cites the files/callers re-read. Dropped/downgraded counts are recorded for the summary. P0 candidates that fail the P0 bar are downgraded or marked unverified. `quality_source` is available for persist when Quality ran.
