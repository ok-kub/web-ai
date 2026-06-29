# 10. TESTING_STANDARD.md

### Concept

ไฟล์นี้บอกว่า AI ต้อง test อะไรบ้าง และห้ามเขียน test แบบเปราะเกินไป

### Location

```txt
docs/ai/TESTING_STANDARD.md
```

### Example

````md
# Testing Standard

## Rules

- Test behavior, not implementation details.
- Follow existing test style and helpers.
- Add tests when changing business logic.
- Do not rewrite test setup unless explicitly asked.
- Keep tests deterministic.

## Backend Test Checklist

- Success case
- Not found case
- Validation error
- Permission error if relevant
- Repository/service behavior if mocked

## Frontend Test Checklist

- Loading state
- Success state
- Empty state
- Error state
- User interaction if relevant
````

### How each AI uses it

```txt
Cursor      → testing.mdc references this file
Copilot     → testing.instructions.md references this file
Claude Code → Test Agent follows this file
Codex       → AGENTS.md Testing Work section references it
Llama       → wrapper injects it for test tasks
```

---
