# AGENTS.md

Two sections, kept separate on purpose:
- **§1 PROJECT** — facts about *this codebase*. Changes only when the repo changes.
- **§2 AGENT RULES** — how to *work in this repo*. Project-specific behavior only.

Universal behavior + personal cross-project style live in the global system
prompt, not here. Conflict → stricter safety rule wins; surface it.

Verify every line against the repo. Delete lines that stop being true.

---

# §1 · PROJECT — facts

## What / why

- **What:** <one line — what this project is>
- **Why:** <one line — the problem it solves / who it's for>
- **Workflows:** <one line — the main surfaces or user paths>

## Stack

- Language / runtime: <…>
- Framework(s): <…>
- Package manager: <…>
- Deploy target: <…>

## Map

- Source: `src/`
- Tests: `tests/`
- Shared / packages: <paths>
- Generated / vendored (never hand-edit): <paths>
- Do not modify without approval: <paths>

## Commands

Exact, copy-pasteable, verified against `package.json` / `Makefile`.

- Install: `<cmd>`
- Test (single file, iterate): `<cmd>`
- Test (all, final pass): `<cmd>`
- Lint / typecheck / format: `<cmd>` / `<cmd>` / `<cmd>`
- Run locally: `<cmd>`
- Migrate / seed: `<cmd>`
- Manual / UI checks: <how, or "ask">

## Routers

Start from the affected module when a task fits one; otherwise the topic.

- Modules (if used): `docs/modules/INDEX.md`
- Project (what & why): `docs/project/INDEX.md`
- Development (how to work here): `docs/development/INDEX.md`
- Plans (pre-code intent): `docs/plans/INDEX.md`
- Live status: `docs/status/ledger.md`

---

# §2 · AGENT RULES — this repo only

## Hard invariants — always apply

Landmines. Only real project-specific rules that must hold on every task.
Generic discipline belongs in the global system prompt.

- <e.g. "Persistence: parameterized SQL via `pg`. No ORM, no query builder.">
- <e.g. "Tenant scope comes from server-side auth context, never request bodies.">
- <e.g. "Cross-module access via `public.ts` surfaces only.">

## Work flow

1. Understand the task.
2. Start from the affected module README (if applicable) or the relevant router.
3. Inspect current code before planning or editing.
4. Medium+ work: create or refresh a plan in `docs/plans/active/` from
   `docs/plans/TEMPLATE.md`.
5. Smallest complete change.
6. Run proportionate checks.
7. Update the plan or `docs/status/ledger.md` in the same change as code.
8. Report changed files, checks run, results, and remaining limits.

Do not code from a stale plan. Confirm current code first.

## Definition of done

<Exact checks + expected result. Example:
"typecheck + full test suite + modularity gate all pass; integration tests
run with DATABASE_URL set (not skipped); report pass/fail counts.">

## Status and evidence

- `docs/status/ledger.md` is the single live status source.
- Update status and evidence in the same change as code.
- Entry: date, owner, work item, evidence path, result, remaining limit.
- A checked box alone is not evidence. Skipped tests are missing evidence,
  not success.
- Never mark work `verified` while required persistence, security, migration,
  UAT, or operational evidence is missing.

## Learnings

One concrete line per correction, only after something actually went wrong.
Tighten instead of duplicating. Delete when the issue is gone. Promote durable
lines up into the sections above.

- (empty)
