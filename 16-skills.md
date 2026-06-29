# 16. Skills

### Concept

Skill คือคู่มือเฉพาะทาง เช่น API contract, frontend page, testing, code review, database query

```txt
Subagent = ใครทำ
Skill    = ทำตามวิธีไหน
Task     = รอบนี้ทำอะไร
```

### Example Structure

```txt
.cursor/
  skills/
    api-contract-skill/
      SKILL.md
    frontend-page-skill/
      SKILL.md
    testing-skill/
      SKILL.md
    code-review-skill/
      SKILL.md
```

### Example: API Contract Skill

````md
---
name: api-contract-skill
description: Use when implementing or changing backend API endpoints, DTOs, schemas, request/response contracts, or endpoint behavior.
---

# API Contract Skill

## Rules

- Do not return raw database entities directly.
- Validate params, query, and body.
- Keep response shape explicit.
- Reuse existing schema/contract files.
- Preserve backward compatibility unless task says otherwise.

## Workflow

1. Find existing similar endpoint.
2. Check route/controller.
3. Check service/usecase.
4. Check repository/query.
5. Update contract/schema.
6. Add or update tests.
````

### How each AI uses skills

```txt
Cursor      → native skill/subagent workflow if configured
Claude Code → can use .claude/skills or explicit prompt/context
Codex       → can use AGENTS.md + skills if configured by tool
Copilot     → usually references skill files as normal markdown context
Llama       → wrapper injects relevant SKILL.md manually
```

---
