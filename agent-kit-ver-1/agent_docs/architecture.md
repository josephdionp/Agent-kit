# Architecture

Read when the task touches module boundaries, data flow, or cross-cutting
concerns. Skip for isolated bug fixes.

Prefer `file:line` pointers over pasted code — snippets go stale.

## Modules

- `<src/module-a>` — <one line: what it owns>
- `<src/module-b>` — <one line: what it owns>

## Data flow

<Where data enters, where it's validated, where it's persisted, where it
leaves. One short paragraph or a numbered list. Point at the entry-point file
and let the agent read from there.>

## Boundaries and contracts

- Public API surface: `<file>`
- Persisted schemas: `<file>` or `<migrations dir>`
- External integrations: <name> at `<file>`

## Load-bearing decisions

Non-obvious *why*s that would otherwise get "helpfully" refactored away.

- <decision>: why (`<file:line>` if relevant)
