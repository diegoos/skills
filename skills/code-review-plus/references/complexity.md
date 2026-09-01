# Complexity and YAGNI (orchestrator)

Open this file in Phase 2.5 only when a candidate is about branching, nesting, a complexity score, speculative abstraction, or YAGNI. Do not preload. Do not give it to hunters.

Project complexity config wins (eslint `complexity`, ruff `C901`, radon, sonar, gocyclo, golangci-lint). No config: estimate on **touched** functions only.

## Count

CC = decision points + 1. Count `if`, `elif` / `else if`, loops, `case`, `catch` / `except`, `&&` / `||` / `and` / `or`, ternary `?:`. `else` = 0. Nested functions have their own CC.

Tools disagree on `switch` (classic: +1 per `case`; modified / Cognitive Complexity: +1 for the whole `switch`). Cite the tool. Eye count: classic, and say so.

CC is a lower bound on basis-path tests and a hotspot rank. It is not a quality score, a bug predictor, or a rewrite trigger.

## Cognitive load vs CC

The readability signal is nesting ≥3, mixed boolean soup, nested ternaries, and unexpected non-local jumps — even when CC is low. Dense one-liners and nested calls can have low CC and high load.

Guard clauses and early returns flatten nesting. They are a fix, not a finding. A higher CC with explicit steps can be the clearer form.

## FLAG vs silence (no project threshold)

| Situation                                                                                                                         | Action                                                                 |
| --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| CC 1–10, or readable with nesting < 3                                                                                             | Silence on CC                                                          |
| New or substantially rewritten function, hard to follow, **and** (nesting ≥3 **or** CC ≥11)                                       | Keep as maintainability; name a remedy                                 |
| Diff **increased** nesting or mixed booleans, even if CC stays < 10                                                               | Keep on the readability signal                                         |
| CC > 20 on touched new/rewritten code                                                                                             | Keep; ask for a local split, table, or tests — not a wholesale rewrite |
| Linear long function; flat `switch` dispatch; table-driven / input validation; Go `if err != nil` series; generated state machine | Drop the complexity candidate                                          |
| High-CC legacy the diff barely touched                                                                                            | Drop (new-code gate)                                                   |
| Score with no comprehension win today                                                                                             | Drop or P3 nit                                                         |

One primary signal per `file:line` (nesting, size, or CC). Project threshold, if present, replaces the CC ≥11 row.

## Anti-gaming

A finding's `suggested_fix` must make a reader faster today. Reject: dense one-liners or nested ternaries that hide branches; extract whose name does not state a responsibility; map/switch swap that only dodges `case` counts; Strategy/polymorphism for a switch that appears once; flattening into boolean soup; `gocyclo:ignore` / eslint-disable without a generated-code or state-machine reason.

## YAGNI

Flag only new complexity in this diff that no real caller uses; skip tests, a refactor that simplifies the current path, and the second real duplicate. Speculative code with no correctness or security hole is Quality/Architecture P2 (plugin / type tree) or P3 (dead field). Abstraction with callers or a shipped contract is not YAGNI.

## Tools (touched files only)

| Stack    | If the project already runs it                        |
| -------- | ----------------------------------------------------- |
| Python   | `radon cc -s` or ruff `C901`                          |
| JS/TS    | eslint `complexity` / sonarjs                         |
| Go       | `gocyclo` or golangci-lint `gocyclo`                  |
| Rust     | cite clippy complexity lints; do not add a second bar |
| Polyglot | lizard or Sonar, if already in CI                     |

Do not introduce a tool the repo does not use. Conflicting numbers: report both; keep the candidate on the human-load signal.

## Remedies (smallest first)

Guard clauses → extract with a responsibility name → lookup / dispatcher → named predicate → polymorphism only when the same switch appears in 2+ places. Phase 3 names the move from `remedies.md`.
