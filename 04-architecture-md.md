# 4. ARCHITECTURE.md

### Concept

ไฟล์นี้อธิบายภาพรวมระบบ เพื่อให้ AI รู้ว่า frontend/backend/shared libs/database อยู่ตรงไหน และ data flow เป็นยังไง

ถ้าไม่มีไฟล์นี้ AI มักสร้าง folder หรือ pattern ใหม่เอง

### Location

```txt
docs/ai/ARCHITECTURE.md
```

### Example

````md
# Architecture

## Apps

- apps/api: Backend API
- apps/web: Frontend web app
- libs/schemas: Shared request/response schemas
- libs/database: Database access layer

## Backend Flow

Controller -> Service -> Repository -> Database

## Frontend Flow

Page -> Component -> API Client -> Backend API

## Shared Contracts

Frontend and backend must use shared schemas from libs/schemas when available.

## Do Not Create

- New architecture layer without approval
- New shared library without approval
- New database abstraction without approval
````

### How each AI uses it

```txt
Cursor      → alwaysApply rule tells Cursor to read ARCHITECTURE.md
Copilot     → copilot-instructions.md links this file
Claude Code → CLAUDE.md tells Claude to inspect architecture before coding
Codex       → AGENTS.md references this file
Llama       → wrapper includes this file when task affects architecture or multiple modules
```

---
