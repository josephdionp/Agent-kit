# agent-kit

Drop-in skeleton for any project's agent + docs configuration. Distilled from
several real-world refactor iterations. Delete this README after you've adapted
the kit — no agent reads it.

## What's inside

```text
AGENTS.md                       Project entry. §1 facts + §2 project-specific rules.
CLAUDE.md                       @AGENTS.md shim for Claude Code.
system-prompt.md                Universal + personal working style. Moves to global slot.
.claude/commands/review.md      /review workflow for Claude Code.
.claude/rules/README.md         How to add path-scoped rules.
.kilo/commands/review.md        /review workflow for Kilo Code.
docs/                           Documentation skeleton (see docs/INDEX.md).
```

Also add `~/.codex/prompts/review.md` (copy of `.claude/commands/review.md`)
if you use Codex.

## Setup (once per machine)

Move `system-prompt.md`'s content — everything below the `---` — into your
global slot:

| Tool | Global slot |
|---|---|
| Claude Code | `~/.claude/CLAUDE.md` |
| Kilo Code | `~/.config/kilo/system-prompt.md`, then add path to `instructions` in `~/.config/kilo/kilo.jsonc` |
| Codex CLI | `~/.codex/AGENTS.md` (see known-bug section in `system-prompt.md`) |

Personal cross-project style (rules that apply to every project) also lives in
this file. Never create a per-repo file for cross-project content.

## Adapt (once per project)

1. Extract this kit at the repo root.
2. Fill in `AGENTS.md` §1 from the real repo. Verify every command against
   `package.json` / `Makefile`.
3. Write `AGENTS.md` §2 with actual project invariants (things true only in
   this repo — architectural boundaries, testing gates, security musts).
4. Fill in `docs/project/{overview,stack,architecture}.md` — one page each.
5. Fill in `docs/development/{setup,testing}.md`.
6. If your project has clear module boundaries, use `docs/modules/` —
   one README per module. Otherwise delete the folder.
7. Verify Kilo whitelist matches `.kilo/commands/` (some repos use `command/`
   singular). Rename if needed.
8. Delete this `README.md` and `system-prompt.md` from the repo.

## Grow

- Add a rule only after the agent got something concrete wrong.
- Learnings go in `AGENTS.md` §2 Learnings. Promote up when durable.
- Anything a linter/formatter/hook can enforce → wire it up. Prompts are
  probabilistic; hooks always fire.
- Prune: for each line ask "would removing this cause a mistake?" If not,
  delete.

## Codex-only note

Codex issue [#8759](https://github.com/openai/codex/issues/8759): global
`~/.codex/AGENTS.md` sometimes doesn't load. Check `/status` — blank
"Agents.md" line means the bug hit you. Simplest workaround: paste the
system-prompt content directly into the repo's `AGENTS.md` §0 (above §1).
Other workarounds in `system-prompt.md`.
