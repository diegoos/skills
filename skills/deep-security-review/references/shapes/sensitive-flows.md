# Shape — Sensitive Flows & Supply Chain

Payments, billing, wallets, package publish. Pair with Business/LLM or Infra.

## High-value flows

- Server computes prices, totals, discounts, credits, entitlements
- Explicit validated state transitions; idempotency on payments/webhooks/retries
- Concurrency: transactions, locks, unique constraints
- Parallel submit, webhook replay, out-of-order steps, cross-tenant attempts

## Payment / billing

- Provider webhooks: verify signatures; dedupe event IDs
- Amounts/currency verified against server records
- Subscription status from trusted provider state, not client
- No card data stored/logged unless explicitly PCI-scoped
- Checkout/billing return URLs allowlisted

## Wallet / blockchain

- Ownership via signed nonces: unique, short-lived, non-replayable
- Verify chain, domain, message, account on signatures
- Transactions check recipient, amount, asset, chain ID, slippage
- Never request/store/log private keys or seed phrases
- Do not trust client-reported tx success without chain/provider verification

## Dependencies / publish

- Lockfile + reproducible CI; triage critical/high vulns
- High-risk parsers/templates/file processors reviewed
- Publish credentials MFA + least privilege; untrusted PRs cannot publish
- Artifacts free of `.env`, keys, private source maps
