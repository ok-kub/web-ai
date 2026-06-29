# 6. COMMANDS.md

### Concept

ไฟล์นี้บอกคำสั่งติดตั้ง รัน dev, test, lint, build, typecheck เพื่อให้ AI ไม่เดาคำสั่งผิด

### Location

```txt
docs/ai/COMMANDS.md
```

### Example

````md
# Commands

## Package Manager

Use pnpm.

## Install

pnpm install

## Development

pnpm dev

## Type Check

pnpm typecheck

## Test All

pnpm test

## Test Backend

pnpm test:api

## Test Frontend

pnpm test:web

## Lint

pnpm lint

## Build

pnpm build

## Database

pnpm db:migrate
pnpm db:seed

## Notes

- Prefer targeted test command first.
- Do not run migration commands unless the task explicitly involves database schema.
````

### How each AI uses it

```txt
Cursor      → uses it before terminal commands
Copilot     → references it when suggesting commands
Claude Code → uses it in coding workflow
Codex       → reads from AGENTS.md reference
Llama       → wrapper injects it when command execution is needed
```

---
