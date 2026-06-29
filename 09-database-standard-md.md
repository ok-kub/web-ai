# 9. DATABASE_STANDARD.md

### Concept

ไฟล์นี้ใช้ควบคุมงาน database/query/migration โดยเฉพาะงานที่มี performance risk เช่น join, pagination, count, indexes

### Location

```txt
docs/ai/DATABASE_STANDARD.md
```

### Example

````md
# Database Standard

## Rules

- Do not change schema unless the task explicitly allows it.
- Do not add migration without clear requirement.
- Use pagination for list APIs.
- Avoid SELECT * in production queries.
- Use explicit column names.
- Check existing indexes before proposing new ones.
- Explain query performance risk when adding joins, filters, or counts.
- Keep SQL readable and parameterized.

## Pagination

Prefer the existing project pattern.

If no pattern exists:

- Use limit/offset for simple admin lists.
- Use cursor pagination for large or time-ordered data.

## Query Checklist

- Filters are indexed or justified
- Pagination is applied for list endpoints
- Count query is separated when needed
- No raw user input in SQL string
- Join cardinality is understood
````

### How each AI uses it

```txt
Cursor      → database.mdc references this file
Copilot     → referenced from copilot-instructions.md
Claude Code → API Agent must read it before DB work
Codex       → AGENTS.md references it for backend/database work
Llama       → harness injects it for SQL tasks
```

---
