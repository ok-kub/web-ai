# 11. REVIEW_STANDARD.md

### Concept

ไฟล์นี้ใช้สำหรับ review-agent หรือก่อน merge PR ให้ AI ตรวจ correctness, security, performance, maintainability และ test coverage

### Location

```txt
docs/ai/REVIEW_STANDARD.md
```

### Example

````md
# Review Standard

## Review Focus

Check:

- Correctness
- Type safety
- Error handling
- Security
- Authorization
- Query performance
- Test coverage
- Maintainability
- Unrelated changes
- Breaking API changes

## Severity

Critical:

- Security vulnerability
- Data loss
- Broken production behavior

Major:

- Incorrect logic
- Missing validation
- Bad query performance
- Missing important tests

Minor:

- Naming
- Readability
- Small duplication

## Output Format

For each issue:

- File
- Severity
- Problem
- Why it matters
- Suggested fix
````

### How each AI uses it

```txt
Cursor      → review-agent + code-review-skill follows it
Copilot     → Copilot Chat can review PR/diff using it
Claude Code → Review Agent follows it
Codex       → use for review task in AGENTS.md
Llama       → wrapper injects it with git diff
```

---
