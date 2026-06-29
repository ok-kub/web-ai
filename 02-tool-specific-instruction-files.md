# 2. Tool-Specific Instruction Files

### 2.1 Cursor

Cursor ใช้ได้หลายแบบ:

```txt
.cursor/rules/*.mdc  = project rules แบบใหม่
.cursorrules         = legacy / แบบเก่า
.cursor/agents/*.md  = Cursor subagents
.cursor/skills/*     = Cursor skills
```

ตัวอย่าง:

```txt
.cursor/rules/project.mdc
```

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

Core rules:

- Follow existing architecture.
- Keep changes minimal and scoped to the assigned task.
- Do not refactor unrelated code.
- Do not change database schema unless the task explicitly allows it.
- Run relevant tests or type checks when possible.
- Summarize changed files, commands run, and risks.
````

การใช้งานกับ Cursor:

```txt
Use api-agent.

Task:
Read tasks/TASK-001-case-detail-api.md and implement it.

Follow:
- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/BACKEND_STANDARD.md
- docs/ai/DATABASE_STANDARD.md
- docs/ai/TESTING_STANDARD.md
```

---

### 2.2 GitHub Copilot

Copilot ใช้ไฟล์หลัก:

```txt
.github/copilot-instructions.md
```

และอาจแยก instruction ตาม domain ได้:

```txt
.github/instructions/backend.instructions.md
.github/instructions/frontend.instructions.md
.github/instructions/testing.instructions.md
```

ตัวอย่าง:

````md
# GitHub Copilot Instructions

Follow the shared team standard:

- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/ARCHITECTURE.md
- docs/ai/COMMANDS.md

When editing backend code, follow:

- docs/ai/BACKEND_STANDARD.md
- docs/ai/DATABASE_STANDARD.md

When editing frontend code, follow:

- docs/ai/FRONTEND_STANDARD.md

When writing tests, follow:

- docs/ai/TESTING_STANDARD.md

Rules:

- Keep changes scoped to the task.
- Do not refactor unrelated code.
- Do not add dependencies without justification.
- Never generate real secrets or production credentials.
````

การใช้งานกับ Copilot Chat:

```txt
Please implement the task in tasks/TASK-001-case-detail-api.md.
Follow the repo instructions and existing backend patterns.
Do not change the database schema.
```

---

### 2.3 Claude Code

Claude Code ใช้ไฟล์หลัก:

```txt
CLAUDE.md
```

และสามารถมีโฟลเดอร์เสริม:

```txt
.claude/
  agents/
  skills/
  settings.json
```

ตัวอย่าง `CLAUDE.md`:

````md
# Claude Code Instructions

This repository uses shared AI standards.

Always read and follow:

- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/ARCHITECTURE.md
- docs/ai/COMMANDS.md
- docs/ai/DEFINITION_OF_DONE.md

Before coding:

1. Read the assigned task from tasks/ if provided.
2. Inspect similar existing code.
3. Identify affected files.
4. Make the smallest safe change.

Do not:

- Refactor unrelated files.
- Change database schema unless task explicitly allows it.
- Add dependencies without explaining why.
- Remove validation, authorization, or audit logging.

After coding:

- Run relevant tests or typecheck when possible.
- Summarize files changed.
- Report risks and assumptions.
````

การใช้งานกับ Claude Code:

```txt
Read CLAUDE.md, then implement tasks/TASK-001-case-detail-api.md.
Use the API Agent role if available.
Run relevant tests and summarize the result.
```

---

### 2.4 Codex

Codex ใช้ไฟล์หลัก:

```txt
AGENTS.md
```

ตัวอย่าง:

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
- Do not add dependencies without justification.
- Run relevant tests or type checks when possible.
- Summarize changed files, commands run, and risks.

## Backend Work

Follow:

- docs/ai/BACKEND_STANDARD.md
- docs/ai/DATABASE_STANDARD.md

## Frontend Work

Follow:

- docs/ai/FRONTEND_STANDARD.md

## Testing Work

Follow:

- docs/ai/TESTING_STANDARD.md
````

การใช้งานกับ Codex:

```txt
Implement tasks/TASK-001-case-detail-api.md.
Follow AGENTS.md and all referenced docs/ai standards.
Do not change database schema.
```

---

### 2.5 Llama / Ollama / Local AI / Other Models

Llama, Qwen, Mistral, DeepSeek, Ollama, LM Studio, llama.cpp, vLLM เป็น model/runtime เป็นหลัก ไม่ใช่ project-aware coding agent โดยตรง

ดังนั้น:

```txt
Model เองไม่อ่าน repo
Tool / wrapper / harness เป็นคนอ่าน repo แล้วป้อน context ให้ model
```

วิธีใช้งานมี 3 แบบ:

#### แบบที่ 1: Copy instruction ใส่ prompt เอง

```txt
You are an AI coding assistant for this repository.

Follow:
- AGENTS.md
- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/BACKEND_STANDARD.md

Task:
Implement pagination for audit logs API.
```

#### แบบที่ 2: ใช้ tool ที่ต่อ local model ได้

ตัวอย่าง tool:

```txt
Cline
Continue
Aider
Open Interpreter
custom Agent Harness
```

flow:

```txt
Cline / Continue / Aider
        ↓
อ่านไฟล์ใน repo
        ↓
ประกอบ prompt + context
        ↓
ส่งเข้า Ollama / LM Studio / local model
```

#### แบบที่ 3: ทำ script เอง

````bash
#!/usr/bin/env bash

TASK_FILE="$1"

cat <<EOF > /tmp/ai-task.md
You are an AI coding assistant for this repository.

Repository instructions:

$(cat AGENTS.md)

Team standard:

$(cat docs/ai/TEAM_AI_STANDARD.md)

Task:

$(cat "$TASK_FILE")
EOF

ollama run llama3.1 < /tmp/ai-task.md
````

ใช้แบบนี้:

```bash
./scripts/run-local-ai.sh tasks/TASK-001-case-detail-api.md
```

---
