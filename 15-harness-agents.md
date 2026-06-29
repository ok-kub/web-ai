# 15. Harness Agents

### Concept

Agent Harness คือระบบจัดงาน multi-agent ระดับ project ส่วน `harness/agents/*.md` คือ role ของ agent ในระบบนั้น

Cursor จะไม่เอา `harness/agents/*.md` ไปใช้เป็น subagent เองอัตโนมัติ ถ้าอยากให้ Cursor ใช้ ต้องสร้าง `.cursor/agents/*.md` เป็น adapter หรือสั่งให้ Cursor อ่านไฟล์ harness เอง

### Location

```txt
harness/agents/api-agent.md
harness/agents/ui-agent.md
harness/agents/test-agent.md
harness/agents/review-agent.md
```

### Example: API Agent

````md
# API Agent

Follow:

- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/BACKEND_STANDARD.md
- docs/ai/DATABASE_STANDARD.md
- docs/ai/TESTING_STANDARD.md

## Scope

Allowed:

- apps/api/**
- libs/schemas/**
- libs/database/**
- tests/api/**

Not allowed:

- apps/web/**
- unrelated refactor
- database schema change unless the task explicitly allows it

## Deliverables

- API implementation
- Updated contract/schema if needed
- Tests
- Summary of changed files
- Risks or follow-up
````

### Cursor subagent adapter

```txt
.cursor/agents/api-agent.md
```

````md
---
name: api-agent
description: Backend API implementation agent that follows the project harness API role.
tools:
  - read_file
  - edit_file
  - grep
  - terminal
---

You are the API Agent.

Before doing any task:

1. Read harness/agents/api-agent.md
2. Read the assigned task file from tasks/
3. Follow relevant docs/ai standards
4. Follow relevant skills from .cursor/skills if available

Do not modify files outside the API Agent scope.
````

---
