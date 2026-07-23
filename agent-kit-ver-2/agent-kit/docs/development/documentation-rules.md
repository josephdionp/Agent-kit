# Documentation rules

Discipline for editing docs — applies to anyone editing (human or agent).

## Structure

- One document owns each subject. Link to the owner; do not copy.
- If a rule appears in two files, delete one.
- Files over ~500 lines split into a folder of numbered chapters with the
  parent `.md` as a router.

## Status vocabulary

- `planned` — approved scope, not started.
- `partial` — useful work exists but the gate is incomplete.
- `verified` — required tests + persistence + security + migrations + UAT +
  operational checks pass.

## Evidence discipline

- A checked box is not evidence by itself.
- Skipped tests are missing evidence, not success.
- Change status and evidence in the same change as the code.
- Ledger entry: date, owner, work item, evidence path, result, remaining limit.
- Never mark work `verified` while required checks are missing.

## Cross-references

- Prefer `file:line` pointers over pasted code — snippets go stale.
- Link to specific sections with anchors when possible.
- Never link a live doc into `archive/`.

## Deleting

- Delete a doc when its content is duplicated elsewhere. Git keeps history.
- Delete a placeholder when it's been empty for >1 iteration.
- Promote durable findings from completed plans into `project/` or
  `development/`, then delete the plan.
