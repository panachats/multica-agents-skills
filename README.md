# Agent Skills

10 skills สำหรับ dev office ใน Multica ตามมาตรฐาน Anthropic Agent Skills

---

## Agent flow

```mermaid
flowchart TD
    U([User: Issue + ระบบ + Stack])
    U --> PM

    PM["pm-orchestrator (Opus)\nprd-writing · task-breakdown · domain-context"]

    PM -->|PRD + tasks| ARCH
    PM -->|PRD + tasks| DES

    ARCH["solution-architect (Opus)\ndomain-context · dbschema-erd\nsystem-design-adr · openapi-contract"]
    DES["ui-designer (Sonnet)\ndesign-system-tokens · ui-component-mapping\nfigma-handoff"]

    ARCH -->|contract + schema| BE
    ARCH -->|contract| FE
    DES -->|design spec| FE

    BE["backend-dev (Sonnet)\ndomain-context · sql-conventions · code-review"]
    FE["frontend-dev (Sonnet)\nfrontend-component · ui-component-mapping\ndesign-system-tokens"]

    BE -->|PR| QA
    BE -->|PR| SEC
    FE -->|PR| QA
    FE -->|PR| SEC

    QA["qa-engineer (Sonnet)\ntest-plan · playwright-e2e · api-testing"]
    SEC["security-analyst (Opus)\nsql-injection-review · owasp-audit · secrets-scan"]

    QA -->|pass| DEV
    SEC -->|clear| DEV

    DEV["devops (Sonnet)\ncicd-pipeline · docker-deploy · deploy-checklist"]
    DEV -->|deployed| TW

    TW["tech-writer (Sonnet)\nuser-manual · api-docs · release-notes"]
    TW --> OUT([Done])

    style PM fill:#EEEDFE,stroke:#534AB7,color:#26215C
    style ARCH fill:#E6F1FB,stroke:#185FA5,color:#042C53
    style DES fill:#FBEAF0,stroke:#993556,color:#4B1528
    style BE fill:#E1F5EE,stroke:#0F6E56,color:#04342C
    style FE fill:#FAECE7,stroke:#993C1D,color:#4A1B0C
    style QA fill:#FAEEDA,stroke:#854F0B,color:#412402
    style SEC fill:#EAF3DE,stroke:#3B6D11,color:#173404
    style DEV fill:#F1EFE8,stroke:#5F5E5A,color:#2C2C2A
    style TW fill:#F1EFE8,stroke:#5F5E5A,color:#2C2C2A
```

> Skills ที่ไม่มีในโฟลเดอร์นี้ (เช่น `system-design-adr`, `owasp-audit`) import จาก ClawHub

---

## Skills ในชุดนี้ (10 ตัว)

| Skill | หน้าที่ | Agent ที่ใช้ |
|---|---|---|
| `prd-writing` | template เขียน PRD | pm-orchestrator |
| `task-breakdown` | แตก task + routing | pm-orchestrator |
| `domain-context` | บริบท domain ของ project ⚠️ | solution-architect, backend-dev, pm-orchestrator |
| `dbschema-erd` | ออกแบบ schema + ERD (รองรับทุก DB engine) | solution-architect |
| `sql-conventions` | convention เขียน SQL (detect engine เอง) | backend-dev |
| `frontend-component` | convention เขียน UI (detect stack เอง) | frontend-dev |
| `ui-component-mapping` | map design element → component ⚠️ | ui-designer, frontend-dev |
| `design-system-tokens` | สี, ฟอนต์, spacing ⚠️ | ui-designer, frontend-dev |
| `sql-injection-review` | ตรวจ SQL injection ก่อน merge | security-analyst |
| `user-manual` | style + โครง user manual ⚠️ | tech-writer |

> ⚠️ = มี placeholder ต้องเติมค่าจริงก่อนใช้ (หรือให้ PM bootstrap จาก issue แรก)

---

## วิธี import

**แนะนำ — From local** (เร็วสุด)
1. แตก zip แล้ว copy folder `agent-skills/` ไปไว้ที่ `~/.claude/skills/`
2. Multica → Settings → Skills → From local
3. Daemon scan เจอทั้ง 10 skills ให้เลือก import ได้ทีเดียว

**From GitHub**
Push repo แล้ว import ทีละ skill โดยวาง URL เช่น
`https://github.com/<you>/<repo>/tree/main/agent-skills/domain-context`

**Manual (New)**
เปิด `SKILL.md` แล้ว copy-paste เนื้อหาเข้า Settings → Skills → New

---

## หมายเหตุ

- skills อ้างถึงกันเอง — attach เป็นชุดตามตารางข้างบนจะได้ผลดีสุด
- `domain-context` ถ้ามีชื่อระบบภายใน sensitive แนะนำเก็บเป็น local / private skill
- แก้ skill หลัง task รันอยู่แล้ว — เฉพาะ task ใหม่ถึงจะได้เวอร์ชันใหม่
