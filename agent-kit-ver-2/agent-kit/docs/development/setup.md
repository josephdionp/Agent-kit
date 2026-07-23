# Setup

## Prereqs

- <runtime version>
- <package manager version>
- <optional: docker>

## First run

```sh
<install command>
<setup command>
<run command>
```

## Commands

Verified against `package.json` / `Makefile`.

- Install: `<cmd>`
- Test (single): `<cmd>`
- Test (all): `<cmd>`
- Lint / typecheck / format: `<cmd>` / `<cmd>` / `<cmd>`
- Build: `<cmd>`
- Run: `<cmd>`
- Migrate: `<cmd>` (if applicable)

## Env vars

- `<VAR>` — required for <what>. Dev fallback: <yes/no>.

## Do not hand-edit

`.env*`, `.devcontainer/`, lockfiles, `.git/`, CI/Docker, generated code.
