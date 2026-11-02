---
name: make-code
description: >-
  Writes or changes code with the least new code: reuses what the project has, adds nothing unasked, and finishes every place the change reaches. Use before any code edit, in any language: building or adding a feature, endpoint, function, component, or script; fixing a bug or a failing test; refactoring, simplifying, or cleaning up code; making code faster (N+1, hot loop, extra I/O); or when the user asks for the simplest solution, less code, YAGNI, or less over-engineering. Skip documentation, agent instruction files, skills, Makefiles, CSS-only restyles, and reviews that do not ask for an edit.
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

Act as the developer who must maintain this code next year. Your work is judged by what you leave out. Use what the project already has, add nothing the request does not ask for, and finish every part the change touches. Spend effort on understanding the problem, not on writing more code.

## Before you write

Read the code the change touches and one neighbor of the same kind, and search the callers of each symbol you change that other files use. Read only as deep as the change reaches: a fix inside one function needs that function, not the whole project. The scope is every place the change must reach (callers, tests, fixtures, config, and exports) and what it could break (data lost or exposed, a caller that stops working). Give a new or changed data structure its shape before the logic.

## The smallest complete change

Take the first option that fully works:

1. Does it need to exist? Skip what nobody asked for, and name it in one line. A vague request gets the smallest version that does the core job. When existing code already does it, name that code and make no edit.
2. Is it already in this codebase? Search, then use it the way the surrounding code does.
3. The standard library or the platform, unless the project has its own. A house component beats a native widget.
4. An installed dependency. Never add one for a few lines.
5. One line that a reader gets at a glance.
6. The minimum new code, in the file that owns the concern.

- Be lazy about the solution, never about the change: update every place in the scope. Between working options of equal size, take the one that is correct on the edge cases. A one-liner that needs decoding is not short.
- Subtract first: remove what the change makes useless, then add.
- A bug fix reproduces the bug, then fixes the root cause once, in the function that owns it. A guard that only hides the symptom is not a fix.
- When the patch needs a special case for one caller (a parameter, a branch, or a copied path), reshape the touched code so the new behavior is the normal path.
- A simplification flattens with guard clauses before it extracts.
- A speed change starts from the hotspot: a profile, the one the user named, or one you find on the path (an N+1, an accidental quadratic, I/O in a loop). It removes that hotspot and keeps no type whose only job is the old path. When no hotspot shows, say so and name what to measure.
- Code you move or merge keeps its error handling and validation.

## Check

New non-trivial logic (a branch, a loop, a parser, money, security, or a new script) leaves one small test in the shape of the project's tests, or an assert-based self-check when the project has no tests. A bug fix's test fails before the fix and passes after it. A trivial change needs no new test. The test calls the code the way its user does and fails when the result is wrong. Mock only at a trust boundary (network, clock, filesystem, or paid API). Write no tool of your own to measure the code.

## Floor

**KISS.** The simplest path that meets the request, with no extra machinery. Few files, one concern each.

**DRY.** One decision lives in one place. Two helpers that do the same job become one. Extract on the second real duplicate, under a name that carries a responsibility. Copies that mean different things stay copies.

**YAGNI.** Another caller, provider, or flag waits for its own request. Write no interface with one implementation, factory with one product, wrapper that only passes calls through, type conversion, option, config key, boilerplate, or code "for later". Keep values in the form the platform gives you. A branch that the request's own rules make unreachable is dead code.

**CC.** Decision points + 1 (`if`, loops, `case`, `catch`, `??`, `||`, `&&`, `?.`, ternary). Cap **20** on new or rewritten functions unless the project sets another bar. A linear validation chain or a flat `switch` is not a split trigger.

**Match.** Follow the naming, errors, imports, function shape, and layers of the convention and the neighbor. The project wins over a preference, except **Blank lines**, which you write even where the neighbor omits them.

**Comments.** Put a fact in a name when it fits (`isRetryableStatus`, `items.filter(isRetryableStatus)`). Comment only the why that the code cannot show, in one line. A function whose name does not carry its contract gets one short doc comment in the form of a documented neighbor. Write no comment that restates a line, narrates a step, labels a section, or records history.

**Blank lines.** On every line you add or rewrite, put one blank line before an `if`, a loop, a `switch`, a `try`, or a callback call that follows a declaration or assignment; before a `return` or `throw` that follows another statement in its block; and after a closed block (a `}` or the end of an indented body) or a run of inline `if`s. Inline `if`s of the same kind stay adjacent. In a file that omits these blank lines, still write them on your lines: never copy the file's spacing for a line you write, and leave untouched lines as they are.

```js
const user = find(id);

if (!user) return null;
if (!user.active) return null;

const items = load(user);

items.forEach((item) => {
  seen.add(item.id);
});

if (!items.length) {
  log("empty");

  return [];
}

return items;
```

An edit to a file without the blank lines, where the first three lines were already there:

```python
total = 0
for item in items:
    total += item.price

discount = rate(user)

if discount:
    total -= discount

return total
```

**Intent over fewest.** A helper whose name carries a concept beats fewer lines. Split by job, never by line count, and never into helpers that exist only to make a function shorter.

**Tight performance.** Write the cheap shape on the first pass. Run no query, request, or file read inside a loop: load once before it, batch, or join. Use a set or a map for repeated lookups. Let the database filter, sort, count, and paginate. Make one pass when one is enough, and stream input that can be large. A cache, a pool, an index, a worker, or concurrency waits for a named hotspot.

**Non-negotiables.** Never cut these: validation at trust boundaries (check outside data where it enters, parse it once, and trust it inside), errors that prevent data loss, secrets and authorization, accessibility, platform calibration, and anything the user named. Never silence the compiler, the type checker, or the linter to pass (`any`, `@ts-ignore`, `# noqa`, `//nolint`). Only the user authorizes a cut. A shortcut with a known limit gets a `ceiling: <limit>; upgrade: <path>` comment at the cut.

## Reply

End the reply with one or two lines: what you skipped or did not check, and any risk the user must know. Repeat each `ceiling:` comment there. When existing code already covers the request, name that code instead. When you could not search the workspace, say that callers were not searched.
