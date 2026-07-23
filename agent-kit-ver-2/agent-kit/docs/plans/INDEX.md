# Plans

Pre-code intent. Written just before implementation, after reading the code
that exists today. Written by the agent, reviewed by you before code starts.

Design docs (`../project/`) are reference — plans link to them, never restate.

## When to write a plan

- **Small** (one layer, no schema/API change, ~<3 files): ledger line only. No plan.
- **Medium+** (multi-layer, schema/public-API/persisted-behavior change, or
  ~3+ files): plan file in `active/` from `TEMPLATE.md`.

## Flow

1. Read relevant `project/` + `development/` + the actual code today.
2. Write plan → link from the `status/ledger.md` entry.
3. Get review OK.
4. Implement. Update ledger in the same change.
5. On completion: promote durable findings into `project/` or `development/`,
   then delete the plan file (git keeps every version).

## Folders

- `active/` — in-flight plans.
- `queued/` — approved but not started.
- `completed/` — verified plans awaiting promotion. Empty by default; delete
  files once their durable findings are promoted up.
- `TEMPLATE.md` — plan shape (5 sections).
