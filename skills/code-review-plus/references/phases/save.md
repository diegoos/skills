# Phase 0 — Save choice

Orchestrator-only. Open at the start of the review branch, before Phase 1.

## Ask

When this conversation already recorded `Save: file` or `Save: session`, reuse it and do not ask. Otherwise ask once: save the report under `docs/code-review/` in the **reviewed** repo, or keep it in this session only. Use the harness question UI when it exists; otherwise ask and wait for the answer.

Record the answer in the conversation as `Save: file` or `Save: session`. When the run cannot ask, use `Save: file` and state that assumption in the Review Summary. A fix or knowns call before any choice uses `Save: file`.

## Effect

- `Save: file`: Phase 4.5 writes `docs/code-review/<timestamp>.md`.
- `Save: session`: Phase 4.5 fills the Session ledger in the reply (`./references/phases/persist.md` § Session ledger) and writes nothing in the reviewed repo. Later review, fix, and knowns calls in this session read and update the newest ledger (`./references/phases/scope.md` § Prior memory, `./references/phases/fix.md`, `./references/phases/knowns.md`).

## Completion criterion

`Save: file` or `Save: session` is recorded in the conversation, and the user was asked at most once in this session.
