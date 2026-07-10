# Domain language

| Term | Definition | Where used |
| ---- | ---------- | ---------- |
| Order | Confirmed purchase, immutable once placed. | architecture.md, specs/orders.md |

## Rules

- Order transitions: `cart → placed → paid → fulfilled → shipped`.
- A placed Order is immutable; corrections are adjustments.
