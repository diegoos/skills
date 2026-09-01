---
name: make-code
description: >-
  XP Simple Design for application code (YAGNI, cyclomatic cap): make it work, right, then fast. Use when writing, refactoring, simplifying, or speeding up code. Branches: write (new behavior), refactor (simpler), improve (faster).
metadata:
  version: 0.0.1
  author: "Diego Oliveira"
  tags:
    - code
    - yagni
    - xp
    - cyclomatic
    - refactor
    - performance
---

# Make code

XP **Simple Design**, in order: the code *runs*, reveals *intent*, has each idea *once*, and uses the *fewest* elements that still do those three. **YAGNI** is the stop. **CC** is the local ceiling.

Pick a **branch** and state it at the start of the run:

- new behavior (feature, fix) → **write**
- same behavior, simpler → **refactor**
- same behavior, faster → **improve** (only with a named hotspot)

## Workflow

1. **Classify.** Branch from the request. **Improve** only when a hotspot is named (profile, N+1, accidental quadratic, extra I/O or alloc in a hot loop, or the user named it). No hotspot → **refactor**, or ask. **Done when:** the branch is named; **improve** cites the hotspot.
2. **Trace.** Name the problem, the entrypoints, the symbols you will change, their callers (search every caller), and the check that proves the change. Read existing docs. Reuse what already covers the need. **Done when:** those five are named, or **YAGNI** stops the work.
3. **Climb.** Stop at the first rung that holds: (1) skip (2) in-repo helper (3) stdlib (4) platform (5) installed dependency (6) one line (7) minimum new code. **Done when:** the chosen rung is named.
4. **Apply** the matching branch. **Done when:** that branch's criterion holds.
5. **Prove.** Smallest *red* check of observable behavior. Mock only at the trust boundary (network, clock, filesystem, paid API). Call through real internals. Trivial one-liners need no extra test. **Done when:** **write** — the check is red before the slice and green after; **refactor** / **improve** — the same check stays green.

## Branch write

Do the *simplest thing* that could work. One slice.

**Done when:** the requested behavior is observable; every new or rewritten function is **CC** ≤ 10 (or the project's bar); no type or file exists that this slice does not call.

## Branch refactor

Preserve behavior. Prefer deletion. Flatten with guard clauses before extract. Extract only with a responsibility name.

**Done when:** behavior matches the original (proof from Prove); every touched function is **CC** ≤ 10 (or the project's bar); the diff is smaller or clearer than the starting shape.

## Branch improve

Keep behavior. Remove the named hotspot. Ship the cheap fast path (stdlib, one pass, no N+1, no accidental quadratic). A cache, pool, or index only when that hotspot is measured or the user named it.

**Done when:** the named hotspot is gone; behavior matches the original (proof from Prove); no new type exists solely to hold the old slower path.

## Floor (every branch)

**YAGNI.** Build the need in this request. The second real duplicate earns extract; the first does not.

**CC.** Decision points + 1 (`if`, loops, `case`, `catch`, `??`, `||`, `&&`, `.?`, boolean short-circuit, ternary). `else` = 0. Cap **10** on new or rewritten functions unless the project sets another bar (`eslint complexity`, ruff `C901`, gocyclo, etc). Keep branches visible (guard clauses, named predicates). A linear validation chain or a flat `switch` is not a split trigger. Use the project's existing complexity command when one exists.

**Tight performance.** Default is the cheap fast path. Speculative optimization is **YAGNI** — that work belongs on **improve** with a named hotspot.

**Keep.** Understanding before the diff. Validation and fail-closed at trust boundaries. Errors that prevent data loss. Secrets and authorization. Accessibility. Platform calibration (clocks, sensors). Anything the user named. A non-trivial change with no *red* check is unfinished. An authorized corner that cuts a real limit: mark `ceiling: <limit>; upgrade: <path>`.

## Ask

Ask when the choice is architecture, a contract, data, security, or two designs of similar size with different costs. For a small reversible choice, pick the *simplest thing* and state the assumption.
