# Survey

Collect evidence. Do not write `docs/`. Read existing docs first (README, `docs/`, `AGENTS.md`, `CONTRIBUTING.md` if present).

## Size verdict

Record one size before dispatch:

- **small:** one service or library, few entry points, stable layout. Orchestrator surveys itself. Record `hunters: none`. Skip the hunter dispatch.
- **medium / large:** several packages, multiple entry points, or a non-trivial deploy graph. Dispatch all three hunters.
- **monorepo:** more than one deployable or publishable unit with its own boundary. Dispatch all three hunters. Nearest `docs/` wins per unit after confirm.

Cite one fact for the verdict (package count, `cmd/` binaries, workspace members). The verdict is confirm material, not a sentence in `docs/`.

## Dispatch (medium / large / monorepo)

Launch **up to 3** hunters in parallel. Same model as the orchestrator. Read-only. One hunter file each.

| Hunter | Path |
| ------ | ---- |
| structure | `./references/hunters/structure.md` |
| behavior | `./references/hunters/behavior.md` |
| voice | `./references/hunters/voice.md` |

On **update** with a scoped diff, pass changed paths in the brief and still use these hunter files (omit a hunter whose lens has no changed path).

Orchestrator-only (never hunter paths): `./references/anti-slop.md`, `./references/language.md`, `./references/examples/`, `./references/template-*.md`, `./references/phases/confirm.md`, `generate.md`, `verify.md`.

## Serial fallback (no subagent)

If the harness has no subagent, run the three hunters **in series**. Record `serial: yes`.

**Carry pack.** After each hunter returns, append its YAML to a running pack. Restate the **full** pack before starting the next hunter. Auto-compact drops earlier hunts: restore from the restated pack first. Mid-series with an empty pack is a failed survey; rebuild from the last restated block.

## Subagent prompt template

```txt
Survey this repository from the [HUNTER] lens only.

Brief (from orchestrator):
[size verdict + entry paths + monorepo units if any + existing-docs paths + optional changed-path scope]

Reference (read ONLY this path, then read the codebase):
- [hunter path]

Return the YAML schema from that hunter file. Cite paths. Put anything the code does not show in unknowns. Invent no quality numbers, no SLO, no API that is not in the tree.

Do not write files under docs/. Do not open other files under references/. Read-only. Same model as the orchestrator.
```

## Evidence pack (orchestrator merge)

After hunters return (or after the solo small survey), the orchestrator holds:

- size verdict + one-line evidence
- `hunters: structure+behavior+voice` or `hunters: none` (and `serial: yes` when used)
- structure, behavior, and voice YAML (solo survey fills the same fields)
- existing-docs list (paths read)
- out-of-scope detections (data model, observability, CI/CD) as unknowns when present

## Completion criterion

Size verdict recorded with one cited fact. Existing docs read. Evidence pack holds stack, runtime, entry points, deploy (or `unknown`), auth only if present, every behavioral domain named by feature, voice language candidate with sources, and an `unknowns` list. Every hunter required by the size has returned, or `hunters: none` is recorded for small.
