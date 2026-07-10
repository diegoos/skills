# make-docs

Generates and maintains project documentation for humans and AI agents:
**architecture** (how the system is structured) and **behavioral specs**
(what it does — observable outcomes an agent can implement or verify).

Works for any project shape: services, CLIs, libraries, workers, monorepos.

## Commands

| Command | When |
| ------- | ---- |
| `/make-docs explore` | Existing codebase — survey, propose, generate the suite |
| `/make-docs update` | Sync docs with commits since `> Updated on` in `docs/README.md` |
| `/make-docs adr` | Record one architecture decision |

## Output

```text
docs/
  README.md
  architecture/
    architecture.md
    domains/          # glossary, api (if any), constraints
    decisions/        # ADRs
    patterns.md
  specs/
    <domain>.md       # requirements + Given/When/Then scenarios
```

Scope scales with the repo: small projects get README + architecture +
decisions; larger ones earn the full set. Unearned sections are cut.

## Files

- **SKILL.md** — agent instructions (source of truth for behavior)
- **references/** — one template per doc type; load only what you write
- **README.md** — this file

## Out of scope (default)

Data model, observability, CI/CD — ask before generating if present;
otherwise skip.
