# Agent kit

Two agents (Claude Code + Kilo Code), one instruction file (`AGENTS.md`), one repo.

## Where each file goes

**In your repo — commit these:**

```
your-project/
├── CLAUDE.md                     # shim: makes Claude Code read AGENTS.md
├── AGENTS.md                     # the real project file — you edit this
├── agent_docs/
│   ├── architecture.md
│   ├── testing.md
│   ├── conventions.md
│   └── forbidden.md
├── .claude/commands/review.md    # /review in Claude Code
└── .kilo/commands/review.md      # /review in Kilo Code
```

**On your machine — global, once:**

Paste `system-prompt.md`'s content (everything below the `---`) into:

| Tool | Where |
|---|---|
| Claude Code | `~/.claude/CLAUDE.md` |
| Kilo Code | Save to `~/.config/kilo/system-prompt.md`, then add `"~/.config/kilo/system-prompt.md"` to the `instructions` array in `~/.config/kilo/kilo.jsonc` |

**Delete after setup:**

- `system-prompt.md` (content lives globally now)
- `README.md` (reference only — not read by either agent)

## What each tool reads

| File | Claude Code | Kilo Code |
|---|---|---|
| `CLAUDE.md` | Yes — imports `AGENTS.md` | Ignored |
| `AGENTS.md` | Via the `CLAUDE.md` import | Yes, directly |
| `agent_docs/*` | Lazy, when `AGENTS.md` points to them | Same |
| `.claude/commands/` | `/review` | Ignored |
| `.kilo/commands/` | Ignored | `/review` |

Using only one tool? Delete the other's folder. If Kilo-only, also delete `CLAUDE.md`.

## Setup

1. Extract the zip at your project root.
2. Paste `system-prompt.md`'s content into your tool's global slot (table above). Once per machine.
3. Fill in `AGENTS.md` from the actual repo. Verify every line.
4. Leave `agent_docs/*` as stubs — expand when the agent misses something concrete.
5. Verify it loaded: Claude Code → run `/memory`, check the files are listed. Kilo → ask "what instructions do you have?"
6. Delete `system-prompt.md` and this `README.md` from the repo.

## Growing it

- Add a line only after the agent got something concrete wrong.
- New rules go in `AGENTS.md` → Learnings section. Promote up when durable.
- Anything a linter/formatter/hook can enforce → wire it up. Prompts are probabilistic; hooks always fire.
- Prune: for each line ask "would removing this cause a mistake?" If not, delete.

## Optional: path-scoped rules

`AGENTS.md`'s pointers rely on the agent's judgment to open `agent_docs/*` when relevant. Both tools also support deterministic loading tied to file patterns:

- **Claude Code:** `.claude/rules/<name>.md` with YAML frontmatter `paths: ["tests/**/*"]`
- **Kilo Code:** `.kilo/rules/<name>.md`, listed in `kilo.jsonc` → `instructions`

Reach for this only if a doc isn't getting read when it should.
