# Make code

Writes, simplifies, and speeds up application code. Each run picks one branch and works through five steps.

## Branches

| Branch | Use it for | Done when |
| --- | --- | --- |
| write | A feature, endpoint, function, or bug fix | The behavior is observable, and new functions stay under the CC cap |
| refactor | The same behavior, simpler | Behavior matches the original, and touched functions stay under the CC cap |
| refactor with a hotspot | The same behavior, faster, on a named or measured hotspot | The hotspot is gone, and no new type exists only for the old slow path |

The skill does not cover docs, agent instructions, Makefiles, or CSS-only restyles.

## Steps

1. Classify. Pick the branch. A speed run needs a named hotspot, such as a profile result, an N+1 query, or extra I/O in a hot loop. Without one, use refactor or ask.
2. Trace. Name the problem, the entry points, the symbols that change, and every caller. Read the local conventions in the nearest `AGENTS.md` or `CLAUDE.md` and in one neighboring file. Fix a bug at its shared function. Check first whether the code needs to exist.
3. Climb. Before new code, try each rung in order: skip, an in-repo helper, the standard library, the platform, an installed dependency, one line, then minimum new code. A new dependency is the last resort.
4. Apply. Write the change under the Floor rules below.
5. Prove. Run the smallest check of observable behavior that fails when the logic breaks. A write run goes red, then green. A refactor stays green.

## The Floor

- KISS: the simplest thing that works. Boring code, fewer files, deletion over addition.
- DRY: one representation per piece of knowledge. Extract on the second real duplicate. Copies that mean different things stay separate.
- YAGNI: build what the request needs, nothing for a future caller.
- CC: decision points plus one. The cap is 20 for new or rewritten functions, unless the project sets its own limit.
- Match: follow the naming, errors, imports, and shape of neighboring code.
- Comments: add a doc comment only when a name cannot carry the contract. Skip comments that repeat the code or label sections.
- Blank lines: separate a declaration from a following block, a block from the code after it, and any statement from `return` or `throw`.
- Intent over fewest: keep a helper when its name carries a concept. Shorter code wins only when neighbors read faster.
- Tight performance: the cheap fast path by default. Caches, pools, and indexes wait for a measurement.
- Non-negotiables: understand before changing, validate at trust boundaries, keep errors that prevent data loss, protect secrets and authorization, keep accessibility and platform calibration, and honor what you named. A non-trivial change needs a check that fails when it breaks.

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
