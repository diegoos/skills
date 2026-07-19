# Shape — LLM / AI

Agents, tool calling, RAG, prompt pipelines. Pair with domain-business-llm.
Prompts are not a security boundary.

## Tools as APIs

- Every tool authorized for current user/tenant in server code
- Narrow schemas; validate all arguments
- No arbitrary URLs, SQL, shell, paths, recipients, or account IDs from the model
- Sensitive tools need confirmation; rate limits and budgets per user/tenant/tool
- Tool outputs filtered before returning to the model; treat as untrusted data

## RAG & injection

- Retrieval scoped to tenant and permissions at query time
- Retrieved docs are untrusted content (indirect prompt injection)
- Citations do not leak hidden titles, paths, or unauthorized snippets
- Separate instructions from untrusted content in prompt structure
- Log suspicious tool-call patterns

## Data & output sinks

- No secrets/tokens/cookies/private keys to model providers
- Minimize PII before prompts; retention/training opt-out documented
- Sanitize model output before HTML, SQL, shell, email, file, or code execution
- AI scanners/agents visiting attacker pages cannot call internal URLs (SSRF-like)

## Review questions

- What APIs can the model reach, and are they protected as public?
- Can one user use the model to affect another user or tenant?
- Can model output become code, HTML, SQL, shell, or a privileged request?
