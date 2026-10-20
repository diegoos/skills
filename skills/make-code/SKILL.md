---
name: make-code
description: >-
  Writes application code. Use when implementing or fixing a feature, endpoint, or function; simplifying or refactoring existing behavior; or speeding up a slow path (make it faster, N+1, hot loop, extra I/O). Skip when the task is documentation, an agent instruction file, a skill, a Makefile, a CSS-only restyle, or a review that does not ask for an edit.
metadata:
  version: 0.5.0
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

Write or change application code. Each run picks one branch and keeps the Floor.

Prefer the simplest, lightest, cheapest path that meets the request: less code, an existing tool, and no extra machinery. The Floor and the check still hold.

- New behavior (feature or fix) → **write**
- Same behavior, simpler, or faster on a named hotspot → **refactor**

## Inputs

- `request` (text, required): the behavior to add, the bug to fix, the code to simplify, or the slow path to speed up. It comes from the user message.
- `codebase` (files, required): the project the change lands in. It comes from the workspace.

## Steps

1. **Classify.** Pick the branch from the list above. **Done when:** the run states `write` or `refactor`. A faster run names the hotspot (a profile, an N+1, an accidental quadratic, extra I/O or allocation in a hot loop, or the name the user gave). A faster run that cannot name it leaves this step unfinished and uses the Output exit.
2. **Trace.** Fill the six fields. Search the workspace for every caller of each symbol the slice will change. A sensitive choice (architecture, contract, data, or security) names each option and its consequence, builds the simplest option that meets the request, and states that assumption. A small reversible choice states the assumption.

   - `problem`: the defect or the behavior, in one sentence
   - `entrypoints`: the paths the run will enter
   - `symbols`: each symbol the slice will change. A bug names the function that owns the defect
   - `callers`: every caller of those symbols, or `callers: none`. When workspace search is unavailable, shared symbols stay unedited and this field says the callers were not searched
   - `check`: the check that proves the slice
   - `convention`: the nearest `AGENTS.md` or `CLAUDE.md`, plus one neighbor of the same kind, or `conventions: none`. The doc that specifies this behavior, or `docs: none`

   **Done when:** `problem`, `entrypoints`, `symbols`, `callers`, `check`, and `convention` are filled, or the run names an existing symbol that already covers the request and stops with no edit. A sensitive choice names the options, the option built, and the assumption.
3. **Climb.** Before new code, answer whether this behavior already exists and whether an existing method already does this job. Stop at the first rung that holds: (1) skip (2) in-repo helper (3) stdlib (4) platform (5) installed dependency (6) one line (7) minimum new code. A new dependency is the last resort, after rung 5 fails. **Done when:** both answers and the chosen rung are named. Rung (2) names the helper. A rung past (2) names the methods searched. When workspace search is unavailable, that rung is the first that holds in the files already open, the line says the wider search did not run, and the run adds no dependency. A new dependency names the rung 5 search that failed. Rung (1) adds no new code.
4. **Apply** the matching branch under the Floor. **Done when:** that branch's criterion holds. KISS, CC, Match, and Blank lines hold on the slice. DRY, YAGNI, Comments, Intent over fewest, Tight performance, and Non-negotiables each hold, or the same line names that heading and why it is skipped.
5. **Prove.** Run the smallest check of observable behavior that fails when the logic breaks. Use the project's test command when one exists (package script, Makefile, or the neighbor's test). Otherwise use a plain assert or a self-check file. Mock only at a trust boundary (network, clock, filesystem, or paid API). Call the real internals. **Done when:** `write` shows the check red before the slice and green after. `refactor` shows that same check green before the edit and after it, and when none existed the run adds one that passes before the edit. A trivial one-liner states why it has no check. When the check cannot run, the run reports `check: not run` and the reason.

## Branch write

One slice of new behavior.

**Done when:** the requested behavior is observable; every new or rewritten function is within the CC cap; every new type and every new file is called by this slice.

## Branch refactor

Preserve behavior. Flatten with guard clauses before an extract. Extract only under a responsibility name.

**Done when:** the Prove check shows the same behavior as before the edit; every touched function is within the CC cap; each extract or inline keeps a name that carries the concept; a speed change removes the named hotspot and adds no type whose only job is to keep the old slower path.

## Floor (every branch)

**KISS.** The simplest, lightest, cheapest path that meets the request: less code, an existing tool, and no extra machinery. Essential path first. A type, a file, a knob, or a layer exists when this request uses it. Fewest files. When two options are the same size, pick the one that is correct on the edge. Deletion over addition. A smaller diff wins once the problem is understood.

**DRY.** One authoritative representation per piece of knowledge. The second real duplicate earns an extract; the first stays. Extract to a responsibility name. Copies that mean different things stay copies.

**YAGNI.** Build the need in this request. Add an abstraction only when a real caller in this request needs it. Another caller, provider, or flag waits for its own request.

**CC.** Decision points + 1 (`if`, loops, `case`, `catch`, `??`, `||`, `&&`, `.?`, boolean short-circuit, ternary). `else` = 0. Cap **20** on new or rewritten functions unless the project sets another bar (`eslint complexity`, ruff `C901`, gocyclo, or the project's complexity command). A linear validation chain or a flat `switch` is not a split trigger. Use the project's complexity command when one exists; otherwise count with this definition.

**Match.** The diff follows naming, errors, imports, and function shape from the convention source Trace named. The project's convention wins over a personal preference. `conventions: none`: follow the Floor and keep one style.

**Comments.** Put a fact in the identifier when it fits (`isRetryableStatus`). An inline callback is a named predicate (`items.filter(isRetryableStatus)`). A function or class whose name does not carry the contract gets one short doc comment: the contract, the units, the errors, or the side effect. Take the form from a documented neighbor of the same kind; with no neighbor, use the language standard (JSDoc, docstring, `///`, or godoc), one line on the purpose. A comment that stays states a constraint the name cannot carry. Leave out a comment that restates the line, narrates a step, labels a section, or records history.

**Blank lines.** A declaration or assignment and the `if` after it have one blank line between them. That holds for a brace body and for a same-line `return`. This blank line stays in the slice when a neighbor omits it. Consecutive inline `if`s of the same kind stay on adjacent lines and share that one leading blank line. A blank line separates that run from a following declaration, block, or `return`/`throw`. Same-kind declarations stay together. A blank line also separates a declaration or assignment from a following loop, `switch`, `try`, or callback call (`forEach`), and a closed block from the code after it. A `return` or `throw` that follows another statement in the same block has a blank line before it. A guard whose body is a diagnostic and a `return` or `throw` keeps those lines together. `else`, `catch`, `finally`, a continued line, and the `}` that closes the current block stay on the next line.

```js
const input = 'test';

if (input) {
  return input;
}

const flag = true;

if (flag) return flag;
if (!flag) return '';

const trimmed = input.trim();

if (!trimmed) {
  console.error('Empty input');

  return '';
}

items.forEach((item) => {
  seen.push(item.id);
});

return trimmed;
```

**Done when:** every declaration or assignment followed by an `if` has a blank line before that `if`, and every run of same-kind inline `if`s has no blank line inside the run.

**Intent over fewest.** Intent outranks fewest lines. This is the exception to **DRY**: a shared helper that hides the idea loses to a helper whose name still carries a concept. Split unrelated work. Fewer lines stay when the result still matches the neighbor's shape and the name still carries the concept.

**Tight performance.** The default path uses the stdlib, one pass, no N+1, and no accidental quadratic. A cache, a pool, or an index waits for a named hotspot. Speculative optimization is **YAGNI**.

**Non-negotiables.** Validation and fail-closed at trust boundaries. Errors that prevent data loss. Secrets and authorization. Accessibility. Platform calibration (clocks, sensors). Anything the user named. An authorized corner that cuts a real limit is marked `ceiling: <limit>; upgrade: <path>`.
