# 12. EXAMPLES.md

### Concept

AI มักทำตามตัวอย่างได้ดีกว่าอ่าน rule อย่างเดียว ไฟล์นี้บอกว่าเวลาทำ API/page/test/query ให้ดูไฟล์ไหนเป็น reference

### Location

```txt
docs/ai/EXAMPLES.md
```

### Example

````md
# Examples and Existing Patterns

## Backend Endpoint Pattern

Use these files as reference:

- apps/api/src/cases/cases.controller.ts
- apps/api/src/cases/cases.service.ts
- apps/api/src/cases/cases.repository.ts
- libs/schemas/src/cases/case-detail.schema.ts

## Frontend Page Pattern

Use these files as reference:

- apps/web/src/app/overview/case-list/page.tsx
- apps/web/src/features/cases/components/case-table.tsx
- apps/web/src/features/cases/api/case-api.ts

## Test Pattern

Use these files as reference:

- apps/api/src/cases/__tests__/cases.controller.spec.ts
- apps/web/src/features/cases/__tests__/case-table.test.tsx

## SQL Query Pattern

Use these files as reference:

- libs/database/src/repositories/case.repository.ts
- libs/database/src/queries/paginated-list.sql
````

### How each AI uses it

```txt
Cursor      → ask Cursor to inspect examples before editing
Copilot     → Copilot uses examples from open workspace/context
Claude Code → CLAUDE.md says inspect similar code first
Codex       → AGENTS.md says follow examples
Llama       → wrapper can inject only the relevant example section
```

---
