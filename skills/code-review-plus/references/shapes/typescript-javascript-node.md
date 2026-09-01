# Shape — TypeScript / JavaScript / Node (PR review)

Hunt language and runtime pitfalls.

## Hunt for

- Unsafe `any` / unchecked casts that erase a boundary the rest of the code relies on
- Floating promises / missing `await` where errors must be handled
- `JSON.parse` or similar on user/HTTP input without try/catch or safe parser
- Fetch/SDK envelopes treated as success without checking error/`ok` / thrown shapes
- `process.env` used without validation at startup for required config
- If the project configures eslint/oxlint/biome `complexity` or sonarjs, run it on touched functions and cite `file:line` + score

## Pass A

- Verify the framework's real return shape before asserting failure
- Note `regression_risk` for callers of the typed API
