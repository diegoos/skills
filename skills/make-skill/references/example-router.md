# User invocation

Read this when the skill is user-invoked, or when user-invoked skills need a router or a shared reference.

## One skill

Weak: a model-invoked description with a trigger list, for a skill a person always starts by name.

Strong: set `disable-model-invocation: true`. The description is one line and names the job: "Reviews a diff when someone types the skill name."

## Router

Three user-invoked skills, `review-sql`, `review-api`, and `review-ui`, cost more to remember than one index.

Weak: a model-invoked skill that tries to fire them.

Strong: one user-invoked router. It names the three and when to use each. It can hint. It cannot fire them.

```markdown
---
name: review-router
description: Opens the review skill for the surface the person names.
disable-model-invocation: true
---

# Review router

Use `review-sql` for a migration or a query. Use `review-api` for a handler or a contract. Use `review-ui` for a screen or a component.
```

## Shared reference

The three skills need the same severity scale.

Weak: paste the scale into each skill.

Strong: one file outside the three, and each skill points to it with the condition for opening it. A model-invoked skill that holds only the scale is the other fit, when other skills must reach it. Put that choice in the skill.
