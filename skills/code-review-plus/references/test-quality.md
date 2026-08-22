# Test quality

Quality-only. Open when the review source includes test paths. Hunt tests **already in the diff**. Missing tests belong to Correctness/scope.

Judge the artifact. Leave TDD write-order (red-green, delete-and-restart) to implementation skills.

## Three questions (required when tests are in scope)

Answer in the report `### Test quality` section and in the memory file when tests are in scope. Omit both when the review source has no tests.

1. Are all tests in the diff useful?
2. Are all of them efficient?
3. Can we remove any that do not cover a critical behavior?

## Gate A — Name the break

For each new or changed test, name the production change that would make **this** test fail, and whether that change is a **bug** or an **intentional decision**.

- Cannot name a bug → KEEP (useless / coverage theater)
- Only a decision fails it (constant, exact wording, private shape) → KEEP (change detector)
- Expected value reuses the code under test or its helpers → KEEP (mirror assertion)
- Asserts source text / "symbol stays removed" → KEEP (behavior, not text)

## Gate B — Exercise the real thing

- Assert on a mock, `*-mock` test id, or a test that fails if you unmock → KEEP (mock-as-SUT)
- Mock is allowed when the dependency is slow or external, sits below the side effects the test needs, mirrors the full real structure, and earns **no** assertion
- Setup of mocks/fixtures larger than the assertion, with no reason for the mock → KEEP
- Method on a production class called only from tests → KEEP (move to test util)
- Fake that accepts anything / one spy for success, error, and malformed → KEEP (wrong branch can pass)

## Gate C — Mutation check

Mentally mutate production. At least one test in the diff should fail for each realistic mutation: wrong constant or argument; wrong branch; missing side effect; empty/default return; missing validation for zero, empty, nil, unauthorized, or malformed.

A mutation nothing catches → KEEP (unprotected or tautological). Asking to **add** a missing case is Correctness when no test exists; Quality flags tests that would still pass.

## KEEP (finding)

- Horizontal pile: many new tests in one imagined layer, same generic fixture, weak tie to the path this diff opened
- Vague name (`test_works`, `test1`) or `"and"` joining two behaviors
- Happy path only when the same diff has error/empty/boundary branches
- Structure-coupled: fails on private shape / fixture keys / internal calls; would still pass if the user-visible result were wrong
- Unit test with network, DB, or `sleep` (wrong level: inefficient)
- Duplicate of the same behavior; obsolete test; getter/reexport/trivial forwarding with no validate/normalize/default/derive/enforce/side effect
- Volume that mirrors production line-by-line, mocks everything, covers trivia, omits the real negative. Finding: utility/cost.

Typical severity: P3 maintainability; P2 when the test is the only claimed proof and a mutation survives, or mock-as-SUT hides a break. Suggested fix: strengthen the assertion, drop the mock-as-SUT, split, or delete the useless test (ask first).

## DROP

- Mock of slow/external I/O with complete fixtures and no assert on the mock
- Narrow characterization test that names a surprising upstream assumption
- Table-driven tests with literal `want` values
- Getter/constructor that validates, normalizes, defaults, derives, enforces, or has a side effect
- POC / spike / landing / throwaway CLI. Skip asking for more tests; an inflated suite there may be a **removal** finding
- "Missing E2E/integration/pyramid" on a unit test
- Coverage % / "should have written tests first"

## Pass A reminders

- Coverage theater without a named break is not kept unless the test is actively misleading (always-green, mock-as-SUT)
- Preference to rewrite with TDD stays out of Quality
- Suggested fix preserves error paths; deleting a test names which behavior becomes unprotected
