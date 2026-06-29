# 8. FRONTEND_STANDARD.md

### Concept

ไฟล์นี้บอก pattern ของ frontend เช่น page/component/API client/state/loading/error/empty state

### Location

```txt
docs/ai/FRONTEND_STANDARD.md
```

### Example

````md
# Frontend Standard

## Rules

- Reuse existing components before creating new ones.
- Follow existing page and route structure.
- Keep API calls in the existing API client/service layer.
- Do not hardcode production data.
- Handle loading, empty, and error states.
- Avoid new state management libraries unless explicitly approved.
- Keep UI consistent with the existing design system.

## Page Checklist

- Route params handled
- API call implemented through service/client
- Loading state
- Empty state
- Error state
- Success state
- Type-safe data mapping
````

### How each AI uses it

```txt
Cursor      → frontend.mdc references this file
Copilot     → frontend.instructions.md references this file
Claude Code → UI Agent follows this file
Codex       → AGENTS.md Frontend Work section references it
Llama       → wrapper injects it for frontend tasks
```

---
