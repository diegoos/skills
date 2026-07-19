# Shape — Security Testing Tooling

Use when the user asks for scanners, CI audit, or runnable verification.
Tools support review; they do not replace threat modeling or AuthZ analysis.

## Tool selection (prefer repo/CI existing tools)

- Secrets: Gitleaks, TruffleHog, platform secret scanning
- SCA: `npm`/`pnpm`/`yarn` audit, Snyk, OSV, Dependabot, `pip-audit`, `composer audit`
- SAST: Semgrep, CodeQL, Bandit, Ruff security, ESLint security plugins
- DAST: ZAP, Burp, authenticated integration/API contract tests
- Container/IaC: Trivy, Grype, Checkov, tfsec

## How to use results

- Confirm reachability and exploitability in this project before raising severity
- Secret hits: treat as compromised until rotated; check history and artifacts
- SAST: confirm user-controlled source → sensitive sink without intervening control
- Do not run intrusive DAST outside authorized scope
- Summarize tool findings — do not dump raw scanner output

## Reporting tool findings

- Tool + command or CI check name
- Category and affected file/dependency
- Confirmed / likely / false positive / needs-runtime
- Minimal remediation + follow-up verification
