# Example

A full pass from a request to a skill. Read it when this is the first skill of the session, or when a draft fails the check in [`SKILL.md`](../SKILL.md).

The request: "Write a skill that reviews database migrations for data loss before we merge them."

## Find the repeat

Weak: a skill that "helps with databases."
Strong: the repeat is a migration review before merge. Review comments already name the risky changes: a drop, a type change, and a NOT NULL addition. A one-off schema design stays a prompt.

## Choose invocation

Weak: user-invoked, because a review feels like a command.
Strong: model-invoked. The agent has to reach the skill when someone asks to check a migration and never types the skill name. The description cost is worth that reach.

## Write the description

Weak: "Helps with database migrations."
Strong: "Reviews a database migration for data-loss risks. Use when the user asks to check, review, or approve a migration file. Skip when the task is to write a new schema." `check`, `review`, and `approve` stay because each is a real request for the same branch. A second wording of `review` would go.

## Structure the skill

Weak: one `SKILL.md` that also holds the rollback catalog, plus a line that says "see the references."
Strong: the steps stay in `SKILL.md`. The catalog is a lookup the agent can run, so it stays out. This skill has no branch depth, so `SKILL.md` holds everything and has no pointer.

## Write the steps

Weak: "Review the migration carefully. Do not miss a drop."
Strong: "For each drop, type change, or NOT NULL addition, state the data-loss risk and the safe alternative. **Done when:** each risky change has a verdict."

Weak output: "Summarize the findings."
Strong output: one line per change, `verdict | change | next action`.

Weak exit: "Ask for the migration file, and wait until it arrives."
Strong exit: "When the request has no migration file, stop with a blocked report that names the missing file and asks for it."

## Prune

Weak: "Be thorough, and remember that data loss is bad."
Strong: delete both clauses. The criterion already forces a verdict on every risky change, and the model already treats data loss as harmful. Neither clause changes a decision.

## Write the cases

The requests and the two functional cases in Check are `cases.md`, beside `SKILL.md`. The report names that file.

## Check

| # | request | should trigger | author | trial |
| --- | --- | --- | --- | --- |
| 1 | Check this migration for data loss | yes | pass | not run |
| 2 | Review the migration before we merge | yes | pass | not run |
| 3 | Approve this migration file | yes | pass | not run |
| 4 | Write a new schema for orders | no | pass | not run |
| 5 | Review the migration runbook for the rollout | no | pass | not run |
| 6 | Help with databases | no | pass | not run |

`author` is `pass` when the reading of the description in [Resulting skill](#resulting-skill) matches `should trigger`. `trial` is `not run` on every row: no clean session for this sample.

Edge. Prompt: review a migration that only adds a nullable column. Inputs: that file. Expected result: an empty risk list. Assertion: the output states that no risky change exists. `trial`: `not run`, no clean session for this sample.

Trap. Prompt: review a migration that drops `users.email` and adds `notes`, a column nothing reads. Inputs: that file. Expected result: a data-loss verdict on the drop, and no data-loss verdict on `notes`. Assertion: the drop line has a verdict and a next action, and `notes` is absent from the data-loss lines. `trial`: `not run`, no clean session for this sample.

## Resulting skill

The check table reads this description. Row 5 is `pass`.

```markdown
---
name: review-migrations
description: >-
  Reviews a database migration for data-loss risks. Use when the user asks to check, review, or approve a migration file. Skip when the task is to write a new schema or to review a runbook.
---

# Review migrations

Review one migration for data loss. A change is risky when it drops an object, changes a type, or adds NOT NULL.

## Inputs

- `migration` (file or diff, required): the migration to review.

## Steps

1. List each risky change. **Done when:** every drop, type change, and NOT NULL addition is in the list.
2. For each item, state the data-loss risk and a safe alternative. **Done when:** each item has a verdict and a next action.
3. Write the output. **Done when:** each risky change appears once as `verdict | change | next action`, and an empty list yields one line that no risky change exists.

## Output

One line per risky change: `verdict | change | next action`. When the list is empty, state that no risky change exists.

When the request has no migration file, stop with a blocked report that names the missing file and asks for it.
```

## Editing a skill

The description in [Write the description](#write-the-description) left row 5 `fail`, because `review` and `migration` also fit a runbook. The skip in the resulting skill names that neighbor, so the row is `pass`.
