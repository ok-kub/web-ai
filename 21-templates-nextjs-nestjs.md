# 21. Templates — Next.js + NestJS

Template ชุดนี้ใช้สำหรับ project ที่มี stack:

- **Frontend**: Next.js 14+ (App Router) + TypeScript + Tailwind CSS
- **Backend**: NestJS + TypeScript
- **Database**: PostgreSQL
- **Monorepo**: pnpm workspaces

copy ไฟล์ด้านล่างไปใส่ใน repo แล้วปรับตามจริง

---

## ไฟล์ที่ต้องสร้าง

```txt
project/
  CLAUDE.md
  AGENTS.md
  .cursor/
    rules/
      project.mdc
  .github/
    copilot-instructions.md
  docs/
    ai/
      TEAM_AI_STANDARD.md
      ARCHITECTURE.md
      BACKEND_STANDARD.md
      FRONTEND_STANDARD.md
      DATABASE_STANDARD.md
      TESTING_STANDARD.md
      COMMANDS.md
      DEFINITION_OF_DONE.md
  tasks/
    TASK_TEMPLATE.md
```

---

## CLAUDE.md

````md
# Claude Code Instructions

This repository uses a NestJS (API) + Next.js (Web) monorepo.

Always read and follow:
- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/ARCHITECTURE.md
- docs/ai/COMMANDS.md
- docs/ai/DEFINITION_OF_DONE.md

Before coding:
1. Read the assigned task from tasks/ if provided.
2. Inspect similar existing code in the relevant app.
3. Identify affected files.
4. Make the smallest safe change.

When working on backend (apps/api):
- Follow docs/ai/BACKEND_STANDARD.md
- Follow docs/ai/DATABASE_STANDARD.md

When working on frontend (apps/web):
- Follow docs/ai/FRONTEND_STANDARD.md

When writing tests:
- Follow docs/ai/TESTING_STANDARD.md

Do not:
- Refactor unrelated files.
- Change database schema unless task explicitly allows it.
- Add npm packages without explaining why.
- Remove validation, authorization, or audit logging.
- Import backend code directly in frontend — use HTTP API only.

After coding:
- Run: pnpm typecheck && pnpm test
- Summarize files changed, commands run, and risks.
````

---

## AGENTS.md

````md
# AGENTS.md

This repository is maintained by humans and AI agents.

All agents must follow:
- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/ARCHITECTURE.md
- docs/ai/COMMANDS.md
- docs/ai/DEFINITION_OF_DONE.md

## Agent Rules

- Before starting, check tasks/ for a task file matching the assigned task.
- Keep changes scoped to the assigned task.
- Do not refactor unrelated code.
- Do not change database schema unless explicitly requested.
- Do not add npm packages without justification.
- Run: pnpm typecheck && pnpm test before reporting done.
- Summarize changed files, commands run, and risks.

## Backend Work (apps/api — NestJS)

Follow:
- docs/ai/BACKEND_STANDARD.md
- docs/ai/DATABASE_STANDARD.md

## Frontend Work (apps/web — Next.js)

Follow:
- docs/ai/FRONTEND_STANDARD.md

## Testing Work

Follow:
- docs/ai/TESTING_STANDARD.md
````

---

## .cursor/rules/project.mdc

````md
---
description: Global project rules
alwaysApply: true
---

# Cursor Project Rules

Read and follow:
- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/ARCHITECTURE.md
- docs/ai/COMMANDS.md
- docs/ai/DEFINITION_OF_DONE.md

Stack: NestJS (apps/api) + Next.js App Router (apps/web) + PostgreSQL

Core rules:
- Before starting, check tasks/ for a task file matching the assigned task.
- Follow existing architecture before creating a new pattern.
- Keep changes minimal and scoped to the assigned task.
- Do not refactor unrelated code.
- Do not change database schema unless the task explicitly allows it.
- Do not add npm packages without justification.
- Run pnpm typecheck && pnpm test when possible.
- Summarize changed files, commands run, and risks.
````

---

## .github/copilot-instructions.md

````md
# GitHub Copilot Instructions

Stack: NestJS (apps/api) + Next.js App Router (apps/web) + PostgreSQL

Follow shared team standard:
- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/ARCHITECTURE.md
- docs/ai/COMMANDS.md

When editing backend code (apps/api), follow:
- docs/ai/BACKEND_STANDARD.md
- docs/ai/DATABASE_STANDARD.md

When editing frontend code (apps/web), follow:
- docs/ai/FRONTEND_STANDARD.md

When writing tests, follow:
- docs/ai/TESTING_STANDARD.md

Rules:
- Keep changes scoped to the task.
- Do not refactor unrelated code.
- Do not add npm packages without justification.
- Never generate real secrets or production credentials.
- Do not import backend modules directly in frontend — call the API.
````

---

## docs/ai/TEAM_AI_STANDARD.md

````md
# Team AI Standard

## Goal

Keep code consistent, maintainable, testable, and safe for both humans and AI agents.

## Global Rules

- Follow existing architecture before creating a new pattern.
- Keep changes minimal and scoped to the assigned task.
- Do not refactor unrelated code.
- Do not change database schema unless the task explicitly allows it.
- Do not introduce new npm packages without explaining why.
- Prefer explicit TypeScript types — avoid `any` and `unknown` unless justified.
- Add or update tests when changing business logic.
- Never commit secrets, tokens, private keys, or real credentials.

## Required Final Summary

Every AI task must end with:

1. Files changed
2. What changed and why
3. Commands/tests run and their output
4. Risks or follow-up needed
````

---

## docs/ai/ARCHITECTURE.md

````md
# Architecture

## Stack

- **Frontend**: Next.js 14+ (App Router), TypeScript, Tailwind CSS — `apps/web`
- **Backend**: NestJS, TypeScript — `apps/api`
- **Database**: PostgreSQL
- **Monorepo**: pnpm workspaces

## Project Layout

```
apps/
  web/                    ← Next.js frontend
    src/
      app/                ← App Router pages and layouts
      components/         ← Shared UI components
      lib/                ← API client, auth helpers, utils
  api/                    ← NestJS backend
    src/
      modules/
        <domain>/
          <domain>.controller.ts
          <domain>.service.ts
          <domain>.repository.ts
          dto/
      main.ts
packages/
  shared/                 ← Shared TypeScript types (optional)
```

## Data Flow

```
Browser
  → Next.js Server Component / Route Handler
  → NestJS REST API (HTTP, /api/v1/*)
  → PostgreSQL
```

## Key Constraints

- Frontend never imports from `apps/api` directly — use HTTP API only.
- All backend routes are prefixed `/api/v1/`.
- Auth is handled by NestJS middleware; frontend reads a session cookie.
- Shared types live in `packages/shared` or are intentionally duplicated.
- Database migrations are managed separately — never auto-migrated in production.
````

---

## docs/ai/BACKEND_STANDARD.md

````md
# Backend Standard (NestJS)

## Architecture

```
Controller → Service → Repository → PostgreSQL
```

## Module Structure

Each domain has its own NestJS module:

```
src/modules/<domain>/
  <domain>.module.ts
  <domain>.controller.ts
  <domain>.service.ts
  <domain>.repository.ts
  dto/
    create-<domain>.dto.ts
    update-<domain>.dto.ts
    <domain>-response.dto.ts
```

## Rules

- Validate all request params, query strings, and bodies using class-validator DTOs.
- Never return raw database entities — always map to a response DTO.
- Keep business logic in the service layer, not controllers or repositories.
- Reuse the existing error format; do not invent new HTTP status codes.
- Do not bypass guards or authorization decorators.
- Keep API responses backward-compatible unless task explicitly allows breaking changes.

## Error Format

```json
{
  "code": "RESOURCE_NOT_FOUND",
  "message": "Resource not found"
}
```

## API Checklist

- Route added to controller with correct HTTP method and path
- Request DTO with validation decorators
- Response DTO with explicit types
- Service method with business logic
- Repository method for DB access
- Unit tests for service
- E2E test for the route
````

---

## docs/ai/FRONTEND_STANDARD.md

````md
# Frontend Standard (Next.js App Router)

## Architecture

```
app/
  (public)/         ← unauthenticated routes
  (protected)/      ← authenticated routes (wrapped by auth layout)
  layout.tsx        ← root layout
components/
  ui/               ← generic UI primitives (Button, Input, etc.)
  <domain>/         ← domain-specific components
lib/
  api/              ← typed API client functions
  auth/             ← session helpers
```

## Rules

- Use Server Components by default; add `"use client"` only when needed (event handlers, hooks, browser APIs).
- Fetch data in Server Components or Route Handlers — never expose API keys to the client.
- All API calls go through `lib/api/` helper functions — never call `fetch` directly in a component.
- Use TypeScript for all files; avoid `any`.
- Style with Tailwind CSS utility classes — do not write custom CSS unless unavoidable.
- Forms use controlled inputs or a form library (e.g., React Hook Form); always validate before submit.
- Loading and error states must be handled — use `loading.tsx` and `error.tsx` conventions.

## Naming

- Page files: `page.tsx` inside the route folder.
- Components: PascalCase, one component per file.
- Hooks: `use<Name>.ts` in `lib/hooks/`.
````

---

## docs/ai/DATABASE_STANDARD.md

````md
# Database Standard (PostgreSQL)

## Rules

- Never auto-migrate in production — migrations are explicit SQL files or ORM migration files.
- Do not change schema unless the task explicitly allows it.
- Always add indexes for foreign keys and columns used in WHERE/ORDER BY clauses.
- Use transactions for multi-table writes.
- Never store secrets, tokens, or PII in plain text — hash or encrypt before insert.
- Use parameterized queries — never concatenate user input into SQL strings.

## Naming Conventions

- Tables: `snake_case`, plural (e.g., `user_profiles`)
- Columns: `snake_case`
- Foreign keys: `<table>_id` (e.g., `user_id`)
- Indexes: `idx_<table>_<column>` (e.g., `idx_orders_user_id`)
- Migrations: `<timestamp>_<description>.sql`

## Query Guidelines

- SELECT only the columns you need — avoid `SELECT *` in application code.
- Paginate large result sets — do not return unbounded lists.
- Log slow queries (>100ms) for investigation.
````

---

## docs/ai/TESTING_STANDARD.md

````md
# Testing Standard

## Stack

- **Backend unit tests**: Jest (NestJS default)
- **Backend e2e tests**: Jest + Supertest
- **Frontend unit tests**: Vitest + React Testing Library
- **E2E browser tests**: Playwright

## Rules

- Test behavior, not implementation — avoid testing private methods or internal state.
- One assertion per test when possible; name tests as "should <do something> when <condition>".
- Mock external dependencies (HTTP calls, email service) — never call real external APIs in tests.
- Do not mock the database in backend tests — use a test database seeded with fixtures.
- Keep test files next to the code they test: `<name>.spec.ts`.
- Do not write tests that always pass regardless of the implementation.

## Coverage Targets

- Business logic (services): 80%+ line coverage
- Controllers: covered by e2e tests, not unit tests
- UI components: smoke test (renders without crashing) + interaction tests for forms

## Commands

```bash
# Backend
pnpm --filter api test          # unit tests
pnpm --filter api test:e2e      # e2e tests

# Frontend
pnpm --filter web test          # unit tests
pnpm --filter web test:e2e      # Playwright
```
````

---

## docs/ai/COMMANDS.md

````md
# Commands

## Install dependencies

```bash
pnpm install
```

## Development

```bash
pnpm --filter api dev     # NestJS on :3001
pnpm --filter web dev     # Next.js on :3000
pnpm dev                  # both (requires turbo or concurrently)
```

## Type check

```bash
pnpm typecheck            # runs tsc --noEmit for all apps
```

## Test

```bash
pnpm test                 # all unit tests
pnpm test:e2e             # all e2e tests
```

## Build

```bash
pnpm build                # builds all apps
```

## Database

```bash
pnpm db:migrate           # run pending migrations
pnpm db:seed              # seed dev data
```
````

---

## docs/ai/DEFINITION_OF_DONE.md

````md
# Definition of Done

A task is DONE when all of the following are true:

- [ ] Code compiles with no TypeScript errors (`pnpm typecheck` passes)
- [ ] All existing tests pass (`pnpm test` passes)
- [ ] New or modified business logic has tests covering the happy path and at least one error case
- [ ] No `console.log` or debug statements left in production code
- [ ] No hardcoded secrets, tokens, or credentials
- [ ] API response shape matches the agreed contract or DTO
- [ ] PR description includes: what changed, why, and how to test
- [ ] No unrelated files were modified
````

---

## tasks/TASK_TEMPLATE.md

````md
# TASK-XXX: <Short title>

## Goal

<One sentence: what this task must achieve.>

## Scope

**In scope:**
- <specific thing to do>

**Out of scope:**
- <specific thing NOT to do>
- Do not change database schema unless listed above.

## Acceptance Criteria

- [ ] <Verifiable outcome 1>
- [ ] <Verifiable outcome 2>
- [ ] Tests pass: `pnpm test`
- [ ] TypeScript compiles: `pnpm typecheck`

## References

- Related file: `apps/api/src/modules/<domain>/`
- Standard to follow: `docs/ai/BACKEND_STANDARD.md`
````
