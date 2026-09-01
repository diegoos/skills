# Patterns

Catalogue consulted on demand. Each heading co-locates a **works** pattern with the anti-pattern it replaces. *Why* each fails is one sentence. Examples are shapes, not templates. Emit only what this repo runs.

## Always-on budget

Place each instruction where attach costs the least.

| Attach | When |
| ------ | ---- |
| Always-on | Every task in this harness (floor in `SKILL.md`) |
| Glob / `.mdc` / `applyTo` / `paths:` | One domain or path slice |
| Nested `AGENTS.md` | Package-specific stack; names replacements |
| Skill | Repeatable workflow (release, review, doc sync) |

**Anti-pattern: everything in always-on.** A 200-line root covering TypeScript style, testing, deploy, and API design. Why it fails: irrelevant lines spend the always-on budget on every task; the middle of the file is skipped.

## Observable or attachable

**Works (always-on):** a runnable command, an observable condition, or a CORRECT/WRONG snippet.

```markdown
## Commands

- Lint one file: `oxlint src/foo.ts --fix`
- Test one file: `pnpm vitest run src/foo.test.ts`
- Typecheck: `pnpm tsc --noEmit`
```

A style convention with a CORRECT/WRONG snippet (always-on or glob body):

```tsx
// Named exports only.
// CORRECT
export const UserCard = (props: UserCardProps) => { /* … */ }

// WRONG
export default function UserCard() { /* … */ }
```

**Works (glob):** the same snippet in a Cursor `.mdc` with `globs: **/*.tsx` (or Copilot `applyTo`) instead of always-on.

**Anti-pattern: preference with no check.** "We value well-tested code." Why it fails: nothing to run or violate.

**Anti-pattern: adjective directives.** "Be careful with Prisma migrations", "handle errors gracefully." Why it fails: "careful" is not a behaviour.

## Closure

**Works:** two to four commands whose exit 0 proves done.

```markdown
## Done when

1. `oxlint .` exits 0
2. `pnpm vitest run` exits 0
3. `pnpm tsc --noEmit` exits 0
```

**Anti-pattern: missing done.** "Make sure the change is ready." Why it fails: the agent reports done on "I think so."

**Anti-pattern: PR checklist in always-on.** Seven-item Definition of Done including commit message and staging. Why it fails: review ceremony belongs in a skill or pointed doc; extra constraints add steps on every task.

## Boundaries

**Works:** exact globs. Silence is permission.

```markdown
READ: src/**, tests/**, docs/**
WRITE: src/**, tests/**
NEVER: .env*, infra/production/**
HUMAN_CHECKPOINT: deploy/**
```

**Anti-pattern: no boundary** in a repo that has `.env`, `generated/`, or `legacy/`. Why it fails: the agent edits whatever unblocks the task.

**Anti-pattern: "be careful with production files."** Why it fails: no glob to diff against.

## Escalation

**Works:** what to do when blocked, plus destructive guardrails.

```markdown
## When blocked

- Tests fail 3×: stop and report full output
- Missing dep: check `package.json`, then ask
- Merge conflicts: stop and list the files
- NEVER: delete the lockfile to "fix" errors, force-push, skip tests
```

**Anti-pattern: no stop rule.** Why it fails: a blocked agent deletes lockfiles or skips checks to make the error go away.

## Precedence

**Works:** numbered tradeoffs.

```markdown
1. Tests pass (`pnpm vitest run` exits 0)
2. Wall clock under 5 minutes
3. Ship
```

**Anti-pattern: unranked opposites.** "Move fast" and "comprehensive coverage" with no winner. Why it fails: the agent drops verification to dodge the conflict.

**Anti-pattern: ban without substitute.** "Don't use outdated libraries." Why it fails: the model guesses from training data. Name the allowed library.

## Capabilities over paths

**Works:** stable domain facts and why.

```markdown
Billing replays from the outbox table, not from the queue: the queue is not durable across deploys.
"organization" = billing entity; "workspace" = team inside an organization. The old word "group" was renamed in v2.
```

**Anti-pattern: file inventory.** "Auth lives in `src/auth/handlers.ts`." Why it fails: the path goes stale and poisons every turn. Point at `src/auth/` only as a start.

## Environment, not a cache

**Works:** cache the gotcha; point at the config for the rest.

```markdown
This repo uses pnpm workspaces. Run `pnpm test`, not `npm test`.
See `src/payments/idempotency.ts` for the key; retrying without it double-charges.
```

**Anti-pattern: narrating the tree.** "The `src/commands/` folder holds our commands." Why it fails: the agent already listed the directory.

**Anti-pattern: "be secure."** Why it fails: no visible violation. Write "SQL goes through `src/db/safe.ts`; string-interpolated SQL is an incident."

## Link, don't copy

**Works:** one home.

```markdown
RBAC is `src/auth/middleware.ts`. Extend edge cases in `tests/auth/edge-cases.test.ts`.
```

**Anti-pattern: three paraphrases** (README, always-on, `architecture.md`). Why it fails: the first copy the agent reads wins after the others drift.

## Adapter, not a second body

**Works:** canonical `AGENTS.md` plus the overlay that harness needs (`@AGENTS.md`, `context.fileName`, `read:`, a glob `.mdc`).

```markdown
@AGENTS.md

Claude-only: use Plan mode for migrations.
```

```yaml
# .cursor/rules/tsx-exports.mdc
description: Named exports in TSX
globs: "**/*.tsx"
alwaysApply: false
```

**Anti-pattern: copy mirrors.** A `CLAUDE.md` pasted from `AGENTS.md`. Why it fails: the first unsynced edit splits the policy.

**Anti-pattern: two always-on files** for Copilot (`copilot-instructions.md` and root `AGENTS.md`). Why it fails: both load; neither wins.

**Anti-pattern: symlink `CLAUDE.md` → `AGENTS.md` when the harness already loads both always-on.** Why it fails: the same text is injected twice.

## Nested files

**Works:** root holds shared rules; the child holds only the delta and names replacements.

```markdown
# services/web/AGENTS.md

Use `pnpm vitest run` instead of `npm test`.
NEVER: edit paths outside `services/web/**`.
```

**Anti-pattern: child reprints the parent's git section.** Why it fails: Codex pays twice toward 32 KiB; Devin already inherited the parent.

**Anti-pattern: override by omission.** Why it fails: Codex still concatenates the parent; Devin still inherits it.

## Ball of mud

**Works:** when always-on is over budget, cut no-ops and move leftovers to glob/nested/skill — do not add another root line.

**Anti-pattern: error → add a root rule → repeat.** Why it fails: every new rule loads on every task; contradictions pile up. Add a rule only after the agent repeats the mistake.

**Anti-pattern: `/init` dump.** Why it fails: generated overviews and generic rules cost tokens and can lower task success. Emit what this repo proves.

## External docs

**Works:** the access pattern the agent will not guess.

```markdown
Docs: try `<docs-root>/llms.txt`, then the same URL with `.md`. GitHub-hosted pages: `raw.githubusercontent.com/{owner}/{repo}/refs/heads/main/{path}`.
```

**Anti-pattern: "see the docs"** with no URL. Why it fails: training-data URLs 404.

## When … slices

**Works as a short always-on slice** when the harness has no glob (plain `AGENTS.md`):

```markdown
## When releasing

- `pnpm version <type>`
- `pnpm run build`
```

**Anti-pattern: organizing the whole file as When Writing / When Reviewing / When Releasing** while Cursor or Copilot could attach by path. Why it fails: you pay always-on for a slice a glob would have scoped. Prefer `globs` / `applyTo` when that harness is in play.
