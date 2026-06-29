# 20. Final Summary

สำหรับ project ที่มีหลายคนและหลาย AI tool:

```txt
1. มี source of truth กลางใน docs/ai/
2. แต่ละ AI tool มี adapter ของตัวเอง
3. ทุก task ต้องเขียนเป็น markdown ที่ชัดเจน
4. Agent Harness ใช้ role + task + standard
5. Local model ต้องมี wrapper/harness อ่านไฟล์แล้ว inject prompt
6. ทุกงานต้องจบด้วย Definition of Done
```

จำง่ายที่สุด:

```txt
Rules      = กติกา
Context    = ระบบเป็นยังไง
Task       = รอบนี้ทำอะไร
Agent      = ใครทำ
Skill      = ทำตามวิธีไหน
Command    = ตรวจยังไง
Review     = ตรวจอะไร
Done       = จบเมื่อไหร่
```
