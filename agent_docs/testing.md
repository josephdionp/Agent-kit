# Testing

Read when adding tests, fixing bugs (regression tests), or verifying a change.

## What "verified" means here

- Baseline: `<cmd to run before editing>`
- Iterate: `<single-file test cmd>`
- Final pass before "done": `<full suite cmd>` + `<lint>` + `<typecheck>`
- For UI/manual checks: <how to run, or "ask the user">

## Test framework and layout

- Framework: <name + version>
- Test files live in: `<path pattern>`
- Fixtures / helpers: `<path>`
- Naming convention: `<pattern>`

## Patterns to match

- Unit test shape: <link to a representative test `file:line`>
- Integration test shape: <link>
- How to mock external services: <link or one line>

## Regressions

New behavior → add a test. Bug fix → add a failing test that reproduces the
symptom first, then fix, then confirm it passes. Never make a failing test
pass by weakening the assertion.

## Known-flaky areas

- <area>: why, how to handle
