# AGENTS.md

Project facts only. Universal behavior lives in the global system prompt.
Conflict → stricter safety rule wins; surface it.

Verify every line from the actual repo. Delete what doesn't apply.

---

## The project

- **What:** <one line — what this project is>
- **Why:** <one line — the problem it solves / who it's for>
- **Primary users / workflows:** <one line>

## Stack

- Language / runtime: <…>
- Framework(s): <…>
- Package manager: <…>
- Deploy target: <…>

## Map

- Source: `src/`
- Tests: `tests/`
- Docs: `docs/`
- Generated / vendored (do not hand-edit): <paths>
- Do not modify without approval: <paths>

## Commands

Exact, copy-pasteable. Iterate with the narrowest check; save full suites for
the final pass.

- Install: `<cmd>`
- Test (single file, iteration): `<cmd>`
- Test (all, final pass): `<cmd>`
- Lint: `<cmd>`
- Typecheck: `<cmd>`
- Format: `<cmd>`
- Run locally: `<cmd>`
- Manual / UI checks: <how, or "ask">

## Deeper docs (read only when relevant to the task)

Plain paths on purpose — in Claude Code, `@path` eagerly imports the file into
every session, which defeats lazy loading.

- `agent_docs/architecture.md` — modules, boundaries, data flow
- `agent_docs/testing.md` — patterns, fixtures, what "verified" means here
- `agent_docs/conventions.md` — naming, errors, config, logging
- `agent_docs/forbidden.md` — things that look reasonable but break this project

## Learnings

Append one concrete line here when corrected — imperative and specific
(`Always use X for Y`, not `be careful with Y`). Tighten existing lines instead
of duplicating. Delete when the underlying issue is gone (refactor, model
upgrade, process change). Promote durable lines up into the sections above.

- (empty)
