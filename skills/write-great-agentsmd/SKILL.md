---
name: write-great-agentsmd
description:
  Generate, update, or lint an AGENTS.md file — the operational policy that
  orchestrates an AI agent inside a repo. Use when the user asks to create,
  write, generate, scaffold, refresh, update, fix, audit, or review an
  AGENTS.md (or tool-mirror files like CLAUDE.md / .cursor/rules / GEMINI.md),
  wants to make an existing one more agent-effective, or mentions reducing
  agent drift, token cost, or false "done" reports. Branches: bootstrap (new),
  update (post-change sync), lint (health-check).
---

# Write a great AGENTS.md

An `AGENTS.md` is **operational policy** for an AI agent, not documentation for
humans. Its root is an **orchestrator** — a short index that points at a small
wiki of topic docs the agent maintains, in the spirit of an LLM-wiki: knowledge
compiled once and kept current, never re-derived each run. The root points at
topic docs rather than duplicating them.

Work in **three branches**, picked from the user's ask — record your pick at the
start of the run:

- create / write / generate / scaffold → **bootstrap** — analyse the repo, emit
  root `AGENTS.md` (and topic docs where the repo earns them).
- refresh / update / fix → **update** — at the end of a run that touched the
  repo, propose scoped edits to the topic docs touched by the change
  (anti-drift).
- audit / review → **lint** — health-check the whole `AGENTS.md` layer; report
  only, do not edit.

State the target behaviour so the banned one is never spoken. Pattern catalogue
(what works, what gets ignored, by theme) lives in [`PATTERNS.md`](PATTERNS.md)
— reach for it when you want a concrete example or need to diagnose a smell.

## Principles (the policy every output must hold)

- **Command-first.** Every instruction is a runnable command with args, or an
  observable condition. Prose with no command is a suggestion the agent skips.
- **Closure-defined.** Each `When …` section names the exit codes that prove
  done, plus the proof artifact the PR must carry (a failing test added first
  then passing, a snapshot, or a runnable demo). No "I think I'm done."
- **Task-organized.** Group by task (`When Writing`, `When Reviewing`,
  `When Releasing`), not by category (style, testing, deployment).
- **Permission boundaries.** State READ / WRITE / NEVER paths and any
  HUMAN_CHECKPOINT actions up front. The agent stays inside the boundary; what
  is not listed is not permitted.
- **Escalation.** State what the agent does when blocked — including the hard
  guardrails it must never cross to "recover."
- **Precedence.** Where rules trade off, number them; never leave the agent to
  guess which wins.
- **Minimal-high-leverage.** Write only what the agent cannot infer from code,
  tests, and configs: historical decisions, tradeoffs, tempting anti-patterns,
  edge cases, migrations in progress, implicit constraints, and non-functional
  constraints (security, performance) phrased prescriptively ("All SQL queries
  must use parameterized statements", not "be secure"). Skip structure the agent
  can see by listing the tree.
- **Link, don't copy.** Point at source, tests, configs. Duplication drifts.

## Branch A — bootstrap

1. **Recon the repo.** Stack, test runner, linter/formatter, build, type
   checker, CI, entrypoints, monorepo? Record path-based facts (`cmd/`,
   `tests/`, config paths), not narrative.
2. **Decide the layout** by repo size — a judgement call: record the size
   verdict and one-line reason before proceeding.
   - **small** — one service, stable patterns, narrow constraints: a single
     `AGENTS.md` that acts as an index, pointing straight at `cmd/`, `tests/`,
     and configs instead of describing them. No topic docs yet.
   - **medium / large** — multi-service, monorepo, or many concerns: root
     `AGENTS.md` (orchestrator) **plus** topic docs — `architecture.md`,
     `conventions.md`, `testing.md`, `releasing.md`, `pitfalls.md` as relevant.
     Root links; topics own the detail.
   - **monorepo (hierarchical scoping)** — place a root `AGENTS.md` with shared
     rules (git workflow, CI, cross-cutting conventions) and one `AGENTS.md` per
     service/package holding only what differs (test runner, lint config,
     build). Nearest file wins; a child file never restates a rule the parent
     already owns — it overrides by omission or by naming the replacement.
3. **Inventory the high-leverage.** List only what is _not_ inferable from the
   repo: architectural decisions and why, tradeoffs (why slower-for-correctness
   was chosen), tempting anti-patterns that regress, edge cases needing special
   handling, migrations in progress, non-functional constraints (security,
   performance) the agent could silently violate, and — if the repo depends on
   external APIs or docs with non-obvious access patterns — the `llms.txt` /
   `.md`-URL / `raw.githubusercontent.com` patterns that let the agent reach
   them without guessing. Each item lands in exactly **one** place.
4. **Emit.** Root + topic docs (if any). Commands verbatim. `When …` sections
   with closure and proof artifact. Escalation block. Numbered precedence where
   rules trade off. A **Permission boundaries** section listing READ / WRITE /
   NEVER paths and any HUMAN_CHECKPOINT actions. Generate mirror files
   (`CLAUDE.md`, `.cursor/rules`, `GEMINI.md`) only when the user's tools need
   them, as thin mirrors that stay in sync with the root.
5. **Verify (completion criterion — exhaustive):**
   - Every build/test/lint command in the output has been **run in this repo**,
     exit code recorded. If one fails, report and ask rather than invent a
     replacement silently.
   - Root ≤ ~80 lines (hard ceiling ~150 total; tools truncate at ~32 KiB).
   - Every item from step 3 is placed — none left orphan.
   - Cut any README narrative, welcoming prose, or redundancy-vs-README. Run the
     no-op test per paragraph: if it only says "project X is…", cut it. Lint
     before you re-emit — cut what the repo no longer does.
   - Single source of truth: each concept lives in one place (root or topic doc,
     not both); the root points.
   - A Permission boundaries section is present, naming READ / WRITE / NEVER
     paths and any HUMAN_CHECKPOINT actions.

## Branch B — update (anti-drift)

At the end of a run that changed the repo, before reporting done:

1. List the concerns touched (modules, CI, conventions, deployment).
2. For each concern, find its topic doc. If it exists, propose a scoped edit as
   a small, reviewable diff; rewrite the whole file only when the structure
   itself is broken. If it doesn't, decide: create a new topic doc only if the
   concern is high-leverage and recurrent; otherwise record
   `no doc change needed` with a one-line reason.
3. Link to the changed source rather than restating it; update cross-references
   the change broke. Propagate the same edits to any mirror files (`CLAUDE.md`,
   `.cursor/rules`, `GEMINI.md`) generated in bootstrap so they stay in sync
   with the root.
4. **Verify (completion criterion — exhaustive):**
   - Every touched concern has either a proposed edit or a justified
     `no doc change needed`.
   - Each concept lives in one place; an item already owned by a topic doc stays
     out of the root.
   - Every mirror file matches its root section verbatim where mirrored.
   - No new command added without having been run with exit code recorded.

## Branch C — lint (report only)

1. Run every command the layer lists; record each exit code. Any non-zero is
   `stale command drift`.
2. Walk each architectural / routing / module claim; confirm it still exists in
   the code. Report drift line by line, citing both the doc line and the code.
   Do the same for external doc links — a broken `llms.txt`, 404'd docs URL, or
   moved page counts as drift.
3. Cross-references between topic docs: orphans (no inbound links), missing (a
   frequently cited concept with no page), contradictions (two pages that
   disagree).
4. Every `When …` section has a closure definition (exit code plus proof
   artifact)? Flag the ones without. Confirm a Permission boundaries section
   exists and still matches the real READ / WRITE / NEVER paths.
5. Compare each mirror file (`CLAUDE.md`, `.cursor/rules`, `GEMINI.md`) against
   the root section it mirrors; flag any drift.
6. **Verify (completion criterion — exhaustive):**
   - Every command executed, exit code recorded.
   - Every contradiction listed with both sources cited.
   - Every orphan and missing cross-reference signalled.
   - Every missing closure flagged.
   - Every mirror file matches its root source, or the mismatch is reported.
   - A report was produced; no file was edited.
