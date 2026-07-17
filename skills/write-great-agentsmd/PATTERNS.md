# Patterns — what works, what gets ignored

Catalogue consulted on demand. Each heading co-locates a **works** pattern with the **anti-pattern** it replaces, so reading one brings the other; _why_ each fails is one sentence, not a paragraph.
Examples are illustrative shapes, not templates to copy verbatim — always read the repo and emit only what it actually runs.

## Instruction budget / placement

Every token in the root `AGENTS.md` loads on every request. Frontier models follow ~150–200 instructions with reasonable consistency; smaller models attend to fewer. Place each instruction where it costs the least:

| Location                                          | When to use                                                                                             |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Root `AGENTS.md`                                  | Relevant to **every single task** (one-liner, package manager, build commands, permissions, escalation) |
| Topic doc (`docs/TYPESCRIPT.md`, `testing.md`, …) | Relevant to one domain; agent reads only when working in that domain                                    |
| Nested `AGENTS.md` (monorepo package)             | Package-specific stack and conventions; merges with root                                                |
| Agent skill                                       | Repeatable workflow pulled on demand (release, security review, doc sync)                               |

**Anti-pattern — everything in the root.** A 200-line root that covers TypeScript style, testing patterns, deployment, and API design. Why it fails: irrelevant instructions waste tokens and distract the agent on every task; critical instructions get buried ("lost in the middle") and skipped.

## Command-first

**Works:** every instruction is a runnable command with arguments, or an observable condition.

```markdown
## Build and Test Commands

- Install: `pnpm install`
- Lint: `oxlint . --fix`
- Format: `oxfmt .` (or `prettier --write .`)
- Test: `pnpm vitest run --reporter=verbose`
- Type check: `pnpm tsc --noEmit -p tsconfig.json`
- Full verify: `oxlint . && oxfmt --check . && pnpm tsc --noEmit && pnpm vitest run`
```

**Anti-pattern — prose without commands.** A paragraph about "we value well-tested code" has no trigger, no threshold, no exit condition. The agent reads it as a vague preference and proceeds without running anything. Why it fails: nothing to verify against.

```markdown
<!-- BAD -->

We value clean, well-tested code. Please ensure all changes are properly tested before submitting.
```

**Anti-pattern — ambiguous directives.** "Be careful with migrations", "handle errors gracefully", "optimize where possible" — none of these name a behaviour the agent can execute or observe. Why it fails: the agent cannot quantify "careful" and so cannot comply.

```markdown
<!-- BAD -->

- Be careful with Prisma migrations
- Handle errors gracefully
```

## Closure-defined

**Works:** each `When …` section names the exact exit conditions that prove done, plus the proof artifact the PR must carry.

```markdown
## Definition of Done

A task is complete when ALL of the following pass:

1. `oxlint .` exits 0
2. `pnpm vitest run` exits 0 with no failures
3. `pnpm tsc --noEmit` exits 0
4. `oxfmt --check .` exits 0 (or `prettier --check .`)
5. Proof artifact in the PR:
   - Bug fix → a failing test added first, now passing
   - Feature → new test or visual snapshot demonstrating the behavior
6. Changed files staged and committed
7. Commit message follows conventional format: `type(scope): description`
```

**Anti-pattern — missing DoD.** Without explicit closure the agent reports done on "I think so", the most common source of agent-introduced bugs. Why it fails: no check the agent can run before claiming complete.

```markdown
<!-- BAD -->

Make sure the change is properly tested and ready to submit.
```

## Permission boundaries

**Works:** a section listing READ / WRITE / NEVER paths and any HUMAN_CHECKPOINT actions up front; the agent stays inside it.

```markdown
## Permissions

READ: src/**, tests/**, docs/** WRITE: src/**, tests/** NEVER: .env\*, infra/production/**, src/db/migrations/** (generate via Prisma) HUMAN_CHECKPOINT: deploy/**, scripts/billing-send/\*\*
```

**Anti-pattern — no boundary.** Without a boundary the agent edits anything to "make the error go away" — migrations written by hand, env files touched, lock files deleted. Why it fails: the agent optimizes for completing the task, not for staying in its lane; silence reads as permission.

```markdown
<!-- BAD -->

Touch whatever you need to make the tests pass.
```

**Anti-pattern — vague boundary.** "Be careful with production files" — the agent cannot map "careful" to a glob. Why it fails: no set the agent can diff against. Name the exact paths.

## Task-organized

**Works:** sections keyed to what the agent is doing right now.

```markdown
## When Writing Code

- Run `oxlint .` after every file change
- Add types to all new functions (rule: `@typescript-eslint/no-explicit-any`)

## When Reviewing Code

- Security lint: `pnpm eslint . --config eslint.security.config.mjs`
- Verify coverage: `pnpm vitest run --coverage --coverage.thresholds.lines=80`
- List changed files: `git diff --name-only HEAD~1`

## When Releasing

- Bump version in `package.json` (use `pnpm version <type>`)
- Build: `pnpm run build`
- Run full suite: `oxlint . && oxfmt --check . && pnpm tsc --noEmit && pnpm vitest run`
- Tag: `git tag -a v<version> -m "Release v<version>"`
```

**Anti-pattern — flat list.** A flat enumeration of every rule forces the agent to parse all of them on every task regardless of relevance. Why it fails: noise drowns signal inside the reasoning loop. Group by task so the agent selects the relevant slice.
**Anti-pattern — monolithic dump / README duplication.** One file that tries to cover everything, or a paste of the human README. Why it fails: "lost in the middle" — critical instructions buried in text get skipped — and the agent already scans the tree, so duplicating it is pure context cost.

## Escalation

**Works:** explicit paths when blocked, plus the hard guardrails.

```markdown
## When Blocked

- If tests fail after 3 attempts: stop and report the failing test with full output
- If a dependency is missing: check `package.json` first, then ask
- If you hit merge conflicts: stop and show the conflicting files
- Never: delete `pnpm-lock.yaml` to resolve errors, force push, or skip tests
```

**Anti-pattern — destructive workarounds.** Without escalation rules, blocked agents improvise: delete lock files, bypass checks, silently ignore failures. Why it fails: the agent optimizes for "make the error go away", which is rarely what you want. Name what to do; reserve "never" for the truly destructive moves you can't phrase positively.

## Precedence

**Works:** numbered priorities wherever rules trade off.

```markdown
## Priorities

1. Priority 1: Tests pass (`pnpm vitest run` exits 0)
2. Priority 2: Under 5 minutes wall clock
3. Priority 3: Ship fast
```

**Anti-pattern — unranked contradictory rules.** "Move fast" and "ensure comprehensive coverage" with no tie-breaker. Why it fails: the agent can't satisfy both and won't pick — it skips verification to dodge the conflict. Number them; the first one wins.
**Anti-pattern — negative-only constraints.** "Don't use outdated libraries" without naming the allowed alternative. Why it fails: the agent guesses from training data and often picks wrong. Pair the ban with the positive substitute.

## Capabilities over paths

**Works:** describe what the system does and why — capabilities and domain concepts that stay stable across refactors.

```markdown
## architecture.md (excerpt)

Billing replays events from the outbox table, not from the SQS queue, because the queue is not durable across deploys. Do not "simplify" by reading straight from the queue — you will lose events on every rollout.
Domain terms: "organization" = billing entity; "workspace" = team container inside an organization. Never use "group" — it was renamed in v2.
```

**Anti-pattern — file-path inventory.** "Authentication logic lives in `src/auth/handlers.ts`" — paths change on every refactor; the agent will confidently look in the wrong place after a rename. Why it fails: stale paths actively poison context on every request. Describe capabilities; use short pointers (`see src/auth/`) only when the agent needs a starting point.

## Minimal-high-leverage

**Works:** only what the agent cannot infer — architectural decisions and why, tradeoffs, tempting anti-patterns, edge cases, migrations in progress.

```markdown
## architecture.md (excerpt)

The billing service replays events from the outbox table, not from the SQS queue, because the queue is not durable across deploys. Do not "simplify" by reading straight from the queue — you will lose events on every rollout.
The payment provider clocks drift by up to ±3s; the reconciliation window is therefore 10s, not 1s. See `src/reconcile/window.ts`.
All outbound payments are idempotent on `idempotencyKey` (see `src/payments/idempotency.ts`); retrying without reusing the key double-charges the customer.
Every SQL query must use the parameterized helpers in `src/db/safe.ts` — string-interpolated SQL is a production incident, not a shortcut.
```

**Anti-pattern — describing what the tree already shows.** "The `src/commands/` folder holds our commands" — the agent already saw it when it listed the directory. Why it fails: pure context cost, no behaviour change. Point at the folder, don't narrate it.
**Anti-pattern — broad non-actionable guidelines.** "Be secure", "ensure quality". Why it fails: no trigger the agent can recognise, no observable compliance. Grip non-functional constraints with a prescriptive rule the agent can both recognise and violate visibly.

## Link, don't copy

**Works:** point at source, tests, configs; let the repo be the source of truth.

```markdown
- See `src/auth/middleware.ts` for the RBAC rules; do not re-implement.
- Edge cases covered by `tests/auth/edge-cases.test.ts` — extend there.
```

**Anti-pattern — duplication.** An architecture paragraph copied from the README, restated in `AGENTS.md`, and paraphrased again in `architecture.md`. Why it fails: triple drift surface — when one copy updates, the other two silently disagree, and the agent trusts whichever it read first.

## Orchestrator root

**Works:** a short root `AGENTS.md` that acts as an index, pointing at topic docs the way an LLM-wiki's `index.md` points at pages. Opens with a one-liner; links are conversational, not ALL-CAPS commands.

```markdown
# AGENTS.md

This is a React component library for accessible data visualization.
This project uses pnpm workspaces.

## Build & Test

- `pnpm install`
- `oxlint . && oxfmt --check .`
- `pnpm tsc --noEmit`

## Permissions

READ: src/**, tests/**, docs/** WRITE: src/**, tests/** NEVER: .env\*, dist/**

## When Blocked

- Tests fail 3×: stop and report full output
- Missing dep: check `package.json`, then ask
- Never: force push, delete `pnpm-lock.yaml` to "fix" errors

## Topic docs

- architecture.md — module boundaries, invariants, why-decisions
- For TypeScript conventions, see conventions.md
- For testing patterns, see testing.md
- For release constraints, see releasing.md
- pitfalls.md — tempting anti-patterns that regress
```

**Anti-pattern — monolith that grew fat.** One `AGENTS.md` that absorbed the team style guide, the review checklist, and deployment runbooks, until it became a 200-line manual. Why it fails: critical instructions buried get truncated out of context; the agent parses the wall of text instead of doing the task. Disclose the detail behind pointers; keep the root an index.

## Ball of mud

**Works:** when the file has grown past ~80 lines, run the **slim** branch — extract essentials, group the rest into topic docs, flag deletions.
**Anti-pattern — the feedback loop.** The agent does something you don't like → you add a rule to prevent it → repeat hundreds of times → file becomes an unmaintainable ball of mud with conflicting opinions nobody style-passes. Why it fails: each new rule loads on every request whether relevant or not; contradictions accumulate; stale rules poison context. Remedy: slim + progressive disclosure, not more rules in the root.
**Anti-pattern — auto-generated dump.** Initialization scripts that flood `AGENTS.md` with "useful for most scenarios" content. Why it fails: prioritizes comprehensiveness over restraint; most generated rules are either redundant or too generic to act on. Emit only what the repo's evidence supports.

## Mirror via symlink

**Works:** one source of truth; tool-specific filenames point at it.

```bash
ln -s AGENTS.md CLAUDE.md
```

**Anti-pattern — copy mirrors that drift.** A `CLAUDE.md` that copies the root verbatim and must be manually synced on every edit. Why it fails: the copy silently disagrees after the first unsynced change; the agent trusts whichever file its tool loaded. Prefer symlinks; use thin copy mirrors only when symlinks are impossible.

## Hierarchical scoping (monorepos)

**Works:** a root `AGENTS.md` with shared rules and one file per service holding only what differs; nearest file wins.

```
my-monorepo/
  AGENTS.md                 # git workflow, CI, cross-cutting conventions
  services/
    api/AGENTS.md           # pytest, FastAPI patterns, db migration rules
    web/AGENTS.md           # vitest, React patterns, build commands
```

```markdown
# services/web/AGENTS.md

Inherits repo root AGENTS.md. Service-specific overrides:

- Test: `pnpm vitest run`
- Lint: `oxlint .` (stricter config in `oxlint.config.json`)
- NEVER: edit anything outside `services/web/**`
```

**Anti-pattern — restating the parent.** A child file copies the root's git rules verbatim. Why it fails: when the root updates, the child silently disagrees — exactly the duplication drift this standard warns against. Override by naming the replacement, or by omission; never by re-pasting.

## External docs access

**Works:** when the repo depends on external APIs or non-obvious doc access patterns, give the agent the patterns it won't discover on its own — without naming specific services; the agent fills in the actual dependencies from the repo's manifest.

```markdown
## External Docs

To access docs for any dependency, service, or SDK this repo uses:

- Check `<docs-root>/llms.txt` first — many docs sites publish one; it indexes every page in a single file.
- Append `.md` to a docs URL for the markdown version (e.g. `<docs-root>/api/<endpoint>.md`). HTML pages parse poorly; markdown parses cleanly.
- For GitHub-hosted docs, prefer `raw.githubusercontent.com/{owner}/{repo}/refs/heads/main/{path}` over the rendered site.
- If a page returns JS-rendered content (no usable text), fall back to the canonical GitHub repo or a static mirror.
  Record the exact access pattern per doc site the repo touches, so the agent doesn't guess URLs from training data (they often 404 or point at moved content).
```

**Anti-pattern — vague "see the docs".** "Consult the API docs" with no URL or access pattern. Why it fails: the agent guesses a URL from training data, often one that has moved or never existed; it rarely re-discovers content after a 404, and a JS-rendered page returns nothing usable. Give the exact access pattern.
