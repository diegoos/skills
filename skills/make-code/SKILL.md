---
name: make-code
description: >-
  Write application code. Use when implementing or fixing a feature, endpoint, or function; simplifying existing behavior; or speeding up a named hotspot (N+1, hot loop, extra I/O). Skip docs, agent instructions, Makefiles, and CSS-only restyles.
metadata:
  version: 0.2.0
  author: "Diego Oliveira"
  tags:
    - code
    - kiss
    - dry
    - yagni
    - cyclomatic
    - refactor
    - performance
---

# Make code

Application code under **KISS**, **DRY**, **YAGNI**, and **CC**. **KISS** is the path. **DRY** is one representation, earned. **YAGNI** is the stop. **CC** is the local ceiling.

Pick a **branch** and state it at the start of the run:

- new behavior (feature, fix) → **write**
- same behavior, simpler → **refactor**
- same behavior, faster → **improve** (only with a named hotspot)

## Workflow

1. **Classify.** Branch from the request. **Improve** only when a hotspot is named (profile, N+1, accidental quadratic, extra I/O or alloc in a hot loop, or the user named it). No hotspot → **refactor**, or ask. **Done when:** the branch is named; **improve** cites the hotspot.
2. **Trace.** Name the problem, the entrypoints, the symbols you will change (a bug: the shared root those callers already hit), their callers (search every caller), the check that proves the change, and the convention source (nearest `AGENTS.md` / `CLAUDE.md` and one neighbor of the same kind, or `conventions: none`). Read existing docs. Reuse what already covers the need. **Done when:** those six are named, or **YAGNI** stops the work.
3. **Climb.** Stop at the first rung that holds: (1) skip (2) in-repo helper (3) stdlib (4) platform (5) installed dependency (6) one line (7) minimum new code. **Done when:** the chosen rung is named.
4. **Apply** the matching branch. **Done when:** that branch's criterion holds.
5. **Prove.** Smallest *red* check of observable behavior. Mock only at the trust boundary (network, clock, filesystem, paid API). Call through real internals. Trivial one-liners need no extra test. **Done when:** **write** — the check is red before the slice and green after; **refactor** / **improve** — the same check stays green.

## Branch write

Do the *simplest thing* that could work. One slice. A bug is one change at the shared root.

**Done when:** the requested behavior is observable; every new or rewritten function is **CC** ≤ 20 (or the project's bar); no type or file exists that this slice does not call.

## Branch refactor

Preserve behavior. Prefer deletion. Flatten with guard clauses before extract. Extract only with a responsibility name.

**Done when:** behavior matches the original (proof from Prove); every touched function is **CC** ≤ 20 (or the project's bar); a reader of the Match neighbor is faster; every extract or inline obeys **Balance**.

## Branch improve

Keep behavior. Remove the named hotspot. Ship the cheap fast path (stdlib, one pass, no N+1, no accidental quadratic). A cache, pool, or index only when that hotspot is measured or the user named it.

**Done when:** the named hotspot is gone; behavior matches the original (proof from Prove); no new type exists solely to hold the old slower path.

## Floor (every branch)

**KISS.** The *simplest thing* that could work. Essential path first. Types, files, knobs, and layers exist when this request uses them. Same-size options: the edge-case-correct one.

**DRY.** One authoritative representation per piece of knowledge. The second real duplicate earns extract; the first stays. Extract to a responsibility name. Copies that mean different things stay copies.

**YAGNI.** Build the need in this request. The extra caller, provider, or flag arrives with its own request.

**CC.** Decision points + 1 (`if`, loops, `case`, `catch`, `??`, `||`, `&&`, `.?`, boolean short-circuit, ternary). `else` = 0. Cap **20** on new or rewritten functions unless the project sets another bar (`eslint complexity`, ruff `C901`, gocyclo, etc). Keep branches visible (guard clauses, named predicates). A linear validation chain or a flat `switch` is not a split trigger. Use the project's existing complexity command when one exists.

**Match.** The diff follows naming, errors, imports, and function shape from the convention source Trace named. Personal preference loses. `conventions: none`: follow the Floor; do not invent a second style.

**Comment.** Concise comments that explain the operation. Follow the project's language comment convention.

**Breath.** Same-kind declarations stay together. A blank line sits between distinct blocks, after a closed `if`/`for`/`while`, and before `return`/`throw`. `else`, a continued line, and the `}` that closes the current block stay attached.

```js
const trimmed = input.trim();

if (!trimmed) {
  return '';
}

if (/^https?:\/\//i.test(trimmed)) {
  return trimmed;
}

for (let index = 0; index < array.length; index++) {
  const element = array[index];
}

return `${DEFAULT_SCHEME}${trimmed}`;
```

**Balance.** *intent* outranks *fewest*. A **DRY** extract that hides the idea loses to **KISS**. Keep the helper whose name still carries a concept. Split unrelated work. Fewer lines only when a reader of the Match neighbor is faster.

**Tight performance.** Default is the cheap fast path. Speculative optimization is **YAGNI** — that work belongs on **improve** with a named hotspot.

**Keep.** Understanding before the diff. Validation and fail-closed at trust boundaries. Errors that prevent data loss. Secrets and authorization. Accessibility. Platform calibration (clocks, sensors). Anything the user named. A non-trivial change with no *red* check is unfinished. An authorized corner that cuts a real limit: mark `ceiling: <limit>; upgrade: <path>`.

## Inform

Inform the user of the options and the consequences of each when the choice is sensitive architecture, a contract, data, or security. For a small reversible choice, pick the *simplest thing* and state the assumption.
