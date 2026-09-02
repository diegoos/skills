# Branch fix — apply findings

Invoked only by `/code-review-plus fix`, `/code-review-plus apply`, or `/code-review-plus implement`. Open `docs/code-review/` in the **reviewed** repo. This file is the only skill reference for this branch.

## Resolve targets

1. Load findings from the last review report **in this conversation**, if one exists.
2. Open the matching memory file under `docs/code-review/` (this conversation's timestamped file, else the newest `YYYY-MM-DD-HH-MM.md`, not `knowns.md`). Read `## Findings`, `Must NOT change`, and `## Fix` when that heading exists (missing `## Fix` means no apply yet).
3. If step 1 found nothing, use `## Findings` from that memory file.
4. If both are empty and the user gave no list, ask. Leave the list empty until they answer.
5. Read `## Fix` when present. Skip an ID listed as Closed when re-reading `file:line` shows the break path is gone. Apply it when the Closed line is stale and the break path still holds. Skip locations in `knowns.md`.
6. Default order: P0 → P1. Apply P2/P3 only when the user asks or lists them.

## Apply loop

For each target finding (one at a time, or one atomic cluster that must ship together):

1. Re-read the cited `file:line` and the finding's `regression_risk` / suggested fix.
2. Apply a **clean minimal local fix** that closes the issue and respects **Must NOT change** from the memory file or the report (Review Summary). Scope = finding path + callers you must touch; no drive-by work outside the finding.
3. Follow **Clean fix** below while editing.
4. Redact secret values in commits, comments, and logs; rotate out-of-band if the finding was a leaked secret.
5. Do not relax auth or validation to make checks pass.
6. Inspect the fix's own diff and re-read touched callers.
7. Run project checks when they exist (test / lint / typecheck / format).
8. Run the **fix acceptance gate** before marking the finding closed.

## Clean fix

Close the finding without changing intended behavior. Prefer the smallest edit that a reader with no PR history can understand.

- **Reuse first.** Use an existing helper/validator/guard in the codebase before inventing a parallel one.
- **One concept per name.** Short everyday words; cut prefixes the module already carries; one name per idea.
- **Derivability.** If a value is computable from what is already in scope, skip a separate pass or store.
- **Comments.** State the non-obvious constraint the code cannot show. Delete narration, conversation/PR history, and comments that restate self-evident code.
- **No unshipped compat.** Drop old signatures, aliases, or shims that only existed earlier in this branch; update callers and delete the dead path.
- **No overfitting.** The diff must stand alone; names and comments must make sense without this conversation.

## Fix acceptance gate

The finding is closed only when all are true:

- The original break/exploit path no longer holds on reading the code today
- No new demonstrable P0/P1 break or vuln was introduced by this fix
- Documented intentional design and named what-must-not-change still hold
- The fix is clean per the section above (reuse, names, no leftover narration/compat)
- Checks that were run passed, or failures are explained and fixed before continuing

If the gate fails: revert or narrow the fix, then retry. Do not proceed to the next finding while a gate failure remains open.

## After all targets

Fill `## Fix` on the memory file from Resolve targets. Create the heading after `## Findings` when it is missing. Merge with Closed/Deferred already there (keep prior Closed IDs that still hold). Replace `_(none yet)_` when an older file still has that placeholder. Write one timestamped file per review.

```markdown
## Fix

- Closed: [ID / severity / file] …
- Deferred: [ID + why] … | none
- Checks: ran … | not run …
```

If that file is missing (read-only gap or no persist), say so in the summary and still report closed vs deferred vs already closed (break path gone, no edit).

Also report to the user:

- Closed findings (ID / severity / file)
- Already closed, no edit (ID + why the path is gone)
- Deferred findings (and why)
- Checks run vs not run

Skip review pipelines. For a re-review, the user invokes `/code-review-plus` on the **fix diff**, with focus: did each fix close its finding without new P0/P1?

## Completion criterion

Every targeted finding is closed (gate passed), skipped because the break path is already gone, or explicitly deferred. No new demonstrable P0/P1 left by the fixes. The memory file's `## Fix` section is updated (or the missing-file gap is stated). Summary of closed vs skipped vs deferred delivered.
