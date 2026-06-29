# 17. Example End-to-End Workflow

### Scenario

ทำหน้า case detail:

```txt
/overview/case/:trackingCode
```

ต้องมี API:

```txt
GET /cases/:trackingCode/detail
```

### Suggested task split

```txt
tasks/TASK-001-case-detail-api.md
tasks/TASK-002-case-detail-ui.md
tasks/TASK-003-case-detail-tests.md
tasks/TASK-004-case-detail-review.md
```

### Cursor prompt

```txt
Use api-agent with api-contract-skill.

Read and implement:
tasks/TASK-001-case-detail-api.md

Follow:
- docs/ai/TEAM_AI_STANDARD.md
- docs/ai/BACKEND_STANDARD.md
- docs/ai/DATABASE_STANDARD.md
- docs/ai/TESTING_STANDARD.md

Do not modify frontend.
Run related tests or typecheck.
Summarize changed files and risks.
```

### Copilot prompt

```txt
Implement tasks/TASK-001-case-detail-api.md.
Follow .github/copilot-instructions.md and the referenced docs/ai standards.
Do not modify frontend or database schema.
```

### Claude Code prompt

```txt
Read CLAUDE.md first.
Then implement tasks/TASK-001-case-detail-api.md.
Use the API Agent role from harness/agents/api-agent.md.
Run relevant checks and summarize the result.
```

### Codex prompt

```txt
Follow AGENTS.md.
Implement tasks/TASK-001-case-detail-api.md.
Use docs/ai/BACKEND_STANDARD.md, DATABASE_STANDARD.md, and TESTING_STANDARD.md.
```

### Llama/Ollama harness prompt shape

```txt
You are the API Agent.

Repository instructions:
[AGENTS.md]

Team standard:
[docs/ai/TEAM_AI_STANDARD.md]

Architecture:
[docs/ai/ARCHITECTURE.md]

Backend standard:
[docs/ai/BACKEND_STANDARD.md]

Database standard:
[docs/ai/DATABASE_STANDARD.md]

Agent role:
[harness/agents/api-agent.md]

Task:
[tasks/TASK-001-case-detail-api.md]

Return:
- Plan
- Files to inspect
- Proposed changes
- Commands to run
- Risks
```

---
