# CONVENTIONS.md — [Project Name]

> The unwritten rules, written down. Prevents code that works but looks foreign.

---

## Naming

| Thing | Convention | Example |
|---|---|---|
| Files | | `user-service.ts` |
| Classes | | `UserService` |
| Functions | | `getUserById` |
| Constants | | `MAX_RETRY_COUNT` |
| Database tables | | `user_sessions` |
| API endpoints | | `/api/v1/users/:id` |
| Environment variables | | `DATABASE_URL` |

## File layout

```
src/
  [explain what goes where]
```

## Error handling

[How errors are handled in this codebase. Throw? Return Result/Either type? Log and swallow? Pick one and describe it.]

```typescript
// Example of the correct error handling pattern in this repo
```

## Testing patterns

- Test framework: [Jest / Vitest / pytest / etc.]
- Test location: [co-located with source / separate `tests/` dir]
- What to test: [unit / integration / e2e / all three]
- Test naming: [describe what the test verifies — e.g. `it('sends email when invoice is created')`]
- Coverage expectation: [e.g. all new code must have unit tests / happy path + one error case minimum]

```bash
# Run tests
[command]

# Run single test file
[command]
```

## Commit format

```
type(scope): short description

# Types: feat | fix | chore | refactor | docs | test
# Example: feat(billing): add retry logic for failed invoice sends
```

## Code review expectations

[What gets flagged in PR review? What's the bar for "good enough"?]

## Things that surprise new people

[The non-obvious stuff. What does every new developer get wrong about this codebase?]
