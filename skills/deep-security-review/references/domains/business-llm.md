# Domain — Business Logic & LLM

Dispatch only when `llm` / `sensitive` tags or high-value flows exist.
Shape file adds LLM or payment/wallet probes.

## Hunt

- Race conditions, idempotency gaps, state-machine skips
- Payment/wallet bypass, anti-automation gaps
- Prompt injection (direct/indirect); tool permission boundaries
- Sensitive context leakage; LLM deciding access without server enforcement

## Business-logic checks

- Server computes prices, totals, discounts, credits, entitlements
- Client amounts, roles, plans, feature flags, status ignored or re-derived
- State transitions explicit and validated
- Idempotency keys for payments, payouts, webhooks, retries
- Concurrency handled with transactions, locks, unique constraints
- Refunds, cancellations, upgrades have explicit authorization and audit

## LLM / agent checks

- Tool calls authorized for current user/tenant in server code
- Tool schemas narrow; arguments validated
- Model cannot choose arbitrary URLs, SQL, shell, paths, or account IDs
- Sensitive tools require confirmation or human approval
- Tool/RAG results treated as untrusted data (not new instructions)
- Retrieval scoped to caller tenant and permissions
- Secrets and raw credentials never sent to model providers
- Model output sanitized before HTML/SQL/shell/email/file sinks

## Red flags

- "System prompt says not to" is the only control
- Model calls admin APIs with service credentials and no user AuthZ
- Signed wallet message proves ownership forever without expiry
- Price/quantity/owner trusted from the client body
