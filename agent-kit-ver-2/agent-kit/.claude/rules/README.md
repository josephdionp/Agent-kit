# Path-scoped rules for Claude Code

Files here load automatically when Claude Code reads a file matching their
YAML `paths:` glob. Deterministic — no judgment needed at the prompt level.

## Format

```markdown
---
paths:
  - "apps/api/**/*"
  - "tests/api/**/*"
---

# API work

Read `docs/project/architecture.md` and the affected module plan before
editing. Confirm tenant scope, transaction boundaries, and typed failures.
```

## When to add one

Only when a rule *must* load whenever the agent touches specific paths.
For everything else, `AGENTS.md` pointers are enough and less overhead.

Typical candidates:
- Frontend rules that must load with any component file.
- Test-writing rules that must load with any test file.
- Migration rules that must load with any SQL file.
- Docs-authoring rules that must load with any `.md` change.

## Not this

Do not put universal rules here (they belong in the global system prompt).
Do not duplicate content from `AGENTS.md` here (single source of truth).

## Delete this README after you add real rules — it's guide-only.
