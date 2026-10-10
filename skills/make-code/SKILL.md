---
name: make-code
description: >-
  Write application code. Use when implementing or fixing a feature, endpoint, or function; simplifying existing behavior; or speeding up a named hotspot (N+1, hot loop, extra I/O). Skip docs, agent instructions, Makefiles, and CSS-only restyles.
metadata:
  version: 0.4.0
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

Think like a lazy senior developer. Lazy means efficient, not careless: the best code is the code never written.

Create application code under **KISS**, **DRY**, **YAGNI**, and **CC**. **KISS** is the path. **DRY** is one representation, earned. **YAGNI** is the stop. **CC** is the local ceiling.

Pick a **branch** and state it at the start of the run:

- new behavior (feature, fix) → **write**
- same behavior, simpler → **refactor**
- same behavior, faster → **refactor** with a named hotspot (see Tight performance)

## Workflow

1. **Classify.** Branch from the request. A speed request needs a named hotspot (profile, N+1, accidental quadratic, extra I/O or alloc in a hot loop, or the user named it); none → **refactor**, or ask. **Done when:** the branch is named; a speed change cites the hotspot.
2. **Trace.** Name the problem and the entrypoints. Name the symbols you will change. Search every caller. Name the check that proves the change, and the convention source (nearest `AGENTS.md` / `CLAUDE.md` and one neighbor of the same kind, or `conventions: none`). Read existing docs. A bug is fixed at its shared root, not at the one caller the report names: fix the shared function once. Ask first: does this need building at all, or does something existing cover it? For a sensitive choice (architecture, contract, data, security), inform the user of each option and its consequences before building; for a small reversible choice, pick the simplest and state the assumption. **Done when:** the items that apply to this task are named (a bug needs callers; a feature needs entrypoints), or **YAGNI** stops the work.
3. **Climb.** Before new code, answer: does this already exist, does an existing method already do this job. Stop at the first rung that holds: (1) skip (2) in-repo helper (3) stdlib (4) platform (5) installed dependency (6) one line (7) minimum new code. A new dependency is the last resort, after rung 5 fails. **Done when:** the two answers are named and the chosen rung is named. A rung past (2) names the methods searched.
4. **Apply** the matching branch under Floor. **Done when:** that branch's criterion holds and **Comments** holds on the slice.
5. **Prove.** Smallest check of observable behavior that fails if the logic breaks. Mock only at the trust boundary (network, clock, filesystem, paid API). Call through real internals. Trivial one-liners need no test. A non-trivial change leaves one runnable check: a plain assert or self-check file. **Done when:** with observable behavior, **write** shows the check red before the slice and green after; **refactor** keeps the same check green; without observable behavior, the check fails when the logic breaks.

## Branch write

Do the *simplest thing* that could work. One slice.

**Done when:** the requested behavior is observable; every new or rewritten function meets the **CC** cap; no type or file exists that this slice does not call.

## Branch refactor

Preserve behavior. Flatten with guard clauses before extract. Extract only with a responsibility name.

**Done when:** behavior matches the original (proof from Prove); every touched function meets the **CC** cap; a reader of the Match neighbor is faster; every extract or inline obeys **Intent over fewest**; for a speed change, the named hotspot is gone and no new type exists solely to hold the old slower path.

## Floor (every branch)

**KISS.** The *simplest thing* that could work. Essential path first. Types, files, knobs, and layers exist when this request uses them. Boring over clever. Fewest files. Same-size options: the edge-case-correct one. Deletion over addition. A smaller diff wins only once the problem is understood; a small change in the wrong place is a second bug.

**DRY.** One authoritative representation per piece of knowledge. The second real duplicate earns extract; the first stays. Extract to a responsibility name. Copies that mean different things stay copies.

**YAGNI.** Build the need in this request. Add an abstraction only when a real caller needs it. The extra caller, provider, or flag arrives with its own request.

**CC.** Decision points + 1 (`if`, loops, `case`, `catch`, `??`, `||`, `&&`, `.?`, boolean short-circuit, ternary). `else` = 0. Cap **20** on new or rewritten functions unless the project sets another bar (`eslint complexity`, ruff `C901`, gocyclo, etc). Keep branches visible (guard clauses, named predicates). A linear validation chain or a flat `switch` is not a split trigger. Use the project's existing complexity command when one exists.

**Match.** The diff follows naming, errors, imports, and function shape from the convention source Trace named. Personal preference loses. `conventions: none`: follow the Floor and keep one style.

**Comments.** Add a comment only when the code cannot say it. A function or class whose contract its name does not carry gets one short doc comment: the contract, the units, the errors, or the side effect. Form comes from a documented neighbor of the same kind; with no neighbor, the language standard (JSDoc, docstring, `///`, godoc), one line on purpose. A conditional comment states a constraint the name cannot carry. A fact that fits in an identifier is an identifier (`isRetryableStatus`) and needs no comment. Skip comments that restate the code, narrate steps, label sections, or record history; skip comments on obvious lines and on helpers whose name already states the contract. An inline callback is a named predicate (`items.filter(isRetryableStatus)`).

**Blank lines.** Same-kind declarations stay together. A blank line separates a declaration or assignment from a block (`if`, loop, `switch`, `try`, or a callback call such as `forEach`), a closed block from the code after it, and any statement from `return`/`throw`. `else`, `catch`, `finally`, a continued line, and the `}` that closes the current block stay attached.

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

```ts
let hasValidItem = false

items.forEach((item) => {
  hasValidItem ||= item.isValid
})

const container = document.querySelector<HTMLElement>(containerSelector)

if (!container) {
  console.error('Container not found:', containerSelector)
  return
}

items = container.querySelectorAll<HTMLElement>(ITEM_SELECTOR)

if (items.length === 0) {
  console.error('No items found.')
  return
}
```

**Intent over fewest.** *Intent* outranks *fewest*. The one exception to **DRY**: a shared helper that hides the idea loses; keep the helper whose name still carries a concept. Split unrelated work. Fewer lines only when a reader of the Match neighbor is faster.

**Tight performance.** Default is the cheap fast path: stdlib, one pass, no N+1, no accidental quadratic. Speed work runs only on a named hotspot, measured or named by the user. A cache, pool, or index waits for that measurement. Speculative optimization is **YAGNI**.

**Non-negotiables.** Understanding before the diff. Validation and fail-closed at trust boundaries. Errors that prevent data loss. Secrets and authorization. Accessibility. Platform calibration (clocks, sensors). Anything the user named. A non-trivial change needs a check that fails when it breaks. An authorized corner that cuts a real limit: mark `ceiling: <limit>; upgrade: <path>`.
