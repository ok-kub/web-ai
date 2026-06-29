# 7. BACKEND_STANDARD.md

### Concept

ไฟล์นี้บอก pattern ของ backend เช่น controller/service/repository, DTO, validation, error handling, logging, authorization

### Location

```txt
docs/ai/BACKEND_STANDARD.md
```

### Example

````md
# Backend Standard

## Architecture

Use this flow:

Controller -> Service -> Repository -> Database

## Rules

- Validate params, query, and body.
- Do not return raw database entities directly.
- Use explicit DTOs or response schemas.
- Keep API response backward-compatible unless task says breaking change is allowed.
- Reuse existing error format.
- Do not bypass authorization checks.
- Keep business logic in service/usecase layer, not controller.

## Error Format

Use existing project error format. If none exists, use:

```json
{
  "code": "CASE_NOT_FOUND",
  "message": "Case not found"
}
```

## API Checklist

- Route added or updated
- Request validated
- Response shape explicit
- Error handling added
- Tests added or updated
````

### How each AI uses it

```txt
Cursor      → backend.mdc references this file
Copilot     → backend.instructions.md references this file
Claude Code → API Agent follows this file
Codex       → AGENTS.md Backend Work section references it
Llama       → harness injects this file for backend tasks
```

---
