# Shape — Rust (PR review)

Hunt language and runtime pitfalls.

## Hunt for

- `unwrap` / `expect` in non-test library code on recoverable error paths
- Acquired handles / FDs / guards without `Drop` (or explicit close) that leak on early return
- `unsafe` without a SAFETY comment stating invariants; `unsafe impl Send` / `Sync` that ignores interior mutability or raw pointers
- Blocking I/O, `thread::sleep`, or sync mutex held across `.await` on an async runtime
- Long-running async work missing cancel / `select!` / timeout when abandonment is concrete in this diff
- Clone storms on a hot path only when the cost is demonstrated (not stylistic Clone preference)
- Secrets or PII written to logs / tracing / stdout in this diff

## Pass A

- Do not duplicate `clippy` / `cargo check` diagnostics when those tools ran
- If clippy already emitted a complexity lint, cite it; do not add a second complexity bar
- Check `edition` / MSRV in Cargo.toml before edition-2024-specific advice
- Re-read SAFETY comments and surrounding invariants before flagging unsafe
