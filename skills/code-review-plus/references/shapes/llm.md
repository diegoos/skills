# Shape — LLM / agent surface (PR review)

Hunt prompt and tool-boundary issues in this diff. Not a full threat model; deeper pass → `/deep-security-review`.

## Hunt for

- Untrusted user or retrieved content concatenated into system/developer prompts without a clear boundary
- Tool / function / MCP output treated as trusted instruction or code without validation
- Secrets, tokens, or PII placed in prompts, tool args, or model-facing logs in this diff
- Missing separation of user vs system roles (or equivalent) where the framework supports it
- Exfiltration path: model-chosen tool args that can send secrets or private data to an external sink

## Pass A

Report secrets as `file:line` + type only. Hardening without a path today stays category hardening.
