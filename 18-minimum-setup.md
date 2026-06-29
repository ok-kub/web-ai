# 18. Minimum Setup

ถ้าไม่อยากเริ่มเยอะเกิน ให้เริ่มแค่ชุดนี้ก่อน:

```txt
project/
  docs/
    ai/
      TEAM_AI_STANDARD.md
      ARCHITECTURE.md
      COMMANDS.md
      BACKEND_STANDARD.md
      FRONTEND_STANDARD.md
      DATABASE_STANDARD.md
      TESTING_STANDARD.md
      REVIEW_STANDARD.md
      DEFINITION_OF_DONE.md

  tasks/
    TASK_TEMPLATE.md

  .cursor/
    rules/
      project.mdc

  .github/
    copilot-instructions.md

  CLAUDE.md
  AGENTS.md
```

แล้วค่อยเพิ่มทีหลัง:

```txt
harness/agents/*.md
.cursor/agents/*.md
.cursor/skills/*/SKILL.md
.github/instructions/*.instructions.md
.claude/agents/*.md
.claude/skills/*/SKILL.md
```

---
