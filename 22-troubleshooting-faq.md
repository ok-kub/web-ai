# 22. Troubleshooting & FAQ

ปัญหาที่พบบ่อยเมื่อเริ่มใช้ AI harness ในโปรเจกต์จริง และวิธีแก้

---

## 1. AI แก้ไขไฟล์นอก scope ที่ assign ไว้

**อาการ:** AI ไปแก้ไฟล์อื่นที่ไม่เกี่ยวกับ task เช่น แก้ component อื่น หรือเปลี่ยน config โดยไม่ได้บอก

**สาเหตุ:** Task description กว้างเกินไป หรือ instruction ไม่ได้ระบุ boundary ชัดเจน

**แก้:**
```txt
เพิ่มใน task file:

Out of scope:
- Do not modify any file outside apps/api/src/modules/user/
- Do not change database schema
- Do not touch frontend
```

และเพิ่มใน CLAUDE.md / AGENTS.md:
```txt
Keep changes scoped to the assigned task.
Do not refactor unrelated code.
```

---

## 2. AI สร้าง pattern ใหม่แทนที่จะใช้ pattern เดิมที่มีอยู่

**อาการ:** Codebase มี pattern ชัดเจน (เช่น Controller→Service→Repository) แต่ AI เขียน logic ใน controller โดยตรง หรือสร้าง class รูปแบบใหม่

**สาเหตุ:** AI ไม่รู้ว่า codebase ใช้ pattern อะไร เพราะ ARCHITECTURE.md ไม่ครอบคลุม หรือไม่ได้อ้างอิงใน instruction

**แก้:**
1. เพิ่ม architecture diagram ใน `docs/ai/ARCHITECTURE.md` ให้ชัดขึ้น
2. ใส่ตัวอย่าง existing code ใน task file:
```txt
Reference existing pattern:
apps/api/src/modules/case/case.service.ts
```
3. ระบุใน task: "Follow the same structure as the existing module at apps/api/src/modules/case/"

---

## 3. AI แต่ละ tool ให้ผลลัพธ์คนละแบบสำหรับ task เดียวกัน

**อาการ:** Cursor สร้าง code แบบหนึ่ง, Claude Code สร้างแบบอื่น, Copilot สร้างแบบที่สาม — ทำให้ codebase มี pattern หลายแบบ

**สาเหตุ:** Anti-pattern หลัก: tool-specific files แต่ละตัวบอกกติกาคนละชุด

**แก้:** ทำตาม single source of truth pattern:
```txt
docs/ai/*.md       = กติกากลาง (แก้ที่เดียว)
CLAUDE.md          = อ้างถึง docs/ai/ เท่านั้น
AGENTS.md          = อ้างถึง docs/ai/ เท่านั้น
.cursor/rules/*.mdc = อ้างถึง docs/ai/ เท่านั้น
```

ดู: [Anti-Patterns](19-anti-patterns.md)

---

## 4. AI เพิ่ม npm package โดยไม่ได้ขออนุญาต

**อาการ:** AI รัน `npm install some-library` แล้ว commit เข้ามาโดยไม่บอก

**แก้:** เพิ่มใน CLAUDE.md / AGENTS.md / tool rules:
```txt
Do not add npm packages without:
1. Explaining why the existing codebase cannot solve this.
2. Listing alternatives considered.
3. Getting explicit approval in the task description.
```

ถ้า AI ติด package ไปแล้ว: ให้ remove ออกก่อน แล้วค่อยเพิ่มชื่อ package ที่ต้องการใน task file พร้อมเหตุผล
```bash
pnpm remove <package-name>
# หรือถ้า commit ไปแล้ว
git revert HEAD
```

---

## 5. AI เปลี่ยน database schema โดยไม่ได้รับอนุญาต

**อาการ:** AI สร้าง migration file หรือเปลี่ยน entity โดยตัวเอง ทั้งที่ task ไม่ได้บอกให้ทำ

**สาเหตุ:** อันตรายมาก เพราะ schema change กระทบ production data

**แก้:** ระบุ explicit ในทุก task file ที่ไม่ต้องการ schema change:
```txt
Out of scope:
- Do not change database schema
- Do not create migration files
```

และใน DATABASE_STANDARD.md:
```txt
Never auto-migrate. Migrations are explicit and reviewed separately.
```

---

## 6. AI ไม่อ่าน instruction file ที่กำหนดไว้

**อาการ:** AI ทำงานโดยไม่ follow กติกาใน CLAUDE.md หรือ docs/ai/ ทั้งที่ตั้งไว้แล้ว

**สาเหตุ:** บาง tool ต้องการ explicit prompt ให้อ่านก่อน ไม่ใช่อ่านอัตโนมัติทุกครั้ง

**แก้ตาม tool:**

```txt
Claude Code:  เริ่ม session ด้วย "Read CLAUDE.md first."
Cursor:       ใช้ alwaysApply: true ใน .cursor/rules/*.mdc
Copilot:      ไม่อ่านอัตโนมัติ — ต้อง reference ใน chat prompt
Codex:        AGENTS.md อ่านอัตโนมัติ แต่ระบุ path ให้ชัดใน task
Llama/Local:  harness ต้อง inject ไฟล์เข้า prompt เองทุกครั้ง
```

---

## 7. AI generate code ที่มีช่องโหว่ด้าน security

**อาการ:** เช่น SQL ที่ concatenate user input, API ที่ไม่มี auth check, หรือ log ที่พิมพ์ sensitive data

**แก้:**
1. เพิ่ม security rules ใน TEAM_AI_STANDARD.md:
```txt
Never concatenate user input into SQL — use parameterized queries.
Do not bypass authorization guards.
Do not log passwords, tokens, or PII.
Never commit secrets or credentials.
```

2. เพิ่ม security checklist ใน DEFINITION_OF_DONE.md:
```txt
- [ ] No SQL injection vectors (parameterized queries used)
- [ ] Auth guard present on protected routes
- [ ] No secrets in code or logs
```

3. Review AI output ก่อน merge เสมอ — AI code review ไม่แทน human review

---

## 8. AI เขียน test ที่ไม่มีประโยชน์ (test ที่ pass เสมอ)

**อาการ:** Test ผ่านทุกครั้งแต่ไม่ได้ verify พฤติกรรมจริง เช่น `expect(true).toBe(true)` หรือ mock ทุกอย่างจน test ไม่ทดสอบอะไรจริงๆ

**แก้:** เพิ่มใน TESTING_STANDARD.md:
```txt
- Test behavior, not implementation.
- A test must fail if the implementation is wrong.
- Do not mock the function under test.
- Assert on the actual output, not on whether a mock was called.
```

ตัวอย่าง test ที่ดี:
```typescript
it('should return 404 when case not found', async () => {
  const res = await request(app).get('/api/v1/cases/INVALID-CODE');
  expect(res.status).toBe(404);
  expect(res.body.code).toBe('CASE_NOT_FOUND');
});
```

---

## 9. AI hallucinate function หรือ API ที่ไม่มีอยู่จริง

**อาการ:** AI เรียก `this.caseService.getByTrackingCode()` แต่ method นั้นไม่มีใน service จริง ทำให้ compile error

**สาเหตุ:** AI ไม่ได้อ่าน existing code จริงก่อน implement

**แก้:** บอก AI ให้อ่านก่อนทำ:
```txt
Before implementing, read:
- apps/api/src/modules/case/case.service.ts
- apps/api/src/modules/case/case.repository.ts

Use only methods that already exist. If you need a new method, define it first.
```

และเพิ่มใน instruction:
```txt
Before coding, inspect similar existing code to understand the available methods and patterns.
```

---

## 10. AI ช้าลงหรือตอบแย่ลงเมื่อ context ยาวขึ้น

**อาการ:** เมื่อ inject docs/ai/ files ทั้งหมดเข้า context AI เริ่ม confuse หรือทำตาม rule ไม่ครบ

**สาเหตุ:** Context window มี limit — ยิ่ง inject เยอะ ยิ่งเพิ่มโอกาสที่ AI จะ "ลืม" บางส่วน

**แก้:**
```txt
อย่า inject ทุก docs/ai/*.md ในทุก task
inject เฉพาะที่เกี่ยวข้องกับ task นั้น:

Backend task  → TEAM_AI_STANDARD + ARCHITECTURE + BACKEND_STANDARD + DATABASE_STANDARD
Frontend task → TEAM_AI_STANDARD + ARCHITECTURE + FRONTEND_STANDARD
Test task     → TEAM_AI_STANDARD + TESTING_STANDARD
```

ดู: [Harness Agents](15-harness-agents.md) สำหรับการแบ่ง agent ตาม role

---

## 11. ไม่แน่ใจว่า AI อ่าน instruction จริงหรือเปล่า

**อาการ:** ตั้งค่า CLAUDE.md / AGENTS.md ไปแล้ว แต่ไม่รู้ว่า AI follow จริง หรือแค่ ignore

**วิธีทดสอบ:** ส่ง prompt นี้ให้ AI ก่อนเริ่มงานจริง:

```txt
Read CLAUDE.md and summarize the rules you must follow in this project.
List each rule as a bullet point.
```

ถ้า AI ตอบได้ถูกต้อง = อ่านแล้ว follow
ถ้า AI ตอบไม่ได้ หรือ summarize ผิด = ไม่ได้อ่าน ให้ลอง:

1. เริ่ม session ใหม่
2. ระบุชื่อไฟล์ใน prompt: `"Read CLAUDE.md first, then..."`
3. ตรวจสอบว่า CLAUDE.md อยู่ใน root ของ project จริง (ไม่ใช่ใน subfolder)

**สำหรับ Cursor:** ตรวจว่า `.cursor/rules/*.mdc` มี `alwaysApply: true`
**สำหรับ Copilot:** ต้อง reference ไฟล์ใน chat prompt ทุกครั้ง — ไม่ auto-read
**สำหรับ Codex:** AGENTS.md อ่านอัตโนมัติ แต่ path ต้องอยู่ที่ root

---

## ยังแก้ไม่ได้?

ถ้าปัญหายังอยู่หลังลองทั้งหมดแล้ว:

1. ตรวจสอบว่า AI tool version อัปเดตแล้ว
2. ลอง model อื่นใน tool เดียวกัน (เช่น เปลี่ยนจาก Sonnet → Opus)
3. Break task ให้เล็กลง — task ที่ใหญ่เกินไปทำให้ AI เดา scope ผิด
4. เพิ่ม example ของ expected output ใน task file
