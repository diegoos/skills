# Dependency review

Orchestrator-only. Open when `package.json`, lockfile, or equivalent manifest is in the review source. Do not give this path to hunters.

## New dependency

- Does the existing stack or stdlib already solve this?
- Size / bundle impact proportional to the need?
- Actively maintained (recent commits, open issues)?
- Known vulns (`npm audit` / equivalent) and compatible license? When the audit cannot run, record it under `Checks: not run`.

Prefer existing utilities over a new dependency.

## Upgrade

- Read the changelog (or migration notes), not only the version bump
- Prefer one dependency (or a small related group) per change
- Review the lockfile diff; do not hand-edit the lockfile
- Suite green before and after when tests exist
