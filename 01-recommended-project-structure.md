# 1. Recommended Project Structure

โครงสร้างที่แนะนำสำหรับ project ที่ใช้หลาย AI tool:

```txt
project/
  docs/
    ai/
      TEAM_AI_STANDARD.md
      ARCHITECTURE.md
      FILE_OWNERSHIP.md
      COMMANDS.md
      BACKEND_STANDARD.md
      FRONTEND_STANDARD.md
      DATABASE_STANDARD.md
      TESTING_STANDARD.md
      REVIEW_STANDARD.md
      EXAMPLES.md
      DEFINITION_OF_DONE.md

  tasks/
    TASK_TEMPLATE.md
    TASK-001-case-detail-api.md
    TASK-002-case-detail-ui.md

  harness/
    agents/
      api-agent.md
      ui-agent.md
      test-agent.md
      review-agent.md

  .cursor/
    rules/
      project.mdc
      backend.mdc
      frontend.mdc
      testing.mdc
    agents/
      api-agent.md
      ui-agent.md
      test-agent.md
      review-agent.md
    skills/
      api-contract-skill/
        SKILL.md
      frontend-page-skill/
        SKILL.md

  .github/
    copilot-instructions.md
    instructions/
      backend.instructions.md
      frontend.instructions.md
      testing.instructions.md

  .claude/
    agents/
      api-agent.md
      ui-agent.md
    skills/
      api-contract-skill/
        SKILL.md

  CLAUDE.md
  AGENTS.md
  .cursorrules
```

หมายเหตุ:

- `docs/ai/*.md` คือกติกากลางที่ทุก tool ควรอ้างถึง
- `.cursor/rules/*.mdc` คือ adapter สำหรับ Cursor
- `.github/copilot-instructions.md` คือ adapter สำหรับ GitHub Copilot
- `CLAUDE.md` คือ adapter สำหรับ Claude Code
- `AGENTS.md` คือ adapter สำหรับ Codex และ generic agent tools
- `harness/agents/*.md` คือ role ของ agent ใน Agent Harness
- `tasks/*.md` คือใบงานที่คนหรือ AI หยิบไปทำ

---
