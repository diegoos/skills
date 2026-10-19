---
name: verb-object
description: >-
  Lead with the job. Use when the user asks for the main trigger. Skip when a nearby task would match by mistake.
---

# Verb object

One sentence: the process this skill makes repeat.

## Inputs

- `input-name` (type, required or optional): where the value comes from.

## Steps

1. Do the first action. **Done when:** a checkable condition that forces the full work.
2. Do the next action. **Done when:** the output matches the shape this step names.

## Output

One short result the caller can check.

When a required input is missing and the run cannot ask, stop and report the missing input as the next thing to provide.
