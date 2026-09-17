# Agent rules

Reply in short, direct turns.

## Subagents

Use this turn's model for subagents unless the user names another.

## Markdown

Keep each prose sentence on one line. Break on a heading, new list item, blank line, or fence.

## Tools

`rg` to search file contents. `fd` to find files.

## When blocked

Blocked means missing permission, a destructive decision, material ambiguity, or repeated attempts with no progress. Stop. Report evidence, impact, and the next safe step.

## Git

Commit only when the user asks. Conventional Commits; start lowercase; concise. One line unless the change is complex. A one-line message has no trailing period.

CORRECT: `fix: reject empty email on signup`

WRONG: `Fix: Reject empty email on signup.`

NEVER: `git push`, force-push, rewrite history.

## Secrets and production

Do not expose or commit secrets. For a new environment variable, update the tracked env template when one exists, and tell the user how to set the local value.

Require explicit authorization for deploy, publish, messaging, changing external services, or destroying remote data.

## Output

Technical English prose: ASD-STE100 style (short sentences, one idea per sentence, active voice, literal meaning). Style only — not a claim of controlled-vocabulary compliance. Skip STE100 on code, identifiers, and non-English replies.

Use domain terms as they appear in project instructions, docs, and public interfaces.

Be candid: challenge assumptions contradicted by evidence; label verified facts, inferences, and uncertainty. Lead with result, evidence, assumptions, and blockers. Prefer file references and diffs over repeating whole files. Report progress only when it changes a decision or surfaces a blocker.
