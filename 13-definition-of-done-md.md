# 13. DEFINITION_OF_DONE.md

### Concept

ไฟล์นี้บอกว่า “งานเสร็จ” ต้องมีอะไร ไม่ใช่แค่ code compile ผ่าน

### Location

```txt
docs/ai/DEFINITION_OF_DONE.md
```

### Example

````md
# Definition of Done

A task is done when:

- Code is implemented within the assigned scope.
- No unrelated files are changed.
- API contract is documented if changed.
- Loading, empty, and error states are handled for UI work.
- Relevant tests or type checks pass.
- Security and authorization are not weakened.
- Query performance risk is considered for database work.
- Final summary includes:
  - Files changed
  - What changed
  - Commands/tests run
  - Risks or follow-up needed
````

### How each AI uses it

```txt
Cursor      → final summary should match this file
Copilot     → prompt Copilot to check against Definition of Done
Claude Code → CLAUDE.md references it after coding
Codex       → AGENTS.md references it as completion criteria
Llama       → wrapper includes it near the end of prompt
```

---
