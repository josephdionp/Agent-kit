# Agent kit

Three agents (Claude Code, Kilo Code, Codex CLI), one instruction file (`AGENTS.md`), one repo.

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

Codex reads `AGENTS.md` from the repo root directly — no shim. Codex custom prompts are global-only, so `review.md` for Codex goes in `~/.codex/prompts/` (below), not in the repo.

**On your machine — global, once:**

Paste `system-prompt.md`'s content (everything below the `---`) into:

| Tool | Where |
|---|---|
| Claude Code | `~/.claude/CLAUDE.md` |
| Kilo Code | Save to `~/.config/kilo/system-prompt.md`, then add `"~/.config/kilo/system-prompt.md"` to the `instructions` array in `~/.config/kilo/kilo.jsonc` |
| Codex CLI | `~/.codex/AGENTS.md` (or `~/.codex/AGENTS.override.md` for a temporary override) |

For Codex `/review`: copy `.claude/commands/review.md` (same content) to `~/.codex/prompts/review.md`. Invoke with `/prompts:review`.

**Delete after setup:**

- `system-prompt.md` (content lives globally now)
- `README.md` (reference only — not read by any agent)

## What each tool reads

| File | Claude Code | Kilo Code | Codex CLI |
|---|---|---|---|
| `CLAUDE.md` | Yes — imports `AGENTS.md` | Ignored | Ignored |
| `AGENTS.md` | Via `CLAUDE.md` import | Yes, directly | Yes, directly (walks repo root → cwd) |
| `agent_docs/*` | Lazy, when `AGENTS.md` points there | Same | Same |
| `.claude/commands/` | `/review` | Ignored | Ignored |
| `.kilo/commands/` | Ignored | `/review` | Ignored |
| `~/.codex/prompts/` | Ignored | Ignored | `/prompts:review` (global only) |

Using only one tool? Delete the other tools' folders. If Kilo-only or Codex-only, also delete `CLAUDE.md`.

## Setup

1. Extract the zip at your project root.
2. Paste `system-prompt.md`'s content into your tool's global slot (table above). Once per machine.
3. Codex users: also copy `.claude/commands/review.md` → `~/.codex/prompts/review.md`.
4. Fill in `AGENTS.md` from the actual repo. Verify every line.
5. Leave `agent_docs/*` as stubs — expand when the agent misses something concrete.
6. Verify it loaded:
   - Claude Code → run `/memory`, check the files are listed.
   - Kilo → ask "what instructions do you have?"
   - Codex → run `/status` in a session. Check the "Agents.md" line — if blank, the global bug hit you (see below).
7. Delete `system-prompt.md` and this `README.md` from the repo.

## Codex-specific notes

- **Size cap:** Codex silently truncates `AGENTS.md` past 32 KiB. Stay well under.
- **Precedence:** In each directory Codex walks (root → cwd), it checks `AGENTS.override.md` first, then `AGENTS.md`. Nested files override earlier ones.
- **Custom prompts are deprecated** in favor of Skills, but still work. If you want a shareable, repo-committed review workflow for Codex, look into Codex Skills — not covered here.

## Codex known bug: global `AGENTS.md` doesn't load

Tracking issue: [openai/codex#8759](https://github.com/openai/codex/issues/8759). Reproduces on codex-cli 0.77.0 and 0.78.0 (may or may not be fixed by the time you read this — check `/status`).

**Symptom:** you put your system-prompt content at `~/.codex/AGENTS.md` as documented, but Codex acts like it doesn't exist. Sessions in directories without a local `AGENTS.md` behave as if there's no global guidance at all.

**How to check:** run `/status` inside a Codex session. If the "Agents.md" line is blank, the file didn't load.

**Pick one workaround** (ranked, most reliable first):

1. **Put system-prompt content directly in every repo's `AGENTS.md`.** Simplest and always works. Downside: you edit it once per repo instead of once globally. If you only have a handful of repos, this is fine.

2. **Symlink the global into each repo.** From the repo root:
   ```bash
   ln -s ~/.codex/AGENTS.md AGENTS.codex.md
   ```
   Then add `AGENTS.codex.md` to `project_doc_fallback_filenames` in `~/.codex/config.toml`. Codex picks it up because it's now a local file. Single source of truth, no duplication.

3. **Loader prompt.** Create `~/.codex/prompts/load-agents.md`:
   ```markdown
   ---
   description: Load global AGENTS.md into this session
   ---
   Read and follow the contents of `~/.codex/AGENTS.md` as binding instructions for this session. Include the full contents verbatim in context.
   ```
   Then run `/prompts:load-agents` at the start of every Codex session. Manual and easy to forget — only use if you can't do #1 or #2.

4. **Set `CODEX_HOME` explicitly.** `export CODEX_HOME=~/.codex` in your shell profile. Some users report this helps; not confirmed to fix all cases.

**Recommended default for this kit:** workaround #1. It's boring but reliable — paste the system-prompt content at the top of each repo's `AGENTS.md`, above the project-specific sections. When the bug is fixed you can pull it back out to `~/.codex/AGENTS.md`.

## Growing it

- Add a line only after the agent got something concrete wrong.
- New rules go in `AGENTS.md` → Learnings. Promote up when durable.
- Anything a linter/formatter/hook can enforce → wire it up. Prompts are probabilistic; hooks always fire.
- Prune: for each line ask "would removing this cause a mistake?" If not, delete.

## Optional: path-scoped rules

`AGENTS.md`'s pointers rely on the agent's judgment to open `agent_docs/*` when relevant. Deterministic alternatives:

- **Claude Code:** `.claude/rules/<name>.md` with YAML frontmatter `paths: ["tests/**/*"]`
- **Kilo Code:** `.kilo/rules/<name>.md`, listed in `kilo.jsonc` → `instructions`
- **Codex CLI:** nested `AGENTS.md` files in subdirectories (e.g. `tests/AGENTS.md`) — Codex loads them when it walks into that directory

Reach for these only if a doc isn't getting read when it should.
