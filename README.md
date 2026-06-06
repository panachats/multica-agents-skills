# DPLUS Agent Skills

11 skills (knowledge packs) สำหรับ agent ใน Multica แต่ละโฟลเดอร์มี `SKILL.md` ตามมาตรฐาน Anthropic Agent Skills — import เข้า Multica ได้ตรง ๆ

## วิธี import เข้า Multica

มี 2 วิธีหลัก:

**A. New (พิมพ์/วางใน UI)** — เร็วสุดสำหรับเริ่มต้น
- ไปที่ Skills → New → วางเนื้อหาจาก `SKILL.md` ของแต่ละโฟลเดอร์ ทำทีละตัว

**B. From GitHub** — เหมาะถ้าอยากให้ทีมใช้ร่วมและ version ได้
1. push โฟลเดอร์นี้ขึ้น GitHub repo
2. Skills → From GitHub → วาง URL ของแต่ละ skill เช่น
   `https://github.com/<you>/<repo>/tree/main/agent-skills/sql-conventions`

จากนั้น **attach** skill เข้า agent ที่เกี่ยวข้อง (1 skill attach ได้หลาย agent)

## Attach skill ↔ agent

| Skill | Attach กับ agent |
|---|---|
| `prd-writing`, `task-breakdown` | pm-orchestrator |
| `design-system-tokens`, `ui-component-mapping` | ui-designer (+ frontend-dev) |
| `dbschema-erd` | solution-architect |
| `domain-context` | solution-architect, backend-dev |
| `sql-conventions`, `erp-linked-server` | backend-dev |
| `frontend-component` | frontend-dev |
| `sql-injection-review` | security-analyst |
| `user-manual` | tech-writer |

## ⚠️ ต้องเติมค่าจริงก่อนใช้

2 ตัวนี้เป็นโครง มี `TODO` ข้างใน ต้องเติมค่าของทีมก่อน:
- **`design-system-tokens`** — ใส่สี/ฟอนต์/spacing จริง (จาก Figma หรือ AntD theme)
- **`user-manual`** — เลือกภาษา/ชื่อแอป/ที่เก็บคู่มือ

## ⚠️ ความปลอดภัย

- **`domain-context`** — ถ้ามีชื่อระบบภายในที่ sensitive แนะนำเก็บเป็น **local / private** workspace skill อย่า push ขึ้น public repo
- Multica ไม่ sandbox skill จากภายนอก ตรวจ `SKILL.md` ทุกตัวก่อน import (ตัวในชุดนี้คุณเขียนเอง ปลอดภัย)

## หมายเหตุ

- แก้ skill แล้ว เฉพาะ task ใหม่ถึงจะได้เวอร์ชันใหม่ — task ที่กำลังรันอยู่ใช้ของเดิม
- skill เหล่านี้อ้างถึงกันเอง (เช่น `sql-conventions` ชี้ไป `domain-context`) — attach เป็นชุดจะได้ผลดีสุด
