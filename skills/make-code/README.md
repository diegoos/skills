# Make code

Writes, simplifies, and speeds up application code. Each run picks one branch and works through five steps.

## Branches

| Branch | Use it for | Done when |
| --- | --- | --- |
| write | A feature, endpoint, function, or bug fix | The behavior is observable, and new functions stay under the CC cap |
| refactor | The same behavior, simpler | Behavior matches the original, and touched functions stay under the CC cap |
| refactor with a hotspot | The same behavior, faster, on a named or measured hotspot | The hotspot is gone, and no new type exists only for the old slow path |

The skill does not cover docs, agent instructions, skills, Makefiles, CSS-only restyles, or a review that does not ask for an edit.

## Steps

1. Classify. Pick the branch. A speed run needs a named hotspot, such as a profile result, an N+1 query, or extra I/O in a hot loop. Without one, ask once which limit to remove and make no edit until the user names it. Stop when the run cannot ask.
2. Trace. Fill six fields: problem, entrypoints, symbols, callers, check, and convention. When an existing symbol already covers the request, stop with no edit.
3. Climb. Before new code, try each rung in order: skip, an in-repo helper, the standard library, the platform, an installed dependency, one line, then minimum new code. A new dependency is the last resort. When workspace search is unavailable, the rung comes from files already open, the run says the wider search did not run, and it adds no dependency.
4. Apply. Write the change under the Floor. KISS, CC, and Match hold. Any other Floor heading that does not apply names itself and the reason on the same line.
5. Prove. Run the smallest check of observable behavior that fails when the logic breaks. A write run goes red, then green. A refactor stays green before the edit and after it.

The run ends with one line: `branch | rung | check`.

## The Floor

- KISS: the simplest, lightest, cheapest path that meets the request. Less code, an existing tool, and no extra machinery.
- DRY: one representation per piece of knowledge. Extract on the second real duplicate. Copies that mean different things stay separate.
- YAGNI: build what the request needs, nothing for a future caller.
- CC: decision points plus one. The cap is 20 for new or rewritten functions, unless the project sets its own limit.
- Match: follow the naming, errors, imports, and shape of neighboring code.
- Comments: add a doc comment only when a name cannot carry the contract. Skip comments that repeat the code or label sections.
- Blank lines: a declaration or assignment has a blank line before the following `if`, braced or on one line. Consecutive inline `if`s stay on adjacent lines. A blank line also separates a block from the code after it, and a statement from `return` or `throw`. A guard that only logs and returns keeps those two lines together.
- Intent over fewest: keep a helper when its name carries a concept. Fewer lines stay when the result still matches the neighbor and the name still carries the concept.
- Tight performance: the cheap fast path by default. Caches, pools, and indexes wait for a named hotspot.
- Non-negotiables: validate at trust boundaries, keep errors that prevent data loss, protect secrets and authorization, keep accessibility and platform calibration, and honor what you named.

When a shortcut cuts a real limit, mark it with a `ceiling: <limit>; upgrade: <path>` comment.

## Files

- `SKILL.md`: the procedure.
- `agents/openai.yaml`: the picker name and invocation setting.
- `README.md`: this file.

## Related

[`code-review-plus`](../code-review-plus/README.md) reads this skill when it is installed, in its Quality hunter and fix branch. Without it, the Quality hunter uses its own default Floor, and the report says so.

## Install

```bash
npx skills add diegoos/skills --skill make-code
```

Then ask in plain language, for example "Add an endpoint that lists orders". The [root README](../../README.md) has more examples.
