# 0. Core Concept

ในโปรเจกต์จริง ไม่ควรมีแค่ `instruction` หรือ `rules` อย่างเดียว เพราะ AI ต้องรู้มากกว่านั้น เช่น architecture, command, task, ownership, testing, review, examples และ definition of done

ให้คิดแบบนี้:

```txt
Rules               = กฎบ้าน / ห้ามทำอะไร / ต้องทำอะไร
Architecture        = ระบบนี้จัดโครงสร้างยังไง
Ownership           = role ไหนแก้ไฟล์ไหนได้
Task                = งานรอบนี้คืออะไร
Commands            = run/test/build ยังไง
Standards           = backend/frontend/database/test ต้องทำตาม pattern ไหน
Examples            = ดู pattern จากไฟล์ไหน
Review Checklist    = ตรวจอะไรบ้างก่อนจบงาน
Definition of Done  = งานเสร็จจริงเมื่อไหร่
```

หลักสำคัญที่สุด:

```txt
docs/ai/*.md = source of truth ของทีม
tool-specific files = adapter ให้แต่ละ AI อ่าน
tasks/*.md = ใบงานเฉพาะรอบ
harness/agents/*.md = role ของ agent ใน workflow
```

---
