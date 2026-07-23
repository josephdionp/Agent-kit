# Delivery ledger

> Live status source. Update evidence in the same change that changes status.
> The single source of truth for implementation state.

## Program status

<Short table of top-level workstreams and their status. Delete this section
if the project is small enough that only the module ledger matters.>

```text
Workstream          Status    Owner       Evidence / blocker
------------------  --------  ----------  ------------------------------
<workstream name>   planned   unassigned  —
```

## Module ledger

```text
Module         Status    Next gate
-------------  --------  ---------------------------------
<module>       planned   <what needs to happen next>
```

## Next-step implementation log

> Newest first. A worker reads the top entry, does exactly that, then updates
> status to `done` with evidence. No entry = no coding.

### `[todo]` <task title>

- **Scope:** <what's being built>
- **Files:** <paths that will change>
- **Approach:** <one paragraph>
- **Done-criteria:** <verifiable checks>
- **Refs:** <ADR, plan, module README>

## Update rule

Any change that moves work forward must update this file in the same commit/PR:

1. Run proportionate automated checks.
2. Update the entry above: date, owner, work item, evidence path, result,
   remaining limit.
3. Change the status.
4. If the repo-wide shape changed, also update `docs/project/architecture.md`.
5. Never mark work `verified` while required checks are missing.

## Blocker rule

A blocker entry must name the missing decision, external prerequisite, or
failed gate and the owner responsible. `blocked` is not a substitute for
incomplete planning.
