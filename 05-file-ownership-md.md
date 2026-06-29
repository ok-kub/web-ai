# 5. FILE_OWNERSHIP.md

### Concept

ไฟล์นี้บอกว่า role หรือ agent ไหนแก้ไฟล์ไหนได้ ช่วยป้องกัน AI แก้ข้าม scope เช่น API Agent ไปแก้ frontend หรือ UI Agent ไปแก้ database migration

### Location

```txt
docs/ai/FILE_OWNERSHIP.md
```

### Example

````md
# File Ownership

## API Agent

Allowed:

- apps/api/**
- libs/schemas/**
- libs/database/**
- tests/api/**

Not allowed:

- apps/web/**
- mobile/**
- infra/**

## UI Agent

Allowed:

- apps/web/**
- libs/ui/**
- tests/web/**

Not allowed:

- apps/api/**
- database migrations
- infra/**

## Test Agent

Allowed:

- tests/**
- apps/**/__tests__/**
- *.spec.ts
- *.test.ts

Not allowed:

- Large production refactor without explicit task scope

## DevOps Agent

Allowed:

- infra/**
- helm/**
- k8s/**
- Dockerfile
- docker-compose.yml
- .github/workflows/**
````

### How each AI uses it

```txt
Cursor Subagents → api-agent/ui-agent should read this before editing
Copilot          → use as reference in prompt or repo instruction
Claude Code      → CLAUDE.md should mention it before coding
Codex            → AGENTS.md should mention it for all tasks
Llama            → harness should inject the relevant ownership section only
```

---
