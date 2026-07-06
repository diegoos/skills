# write-great-agentsmd

Generates, updates, and audits `AGENTS.md` — the **operational policy** that
orchestrates an AI agent inside a repo.

## What it does

`AGENTS.md` is not human documentation. It's executable policy: verbatim
commands, closure criteria, permission boundaries, escalation when blocked. This
skill produces that file by maintaining a small wiki of topic docs the agent
owns (llm-wiki pattern).

Three operation branches:

| Branch        | When to use                        | What it does                                              |
| ------------- | ---------------------------------- | --------------------------------------------------------- |
| **bootstrap** | create/write/generate from scratch | Analyse the repo, inventory high-leverage, emit root+docs |
| **update**    | after a change to the repo         | Sync topic docs touched by the change (anti-drift)        |
| **lint**      | audit/review existing `AGENTS.md`  | Health-check: drift, stale commands, contradictions       |

## Files

- `SKILL.md` — the skill itself: branches, principles, exhaustive completion
  criteria.
- `PATTERNS.md` — catalogue of what works vs. anti-patterns, co-located by
  theme. Consulted on demand.

## Principles every output must hold

- **Command-first** — every instruction is a runnable command, not prose.
- **Closure-defined** — exit codes + proof artifact (failing test now passing,
  snapshot, demo).
- **Task-organized** — grouped by task (`When Writing / Reviewing / Releasing`).
- **Permission boundaries** — `READ` / `WRITE` / `NEVER` / `HUMAN_CHECKPOINT`.
- **Escalation** — what to do when blocked; what never to do to "recover".
- **Precedence** — numbered tradeoffs; the agent never guesses which wins.
- **Minimal-high-leverage** — only what the agent cannot infer from code
  (decisions, tradeoffs, non-functional constraints).
- **Link, don't copy** — point at source; duplication drifts.

## Usage

Invoke via model description (model-invoked):

```text
create/write/generate an AGENTS.md → bootstrap
refresh/update/fix → update
audit/review → lint
```

Or by the skill name in tools that support direct invocation.
