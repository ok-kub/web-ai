# Templates & FAQ — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add two new content sections to the docs site: (1) ready-to-copy AI harness template files for a Next.js + NestJS stack, and (2) a Thai-language Troubleshooting / FAQ page covering the 10 most common AI harness problems.

**Architecture:** All new content is markdown files in the repo root (matching the existing pattern). Docsify serves them automatically. The sidebar (`_sidebar.md`) is updated last to wire both pages into the navigation. Tasks 1 and 2 are independent and can be done in either order; Task 3 depends on both.

**Tech Stack:** Markdown, Docsify 4 (CDN), existing `_sidebar.md` nav pattern

## Global Constraints

- All new `.md` files go in repo root `/Users/ananchaiphahupongsub/work/web-ai/` — no subdirectories (matches existing pattern)
- Page prose is in Thai (matching existing site language)
- Template file *contents* (inside code blocks) are in English (engineers copy them into their projects)
- Do not move, rename, or modify any existing `.md` files except `_sidebar.md`
- Do not add npm packages or change `vercel.json`, `index.html`, or `package.json`
- Filenames follow the existing numbering convention: `21-*.md`, `22-*.md`
- Verify locally with `python3 -m http.server 3000` after each task

---

## File Structure

```
web-ai/
├── 21-templates-nextjs-nestjs.md   ← CREATE (Task 1)
├── 22-troubleshooting-faq.md       ← CREATE (Task 2)
└── _sidebar.md                     ← MODIFY (Task 3) — add Templates + Troubleshooting sections
```

---

### Task 1: Next.js + NestJS template bundle page

**Files:**
- Create: `21-templates-nextjs-nestjs.md`

**Interfaces:**
- Produces: a page at `/#/21-templates-nextjs-nestjs` with 12 copy-ready template files

- [ ] **Step 1: Create `21-templates-nextjs-nestjs.md`**

Create `/Users/ananchaiphahupongsub/work/web-ai/21-templates-nextjs-nestjs.md` with this exact content:

```markdown
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
```

- [ ] **Step 2: Verify page renders locally**

```bash
cd /Users/ananchaiphahupongsub/work/web-ai
python3 -m http.server 3000 &
sleep 2
curl -s http://localhost:3000/21-templates-nextjs-nestjs.md | head -5
kill %1
```

Expected: first line is `# 21. Templates — Next.js + NestJS`

- [ ] **Step 3: Commit**

```bash
cd /Users/ananchaiphahupongsub/work/web-ai
git add 21-templates-nextjs-nestjs.md
git commit -m "content: add Next.js + NestJS AI harness template bundle"
```

---

### Task 2: Troubleshooting / FAQ page

**Files:**
- Create: `22-troubleshooting-faq.md`

**Interfaces:**
- Produces: a page at `/#/22-troubleshooting-faq` with 10 common problems + solutions in Thai

- [ ] **Step 1: Create `22-troubleshooting-faq.md`**

Create `/Users/ananchaiphahupongsub/work/web-ai/22-troubleshooting-faq.md` with this exact content:

```markdown
# 22. Troubleshooting & FAQ

ปัญหาที่พบบ่อยเมื่อเริ่มใช้ AI harness ในโปรเจกต์จริง และวิธีแก้

---

## 1. AI แก้ไขไฟล์นอก scope ที่ assign ไว้

**อาการ:** AI ไปแก้ไฟล์อื่นที่ไม่เกี่ยวกับ task เช่น แก้ component อื่น หรือเปลี่ยน config โดยไม่ได้บอก

**สาเหตุ:** Task description กว้างเกินไป หรือ instruction ไม่ได้ระบุ boundary ชัดเจน

**แก้:**
```txt
เพิ่มใน task file:

Out of scope:
- Do not modify any file outside apps/api/src/modules/user/
- Do not change database schema
- Do not touch frontend
```

และเพิ่มใน CLAUDE.md / AGENTS.md:
```txt
Keep changes scoped to the assigned task.
Do not refactor unrelated code.
```

---

## 2. AI สร้าง pattern ใหม่แทนที่จะใช้ pattern เดิมที่มีอยู่

**อาการ:** Codebase มี pattern ชัดเจน (เช่น Controller→Service→Repository) แต่ AI เขียน logic ใน controller โดยตรง หรือสร้าง class รูปแบบใหม่

**สาเหตุ:** AI ไม่รู้ว่า codebase ใช้ pattern อะไร เพราะ ARCHITECTURE.md ไม่ครอบคลุม หรือไม่ได้อ้างอิงใน instruction

**แก้:**
1. เพิ่ม architecture diagram ใน `docs/ai/ARCHITECTURE.md` ให้ชัดขึ้น
2. ใส่ตัวอย่าง existing code ใน task file:
```txt
Reference existing pattern:
apps/api/src/modules/case/case.service.ts
```
3. ระบุใน task: "Follow the same structure as the existing module at apps/api/src/modules/case/"

---

## 3. AI แต่ละ tool ให้ผลลัพธ์คนละแบบสำหรับ task เดียวกัน

**อาการ:** Cursor สร้าง code แบบหนึ่ง, Claude Code สร้างแบบอื่น, Copilot สร้างแบบที่สาม — ทำให้ codebase มี pattern หลายแบบ

**สาเหตุ:** Anti-pattern หลัก: tool-specific files แต่ละตัวบอกกติกาคนละชุด

**แก้:** ทำตาม single source of truth pattern:
```txt
docs/ai/*.md       = กติกากลาง (แก้ที่เดียว)
CLAUDE.md          = อ้างถึง docs/ai/ เท่านั้น
AGENTS.md          = อ้างถึง docs/ai/ เท่านั้น
.cursor/rules/*.mdc = อ้างถึง docs/ai/ เท่านั้น
```

ดู: [Anti-Patterns](19-anti-patterns.md)

---

## 4. AI เพิ่ม npm package โดยไม่ได้ขออนุญาต

**อาการ:** AI รัน `npm install some-library` แล้ว commit เข้ามาโดยไม่บอก

**แก้:** เพิ่มใน CLAUDE.md / AGENTS.md / tool rules:
```txt
Do not add npm packages without:
1. Explaining why the existing codebase cannot solve this.
2. Listing alternatives considered.
3. Getting explicit approval in the task description.
```

ถ้า AI ติด package ไปแล้ว: ให้ revert แล้วเพิ่มชื่อ package ที่ต้องการใน task file พร้อมเหตุผล

---

## 5. AI เปลี่ยน database schema โดยไม่ได้รับอนุญาต

**อาการ:** AI สร้าง migration file หรือเปลี่ยน entity โดยตัวเอง ทั้งที่ task ไม่ได้บอกให้ทำ

**สาเหตุ:** อันตรายมาก เพราะ schema change กระทบ production data

**แก้:** ระบุ explicit ในทุก task file ที่ไม่ต้องการ schema change:
```txt
Out of scope:
- Do not change database schema
- Do not create migration files
```

และใน DATABASE_STANDARD.md:
```txt
Never auto-migrate. Migrations are explicit and reviewed separately.
```

---

## 6. AI ไม่อ่าน instruction file ที่กำหนดไว้

**อาการ:** AI ทำงานโดยไม่ follow กติกาใน CLAUDE.md หรือ docs/ai/ ทั้งที่ตั้งไว้แล้ว

**สาเหตุ:** บาง tool ต้องการ explicit prompt ให้อ่านก่อน ไม่ใช่อ่านอัตโนมัติทุกครั้ง

**แก้ตาม tool:**

```txt
Claude Code:  เริ่ม session ด้วย "Read CLAUDE.md first."
Cursor:       ใช้ alwaysApply: true ใน .cursor/rules/*.mdc
Copilot:      ไม่อ่านอัตโนมัติ — ต้อง reference ใน chat prompt
Codex:        AGENTS.md อ่านอัตโนมัติ แต่ระบุ path ให้ชัดใน task
Llama/Local:  harness ต้อง inject ไฟล์เข้า prompt เองทุกครั้ง
```

---

## 7. AI generate code ที่มีช่องโหว่ด้าน security

**อาการ:** เช่น SQL ที่ concatenate user input, API ที่ไม่มี auth check, หรือ log ที่พิมพ์ sensitive data

**แก้:**
1. เพิ่ม security rules ใน TEAM_AI_STANDARD.md:
```txt
Never concatenate user input into SQL — use parameterized queries.
Do not bypass authorization guards.
Do not log passwords, tokens, or PII.
Never commit secrets or credentials.
```

2. เพิ่ม security checklist ใน DEFINITION_OF_DONE.md:
```txt
- [ ] No SQL injection vectors (parameterized queries used)
- [ ] Auth guard present on protected routes
- [ ] No secrets in code or logs
```

3. Review AI output ก่อน merge เสมอ — AI code review ไม่แทน human review

---

## 8. AI เขียน test ที่ไม่มีประโยชน์ (test ที่ pass เสมอ)

**อาการ:** Test ผ่านทุกครั้งแต่ไม่ได้ verify พฤติกรรมจริง เช่น `expect(true).toBe(true)` หรือ mock ทุกอย่างจน test ไม่ทดสอบอะไรจริงๆ

**แก้:** เพิ่มใน TESTING_STANDARD.md:
```txt
- Test behavior, not implementation.
- A test must fail if the implementation is wrong.
- Do not mock the function under test.
- Assert on the actual output, not on whether a mock was called.
```

ตัวอย่าง test ที่ดี:
```typescript
it('should return 404 when case not found', async () => {
  const res = await request(app).get('/api/v1/cases/INVALID-CODE');
  expect(res.status).toBe(404);
  expect(res.body.code).toBe('CASE_NOT_FOUND');
});
```

---

## 9. AI hallucinate function หรือ API ที่ไม่มีอยู่จริง

**อาการ:** AI เรียก `this.caseService.getByTrackingCode()` แต่ method นั้นไม่มีใน service จริง ทำให้ compile error

**สาเหตุ:** AI ไม่ได้อ่าน existing code จริงก่อน implement

**แก้:** บอก AI ให้อ่านก่อนทำ:
```txt
Before implementing, read:
- apps/api/src/modules/case/case.service.ts
- apps/api/src/modules/case/case.repository.ts

Use only methods that already exist. If you need a new method, define it first.
```

และเพิ่มใน instruction:
```txt
Before coding, inspect similar existing code to understand the available methods and patterns.
```

---

## 10. AI ช้าลงหรือตอบแย่ลงเมื่อ context ยาวขึ้น

**อาการ:** เมื่อ inject docs/ai/ files ทั้งหมดเข้า context AI เริ่ม confuse หรือทำตาม rule ไม่ครบ

**สาเหตุ:** Context window มี limit — ยิ่ง inject เยอะ ยิ่งเพิ่มโอกาสที่ AI จะ "ลืม" บางส่วน

**แก้:**
```txt
อย่า inject ทุก docs/ai/*.md ในทุก task
inject เฉพาะที่เกี่ยวข้องกับ task นั้น:

Backend task  → TEAM_AI_STANDARD + ARCHITECTURE + BACKEND_STANDARD + DATABASE_STANDARD
Frontend task → TEAM_AI_STANDARD + ARCHITECTURE + FRONTEND_STANDARD
Test task     → TEAM_AI_STANDARD + TESTING_STANDARD
```

ดู: [Harness Agents](15-harness-agents.md) สำหรับการแบ่ง agent ตาม role

---

## ยังแก้ไม่ได้?

ถ้าปัญหายังอยู่หลังลองทั้งหมดแล้ว:

1. ตรวจสอบว่า AI tool version อัปเดตแล้ว
2. ลอง model อื่นใน tool เดียวกัน (เช่น เปลี่ยนจาก Sonnet → Opus)
3. Break task ให้เล็กลง — task ที่ใหญ่เกินไปทำให้ AI เดา scope ผิด
4. เพิ่ม example ของ expected output ใน task file
```

- [ ] **Step 2: Verify page renders locally**

```bash
cd /Users/ananchaiphahupongsub/work/web-ai
python3 -m http.server 3000 &
sleep 2
curl -s http://localhost:3000/22-troubleshooting-faq.md | head -5
kill %1
```

Expected: first line is `# 22. Troubleshooting & FAQ`

- [ ] **Step 3: Commit**

```bash
cd /Users/ananchaiphahupongsub/work/web-ai
git add 22-troubleshooting-faq.md
git commit -m "content: add troubleshooting and FAQ page"
```

---

### Task 3: Update sidebar to wire both new pages

**Files:**
- Modify: `_sidebar.md`

**Interfaces:**
- Consumes: `21-templates-nextjs-nestjs.md` (Task 1), `22-troubleshooting-faq.md` (Task 2)
- Produces: updated sidebar with Templates and Troubleshooting sections visible in nav

- [ ] **Step 1: Read current `_sidebar.md`**

Read `/Users/ananchaiphahupongsub/work/web-ai/_sidebar.md` to confirm current content before editing.

Expected current content (verify it matches):
```markdown
- [Home](README.md)
- **Getting Started**
  - [Overview](00-overview.md)
  - [Core Concept](00-core-concept.md)
- **Setup**
  - [Recommended Project Structure](01-recommended-project-structure.md)
  - [Tool-Specific Instruction Files](02-tool-specific-instruction-files.md)
  - [Minimum Setup](18-minimum-setup.md)
- **Standards**
  - [Team AI Standard](03-team-ai-standard-md.md)
  - [Architecture](04-architecture-md.md)
  - [File Ownership](05-file-ownership-md.md)
  - [Commands](06-commands-md.md)
  - [Backend Standard](07-backend-standard-md.md)
  - [Frontend Standard](08-frontend-standard-md.md)
  - [Database Standard](09-database-standard-md.md)
  - [Testing Standard](10-testing-standard-md.md)
  - [Review Standard](11-review-standard-md.md)
- **Reference**
  - [Examples](12-examples-md.md)
  - [Definition of Done](13-definition-of-done-md.md)
  - [Task Template](14-task-template-md.md)
  - [Harness Agents](15-harness-agents.md)
  - [Skills](16-skills.md)
- **Advanced**
  - [End-to-End Workflow](17-example-end-to-end-workflow.md)
  - [Anti-Patterns](19-anti-patterns.md)
  - [Final Summary](20-final-summary.md)
```

- [ ] **Step 2: Replace `_sidebar.md` with updated content**

Write `/Users/ananchaiphahupongsub/work/web-ai/_sidebar.md` with this exact content:

```markdown
- [Home](README.md)
- **Getting Started**
  - [Overview](00-overview.md)
  - [Core Concept](00-core-concept.md)
- **Setup**
  - [Recommended Project Structure](01-recommended-project-structure.md)
  - [Tool-Specific Instruction Files](02-tool-specific-instruction-files.md)
  - [Minimum Setup](18-minimum-setup.md)
- **Standards**
  - [Team AI Standard](03-team-ai-standard-md.md)
  - [Architecture](04-architecture-md.md)
  - [File Ownership](05-file-ownership-md.md)
  - [Commands](06-commands-md.md)
  - [Backend Standard](07-backend-standard-md.md)
  - [Frontend Standard](08-frontend-standard-md.md)
  - [Database Standard](09-database-standard-md.md)
  - [Testing Standard](10-testing-standard-md.md)
  - [Review Standard](11-review-standard-md.md)
- **Reference**
  - [Examples](12-examples-md.md)
  - [Definition of Done](13-definition-of-done-md.md)
  - [Task Template](14-task-template-md.md)
  - [Harness Agents](15-harness-agents.md)
  - [Skills](16-skills.md)
- **Templates**
  - [Next.js + NestJS](21-templates-nextjs-nestjs.md)
- **Advanced**
  - [End-to-End Workflow](17-example-end-to-end-workflow.md)
  - [Anti-Patterns](19-anti-patterns.md)
  - [Final Summary](20-final-summary.md)
- **Troubleshooting**
  - [FAQ](22-troubleshooting-faq.md)
```

- [ ] **Step 3: Verify sidebar and both pages render locally**

```bash
cd /Users/ananchaiphahupongsub/work/web-ai
python3 -m http.server 3000 &
sleep 2
curl -s http://localhost:3000/_sidebar.md | grep -E "Templates|Troubleshooting|21-|22-"
kill %1
```

Expected output (all 4 lines must appear):
```
- **Templates**
  - [Next.js + NestJS](21-templates-nextjs-nestjs.md)
- **Troubleshooting**
  - [FAQ](22-troubleshooting-faq.md)
```

- [ ] **Step 4: Commit and push**

```bash
cd /Users/ananchaiphahupongsub/work/web-ai
git add _sidebar.md
git commit -m "nav: add Templates and Troubleshooting sections to sidebar"
git push origin main
```

Expected: push succeeds, GitHub Actions deploy run starts within ~10 seconds.

- [ ] **Step 5: Verify GitHub Actions deploy completes**

```bash
sleep 30 && gh run list --repo ok-kub/web-ai --workflow=deploy.yml --limit 1 --json status,conclusion | cat
```

Expected:
```json
[{"conclusion":"success","status":"completed"}]
```

---

## Self-Review

**Spec coverage:**
- Next.js + NestJS template bundle → Task 1 (`21-templates-nextjs-nestjs.md`, 12 template files as code blocks)
- Troubleshooting / FAQ (10 problems) → Task 2 (`22-troubleshooting-faq.md`, 10 items)
- Site navigation wired → Task 3 (`_sidebar.md` updated with Templates + Troubleshooting sections)
- Deploy to Vercel → Task 3 Step 4-5 (`git push` triggers GitHub Actions)
- Thai prose → confirmed in Tasks 2 and 3; template file contents in English as required
- No existing files modified except `_sidebar.md` → confirmed
- No npm packages added → confirmed

**Placeholder scan:** None — all steps contain exact file content, exact commands, and expected output.

**Type consistency:** N/A — no custom code, only markdown content.
