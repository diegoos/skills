# Shape — LLM / AI

Agents, tool calling, RAG, prompt pipelines. Pair with `domains/business-llm.md`.
Prompts are not a security boundary. Hunt rules (_boundary-crossing_, confused deputy) live in the domain — this file holds stack probes.

## Tools as APIs

- Narrow schemas; validate all arguments; rate limits and budgets per user/tenant/tool
- Sensitive tools need confirmation; tool outputs filtered before returning to the model
- MCP / inherited toolsets: child sessions do not inherit broader permissions than the caller

## RAG & assembly

- Retrieval scoped to tenant and permissions at query time
- Retrieved docs are untrusted content (indirect prompt injection)
- Delimiter/template mistakes are assembly bugs — untrusted content must not escape its slot
- Citations do not leak hidden titles, paths, or unauthorized snippets

## Loops / cost / multimodal

- Denial-of-wallet: unbounded tool/LLM loops, retries, or fan-out without budget
- Image/file auto-load + weak CSP → exfil path; report only with that path present
- AI scanners/agents visiting attacker pages cannot call internal URLs (SSRF-like)

## Data & output sinks

- No secrets/tokens/cookies/private keys to model providers; minimize PII before prompts
- Sanitize model output before HTML, SQL, shell, email, file, or code execution

## Review questions

- What APIs can the model reach, and are they protected as public?
- Can one user use the model to affect another user or tenant (_boundary-crossing_)?
- Can model output become code, HTML, SQL, shell, or a privileged request?
