# Phase 1 — Scope

Establish intent and review source before any pipeline runs.

## Intent questions

Answer before dispatching:

```txt
- What is this change trying to accomplish?
- Which specification, task, or PR does it implement?
- What is the expected behavior change?
- What should NOT change?
```

`What should NOT change` feeds the **regression gate** later — keep it concrete (APIs, contracts, UX, callers).

## Identify what to review

| Source              | Action                                                       |
| ------------------- | ------------------------------------------------------------ |
| Specific files      | Review those files in full context                           |
| Uncommitted changes | `git diff`                                                   |
| Feature branch      | `git diff <base>...HEAD` (use repo's default base)           |
| Pasted code         | Review directly                                              |
| Large diff          | Prioritize: new files → modified logic → config → formatting |

## Tests first

Tests reveal intent and coverage gaps:

- Are there tests for the change?
- Do they test behavior, not implementation details?
- Are edge cases covered?
- Would tests catch a regression?

Capture a one-to-two sentence context summary for subagent prompts.

## Completion criterion

Scope answers written; review source identified; context summary ready for Phase 2.
