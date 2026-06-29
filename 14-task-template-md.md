# 14. TASK_TEMPLATE.md

### Concept

Task คือใบงานเฉพาะรอบ ช่วยให้ AI ไม่หลุด scope

ถ้าให้ AI แค่ “ทำหน้านี้ให้หน่อย” โอกาสหลุดสูงมาก ควรให้ task ที่มี Goal, Scope, Out of Scope, Acceptance Criteria, Files Likely Involved

### Location

```txt
tasks/TASK_TEMPLATE.md
```

### Example

````md
# Task: [Title]

## Metadata

| Field | Value |
|---|---|
| Created | YYYY-MM-DD |
| Owner | GitHub username or name |
| Agent role | API Agent / UI Agent / Test Agent / Review Agent / DevOps Agent |
| Status | TODO / IN PROGRESS / BLOCKED / DONE |
| Branch | feat/<slug> |

## Goal

One paragraph describing what must be true when this task is complete.

## Background

Context the agent needs. Business reason, existing behavior, decisions already made.

## Scope

- [ ] Item 1
- [ ] Item 2

## Out of Scope

- Do not refactor unrelated code.
- Do not change database schema unless noted.

## Files Likely Involved

```txt
apps/api/src/...
libs/schemas/src/...
```

## Acceptance Criteria

- [ ] Expected behavior works
- [ ] Error case handled
- [ ] Tests added or updated
- [ ] Relevant commands pass

## Notes for AI

Follow:

- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/ARCHITECTURE.md
- docs/ai/COMMANDS.md
- docs/ai/DEFINITION_OF_DONE.md
````

### How each AI uses it

```txt
Cursor      → “Use api-agent. Read tasks/TASK-001.md.”
Copilot     → paste task path into Copilot Chat
Claude Code → “Read CLAUDE.md and tasks/TASK-001.md”
Codex       → “Implement tasks/TASK-001.md following AGENTS.md”
Llama       → wrapper injects task content into prompt
```

---
