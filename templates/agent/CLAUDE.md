# CLAUDE.md — [Project Name]

> This is your orientation file. Read it before touching anything.

---

## What this is

[One paragraph. What the system does, in business terms. Who it's for. What matters most.]

## What never to touch without asking

- [File/module/pattern that is sacred or fragile]
- [Anything with regulatory/compliance implications]

## Conventions

**Naming:** [e.g. snake_case for files, PascalCase for classes, kebab-case for routes]  
**File layout:** [where things go — models, services, controllers, utils]  
**Error handling:** [how errors are handled in this codebase — throw? return Result? log and swallow?]  
**Commits:** [format — e.g. `feat:`, `fix:`, `chore:` prefixes]

## How to run tests

```bash
# Run full suite
[command]

# Run single test
[command]

# Run before every commit — if tests fail, fix before committing
[command]
```

## How to run locally

```bash
[setup and start commands]
```

## Domain vocabulary

See `GLOSSARY.md`. Use the terms defined there, not your own interpretations.

## What's uncertain

See `docs/open-questions.md`. If you're unsure about something — check there before inventing an answer.

## Architecture

See `ARCHITECTURE.md` for the full picture. See per-directory CLAUDE.md files for local context.

## Security rules

See `SECURITY.md`. Non-negotiable.
