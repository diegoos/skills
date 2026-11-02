# Make code

Makes the code change you ask for with as little new code as possible. It uses what your project already has, adds nothing you did not ask for, and still updates every place the change touches.

Use it for any code edit: a new feature, a bug fix, a refactor, or a slow path. It does not write docs, agent instructions, skills, Makefiles, or CSS-only restyles, and it reviews code only when you ask for an edit.

## How it works

1. It reads the code the change touches and lists what the change must reach: callers, tests, fixtures, config, and exports.
2. It takes the first option that works: skip it, reuse code from the project, use the standard library or an installed dependency, write one clear line, or write the minimum new code. When existing code already does the job, it says so and edits nothing.
3. A bug fix goes to the root cause, so a guard that only hides the symptom does not count. A speed request starts from the slow spot you name or one it finds, such as an N+1 query.
4. New logic with a branch, a loop, a parser, money, or security gets one small test. A trivial change gets none. Your project's rules decide when its tests and linter run, and [`code-review-plus`](../code-review-plus/README.md) runs them on a fix.
5. The reply ends with what it skipped and any risk you should know.

## Code rules

- KISS, DRY, and YAGNI: the simplest path, one place for each decision, and nothing built for later, such as an interface with one implementation, a wrapper that only passes calls through, or an option nobody uses.
- New or rewritten functions stay at a cyclomatic complexity of 20 or less, unless your project sets its own limit.
- The code follows the naming, errors, imports, and structure of the code around it.
- Comments explain only the why that the code cannot show.
- A blank line goes before an `if` or loop that follows a declaration, before a `return` or `throw` that follows another statement, and after a closed block. This holds even when the rest of the file skips it.
- The first version is already cheap: no query or file read inside a loop, and a cache or index waits for a measured slow spot.
- It never cuts input validation, error handling that prevents data loss, security, accessibility, or anything you asked for, and it never silences the compiler or linter.

A shortcut with a known limit gets a `ceiling: <limit>; upgrade: <path>` comment in the code, and the reply repeats it.

## Files

- `SKILL.md`: the procedure.
- `agents/openai.yaml`: the picker name and invocation setting.
- `README.md`: this file.

## Related

[`code-review-plus`](../code-review-plus/README.md) reads this skill when it is installed, in its Quality hunter and its fix branch. Without it, the Quality hunter uses its own default rules, and the report says so.

## Install

```bash
npx skills add diegoos/skills --skill make-code
```

Then ask in plain language, for example "Add an endpoint that lists orders". The [root README](../../README.md) has more examples.
