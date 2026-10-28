# Known items

Orchestrator-only. Open when the user marks a finding as a false positive or won't-fix. Confirm the row in that turn.

When this session recorded `Save: session`, add the row to the Session ledger `## Knowns` (same columns) and re-emit the ledger; leave the reviewed repo untouched. Otherwise create `docs/code-review/knowns.md` in the **reviewed** repo if it is missing. `knowns.md` stays; prune and persist do not delete it.

```markdown
# Known review items

Skip these unless the cited path's behavior changed.

## False positives

| Date | Location | Finding | Why | Source |
| ---- | -------- | ------- | --- | ------ |

## Won't fix

| Date | Location | Finding | Why | Source |
| ---- | -------- | ------- | --- | ------ |
```

`Source` is the review filename (stem). Date is `YYYY-MM-DD`.

## Completion criterion

The row is in `knowns.md` or the Session ledger. The user has a confirmation.
