---
name: write-great-agentsmd
description: >-
  Generate, update, or lint an AGENTS.md file — the operational policy that orchestrates an AI agent inside a repo. Use when the user asks to create, write, generate, scaffold, refresh, update, fix, audit, or review an AGENTS.md (or tool-mirror files like CLAUDE.md / .cursor/rules / GEMINI.md), wants to make an existing one more agent-effective, or mentions reducing agent drift, token cost, or false "done" reports. Branches: bootstrap (new), update (post-change sync), lint (health-check), slim (refactor bloated file).
---

# Write a great AGENTS.md

An `AGENTS.md` is **operational policy** for an AI agent, not documentation for humans. Its root is an **orchestrator** — a short index that points at a small wiki of topic docs the agent maintains, in the spirit of an LLM-wiki: knowledge compiled once and kept current, never re-derived each run. The root points at topic docs rather than duplicating them.

Every token in the root loads on **every request** — treat it as an instruction budget. Frontier models follow ~150–200 instructions with reasonable consistency; smaller models attend to fewer. Keep the root as small as possible; push detail to topic docs, nested `AGENTS.md` files, or agent skills (pulled on demand).

Work in **four branches**, picked from the user's ask — record your pick at the start of the run:

- create / write / generate / scaffold → **bootstrap** — analyse the repo, emit root `AGENTS.md` (and topic docs where the repo earns them).
- refresh / update / fix → **update** — at the end of a run that touched the repo, propose scoped edits to the topic docs touched by the change (anti-drift).
- audit / review → **lint** — health-check the whole `AGENTS.md` layer; report only, do not edit.
- slim / refactor / progressive disclosure → **slim** — shrink a bloated `AGENTS.md` by extracting essentials, grouping the rest into topic docs, and flagging instructions for deletion.

State the target behaviour so the banned one is never spoken. Pattern catalogue (what works, what gets ignored, by theme) lives in [`PATTERNS.md`](PATTERNS.md) — reach for it when you want a concrete example or need to diagnose a smell.

## Principles (the policy every output must hold)

- **Command-first.** Every instruction is a runnable command with args, or an observable condition. Prose with no command is a suggestion the agent skips.
- **Closure-defined.** Each `When …` section names the exit codes that prove done, plus the proof artifact the PR must carry (a failing test added first then passing, a snapshot, or a runnable demo). No "I think I'm done."
- **Task-organized.** Group by task (`When Writing`, `When Reviewing`, `When Releasing`), not by category (style, testing, deployment).
- **Permission boundaries.** State READ / WRITE / NEVER paths and any HUMAN_CHECKPOINT actions up front. The agent stays inside the boundary; what is not listed is not permitted.
- **Escalation.** State what the agent does when blocked — including the hard guardrails it must never cross to "recover."
- **Precedence.** Where rules trade off, number them; never leave the agent to guess which wins.
- **Instruction budget / minimal-high-leverage.** The root holds only what applies to **every single task**; everything else lives in a topic doc, nested `AGENTS.md`, or an agent skill. Write only what the agent cannot infer from code, tests, and configs: historical decisions, tradeoffs, tempting anti-patterns, edge cases, migrations in progress, implicit constraints, and non-functional constraints (security, performance) phrased prescriptively ("All SQL queries must use parameterized statements", not "be secure"). Prefer capabilities and domain concepts over file-path inventories — paths drift; concepts are more stable. Skip structure the agent can see by listing the tree. Do not fill with generic rules "useful for most scenarios" without evidence in the repo; omit rather than pad.
- **Link, don't copy.** Point at source, tests, configs. Duplication drifts.
- **Progressive disclosure via skills.** Repeatable workflows (release, security review, doc sync) belong in agent skills the agent invokes on demand — not in the root.

## Root essentials (the floor every bootstrap / slim must include)

1. **One-liner** — exactly one sentence anchoring the agent's role in this repo (e.g. "This is a React component library for accessible data visualization.").
2. **Package manager** — if not npm, state it explicitly (e.g. "This project uses pnpm workspaces."). `corepack` is an acceptable alternative when enabled.
3. **Build / test / typecheck commands** — verbatim, non-obvious only (skip `npm test` when `package.json` already defines it).
4. **Always-relevant operational blocks** — Permission boundaries, Escalation, and Precedence (when rules trade off).

Everything else → topic doc, nested `AGENTS.md`, or skill.

## Branch A — bootstrap

1. **Recon the repo.** Stack, test runner, linter/formatter, build, type checker, CI, entrypoints, monorepo? Record **capabilities and domain concepts** with a light touch (e.g. "billing replays from outbox, not queue"). Use short path pointers (`see cmd/`, `see tests/`) — never a directory inventory or narrative.
2. **Decide the layout** by repo size — a judgement call: record the size verdict and one-line reason before proceeding.
   - **small** — one service, stable patterns, narrow constraints: a single `AGENTS.md` that acts as an index, pointing straight at `cmd/`, `tests/`, and configs instead of describing them. No topic docs yet.
   - **medium / large** — multi-service, monorepo, or many concerns: root `AGENTS.md` (orchestrator) **plus** topic docs — `architecture.md`, `conventions.md`, `testing.md`, `releasing.md`, `pitfalls.md` as relevant. Root links; topics own the detail.
   - **monorepo (hierarchical scoping)** — place a root `AGENTS.md` with shared rules (git workflow, CI, cross-cutting conventions) and one `AGENTS.md` per service/package holding only what differs (test runner, lint config, build). Nearest file wins; a child file never restates a rule the parent already owns — it overrides by omission or by naming the replacement. The agent sees all merged `AGENTS.md` files — keep each level focused.
3. **Inventory the high-leverage.** List only what is _not_ inferable from the repo: architectural decisions and why, tradeoffs (why slower-for-correctness was chosen), tempting anti-patterns that regress, edge cases needing special handling, migrations in progress, non-functional constraints (security, performance) the agent could silently violate, and — if the repo depends on external APIs or docs with non-obvious access patterns — the `llms.txt` / `.md`-URL / `raw.githubusercontent.com` patterns that let the agent reach them without guessing. Each item lands in exactly **one** place. Do not auto-generate a comprehensive dump of generic best practices.
4. **Emit.** Root + topic docs (if any). Include the **root essentials** (see above). Commands verbatim. `When …` sections with closure and proof artifact. Escalation block. Numbered precedence where rules trade off. A **Permission boundaries** section listing READ / WRITE / NEVER paths and any HUMAN_CHECKPOINT actions. For tool mirrors (`CLAUDE.md`, `GEMINI.md`): prefer `ln -s AGENTS.md CLAUDE.md` when the user's tools support symlinks — one source of truth, zero sync drift. Use thin copy mirrors only when symlinks are impossible in the environment. Generate `.cursor/rules` only when needed.
5. **Verify (completion criterion — exhaustive):**
   - Every build/test/lint command in the output has been **run in this repo**, exit code recorded. If one fails, report and ask rather than invent a replacement silently.
   - Root ≤ ~80 lines (hard ceiling ~150 total; tools truncate at ~32 KiB).
   - Every item from step 3 is placed — none left orphan.
   - Cut README narrative, welcoming prose, or redundancy-vs-README. Allow **exactly one sentence** as the project one-liner; cut any further "project X is…" prose. Lint before you re-emit — cut what the repo no longer does.
   - Single source of truth: each concept lives in one place (root or topic doc, not both); the root points.
   - A Permission boundaries section is present, naming READ / WRITE / NEVER paths and any HUMAN_CHECKPOINT actions.
   - No instruction in the root that applies only to a subset of tasks.

## Branch B — update (anti-drift)

At the end of a run that changed the repo, before reporting done:

1. List the concerns touched (modules, CI, conventions, deployment).
2. For each concern, find its topic doc. If it exists, propose a scoped edit as a small, reviewable diff; rewrite the whole file only when the structure itself is broken. If it doesn't, decide: create a new topic doc only if the concern is high-leverage and recurrent; otherwise record `no doc change needed` with a one-line reason.
3. Link to the changed source rather than restating it; update cross-references the change broke. If mirror files exist as symlinks, no sync needed; if thin copies (`CLAUDE.md`, `.cursor/rules`, `GEMINI.md`), propagate edits so they stay in sync with the root.
4. **Verify (completion criterion — exhaustive):**
   - Every touched concern has either a proposed edit or a justified `no doc change needed`.
   - Each concept lives in one place; an item already owned by a topic doc stays out of the root.
   - Every non-symlink mirror file matches its root section verbatim where mirrored.
   - No new command added without having been run with exit code recorded.

## Branch C — lint (report only)

1. Run every command the layer lists; record each exit code. Any non-zero is `stale command drift`.
2. Walk each architectural / routing / module claim; confirm it still exists in the code. Report drift line by line, citing both the doc line and the code. Do the same for external doc links — a broken `llms.txt`, 404'd docs URL, or moved page counts as drift.
3. Cross-references between topic docs: orphans (no inbound links), missing (a frequently cited concept with no page), contradictions (two pages that disagree).
4. Every `When …` section has a closure definition (exit code plus proof artifact)? Flag the ones without. Confirm a Permission boundaries section exists and still matches the real READ / WRITE / NEVER paths.
5. Compare each non-symlink mirror file (`CLAUDE.md`, `.cursor/rules`, `GEMINI.md`) against the root section it mirrors; flag any drift.
6. **Instruction budget audit:** flag any root instruction that does not apply to every single task — candidate for extraction to a topic doc or skill.
7. **Flag for deletion:** instructions that are redundant (the agent already knows), too vague to be actionable, or overly obvious ("write clean code").
8. **Verify (completion criterion — exhaustive):**
   - Every command executed, exit code recorded.
   - Every contradiction listed with both sources cited.
   - Every orphan and missing cross-reference signalled.
   - Every missing closure flagged.
   - Every non-symlink mirror file matches its root source, or the mismatch is reported.
   - Every out-of-budget root instruction flagged with a suggested destination.
   - Every deletion candidate listed with reason.
   - A report was produced; no file was edited.

## Branch D — slim (refactor bloated AGENTS.md)

Use when the existing `AGENTS.md` has grown into a ball of mud (error → add rule → repeat) or the user asks for progressive disclosure / refactor.

1. **Find contradictions.** List every pair of instructions that conflict. For each, ask the user which version to keep before proceeding.
2. **Extract essentials.** Pull into the root only what belongs there (see **Root essentials** above).
3. **Group the rest.** Organize remaining instructions into logical categories (TypeScript conventions, testing patterns, API design, git workflow, etc.). Create one topic doc per group.
4. **Emit structure:**
   - A minimal root `AGENTS.md` with conversational links to topic docs (e.g. "For TypeScript conventions, see `docs/TYPESCRIPT.md`.")
   - Each topic doc with its relevant instructions
   - A suggested `docs/` folder tree
5. **Flag for deletion.** Identify instructions that are:
   - Redundant (the agent already knows)
   - Too vague to be actionable
   - Overly obvious (like "write clean code")
   - File-path inventories the agent can discover by listing the tree
6. **Verify (completion criterion — exhaustive):**
   - Every contradiction resolved (user chose) or flagged unresolved.
   - Root contains the essentials floor and nothing that belongs only in a topic doc.
   - Every surviving instruction has exactly one home.
   - Deletion candidates listed with reason; user confirms before removal.
   - Root ≤ ~80 lines after slim.
   - Symlink mirrors preferred over copy mirrors where applicable.
