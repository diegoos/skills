# Known items

Orchestrator-only. Open when the user marks a finding as a false positive or out of scope. Confirm the row in that turn.

Create `docs/code-review/knowns.md` in the **reviewed** repo if it is missing. `knowns.md` stays; prune and persist do not delete it.

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

The row is in `knowns.md`. The user has a confirmation.
