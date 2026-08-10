# Shape — LLM / agent surface (PR review)

Hunt prompt and tool-boundary issues in this diff. Not a full threat model; deeper pass → `/deep-security-review`.

## Hunt for

- Untrusted user or retrieved content concatenated into system/developer prompts without a clear boundary
- Tool / function / MCP output treated as trusted instruction or code without validation
- Secrets, tokens, or PII placed in prompts, tool args, or model-facing logs in this diff
- Missing separation of user vs system roles (or equivalent) where the framework supports it
- Exfiltration path: model-chosen tool args that can send secrets or private data to an external sink

## Pass A

- Defense-in-depth gaps are hardening (P2); only flag vulns exploitable or broken today with a pointable line
- Report secrets as `file:line` + type only; never echo values
- Surface needs threat modeling beyond this pass → tell the user to invoke `/deep-security-review` (do not auto-start)
