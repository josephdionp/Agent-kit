# Testing

## Frameworks

- <framework>: what it covers

## Definition of "verified"

For any change to move work forward:

1. `<typecheck cmd>` — passes.
2. `<test cmd>` — passes. Report pass/fail count in the ledger entry.
3. `<lint cmd>` — passes.
4. If integration tests exist that need `<ENV VAR>`: run with it set.
   A green run without that env set is NOT verified.

## Iterate loop

- Baseline first: run relevant tests before editing so failures trace to your change.
- Iterate with the narrowest check.
- Save the full suite for the final pass.
- Fix root causes, not symptoms. Never weaken a test to make it pass.

## Patterns

- **<pattern name>:** <one line — what tests must cover>
