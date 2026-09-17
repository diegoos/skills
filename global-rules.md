# Agent rules

- **Be** direct in your communication; do not respond with long articles or be wordy.

## Sub agent rules

- **Always** use the same model for subagents, unless requested by the user.

## Markdown rules

- Don't use prose hard line-break.

## Tools

- Prefer to use `rg` (ripgrep) over `grep` for searching text in files.
- Prefer to use `fd` over `find` to find files.

## When blocked and Git safety

- When **blocked** (missing permission, destructive decision needed, material ambiguity, or repeated attempts with no progress): stop; report evidence, impact, and the next safe step.
- Never `git push`. Commit only when the user asks. Never force-push or rewrite history.
- Never expose or commit secrets. For a new environment variable, update the tracked env template when one exists, and tell the user how to set the local value.
- Require explicit authorization for deploy, publish, messaging, changing external services, or destroying remote data.

### Git commit rules

- Commit message should be in conventional commit format.
- Always start a commit message with lowercase letters.
- Commit message should be concise and to the point.
- Commits with only one line should not end with a period.
- Commits **should** use one line, unless the changes are complex.

## Output

- For technical English prose: ASD-STE100 style — short sentences, one idea per sentence, active voice, literal meaning. Do not claim formal controlled-vocabulary compliance. Do not apply STE100 to code, identifiers, or non-English replies.
- Use domain terms as they appear in project instructions, docs, and public interfaces.
- Be direct and candid: challenge assumptions contradicted by evidence; label verified facts, inferences, and uncertainty. Lead with result, evidence, assumptions, and blockers. Prefer file references and diffs over repeating whole files. Report progress only when it changes a decision or surfaces a blocker.
