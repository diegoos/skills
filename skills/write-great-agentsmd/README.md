# write-great-agentsmd

Generates, updates, and audits `AGENTS.md` — the **operational policy** that orchestrates an AI agent inside a repo.

## What it does

`AGENTS.md` is not human documentation. It's executable policy: verbatim commands, closure criteria, permission boundaries, escalation when blocked. This skill produces that file by maintaining a small wiki of topic docs the agent owns (llm-wiki pattern).
Every token in the root loads on **every request** — the skill treats the root as an instruction budget (~150–200 instructions for frontier models). Keep the root minimal; push detail to topic docs, nested `AGENTS.md` files, or agent skills.
Four operation branches:

| Branch        | When to use                                      | What it does                                                             |
| ------------- | ------------------------------------------------ | ------------------------------------------------------------------------ |
| **bootstrap** | create/write/generate from scratch               | Analyse the repo, inventory high-leverage, emit root+docs                |
| **update**    | after a change to the repo                       | Sync topic docs touched by the change (anti-drift)                       |
| **lint**      | audit/review existing `AGENTS.md`                | Health-check: drift, stale commands, contradictions, deletion candidates |
| **slim**      | refactor / progressive disclosure / bloated file | Extract essentials, group rest into topic docs, flag deletions           |

## Files

- `SKILL.md` — the skill itself: branches, principles, exhaustive completion criteria.
- `PATTERNS.md` — catalogue of what works vs. anti-patterns, co-located by theme. Consulted on demand.

## Principles every output must hold

- **Command-first** — every instruction is a runnable command, not prose.
- **Closure-defined** — exit codes + proof artifact (failing test now passing, snapshot, demo).
- **Task-organized** — grouped by task (`When Writing / Reviewing / Releasing`).
- **Permission boundaries** — `READ` / `WRITE` / `NEVER` / `HUMAN_CHECKPOINT`.
- **Escalation** — what to do when blocked; what never to do to "recover".
- **Precedence** — numbered tradeoffs; the agent never guesses which wins.
- **Instruction budget** — root holds only what applies to every task; rest → topic docs / skills.
- **Link, don't copy** — point at source; duplication drifts.

## Tool mirrors

Prefer `ln -s AGENTS.md CLAUDE.md` over copy mirrors — one source of truth, zero sync drift. Thin copy mirrors only when symlinks are impossible.

## Usage

Invoke via model description (model-invoked):

```text
create/write/generate an AGENTS.md → bootstrap
refresh/update/fix → update
audit/review → lint
slim/refactor/progressive disclosure → slim
```

Or by the skill name in tools that support direct invocation.
