# 19. Anti-Patterns

หลีกเลี่ยงแบบนี้:

```txt
Cursor rules บอกอย่างหนึ่ง
Copilot instructions บอกอีกอย่าง
CLAUDE.md บอกอีกอย่าง
AGENTS.md บอกอีกอย่าง
harness agents บอกอีกอย่าง
```

เพราะ AI แต่ละตัวจะ generate code คนละ pattern

ควรเป็นแบบนี้:

```txt
docs/ai/*.md = source of truth
tool-specific files = adapter
```

---
