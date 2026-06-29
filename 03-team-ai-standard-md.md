# 3. TEAM_AI_STANDARD.md

### Concept

ไฟล์นี้คือกติกากลางของทีม เป็น source of truth ที่ทุก AI tool ต้องอ้างถึง

ไม่ควรเขียน rules ซ้ำหลายที่ เพราะจะทำให้ Cursor, Copilot, Claude, Codex ทำงานคนละแนว

### Location

```txt
docs/ai/TEAM_AI_STANDARD.md
```

### Example

````md
# Team AI Standard

## Goal

Keep code consistent, maintainable, testable, and safe for both humans and AI agents.

## Global Rules

- Follow existing architecture before creating a new pattern.
- Keep changes minimal and scoped to the assigned task.
- Do not refactor unrelated code.
- Do not change database schema unless the task explicitly allows it.
- Do not introduce new dependencies without explaining why.
- Prefer explicit types over implicit or any-like types.
- Add or update tests when changing business logic.
- Never commit secrets, tokens, private keys, or real credentials.

## Required Final Summary

Every AI task must end with:

1. Files changed
2. What changed
3. Commands/tests run
4. Risks or follow-up needed
````

### How each AI uses it

```txt
Cursor      → .cursor/rules/project.mdc references this file
Copilot     → .github/copilot-instructions.md references this file
Claude Code → CLAUDE.md references this file
Codex       → AGENTS.md references this file
Llama       → wrapper/harness reads this file and injects it into prompt
```

---
