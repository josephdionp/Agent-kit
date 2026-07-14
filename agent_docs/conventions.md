# Conventions

Read when writing new code. If a linter/formatter enforces something
deterministically, leave it out of this file — enforcement beats prose.

## Naming

- Files: <pattern>
- Functions / methods: <pattern>
- Types / classes: <pattern>
- Constants / env vars: <pattern>

## Imports

- Style: <e.g. absolute from `src/`, ordered by group>
- Enforced by: `<linter rule>` (if any)

## Errors

- Throw vs return: <policy>
- Error types live in: `<file>`
- Never swallow exceptions — fail loudly with what broke and where.

## Configuration

- Env vars: `<file>` (`.env.example` if present)
- Config files: `<paths>`
- No hardcoded env-dependent values in logic.

## Logging

- Logger: `<name>`
- Levels used: <policy>
- Never log secrets, tokens, PII, or full request bodies.

## Documentation

- Where docstrings/comments go (if anywhere): <policy>
- Comment the *why*, not the *what*. Few, short, only where needed.
