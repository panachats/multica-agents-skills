---
name: domain-context
description: Team-specific domain context — which systems are the source of truth, what business segments or categories exist, key objects agents are likely to encounter, and naming conventions. Use this skill before writing queries, designing schemas, or routing data so every agent uses the same vocabulary. Fill the sections below once per project; leave blank rows for domains that do not apply.
---

# Domain context

Business vocabulary for this workspace — not a tech stack choice. Keep as a **local** or **private** skill if it contains internal system names.

## Step 0 — discover before filling

Before writing or updating this skill, gather facts from the project:

```shell
ls migrations/ db/ schema/ prisma/          # existing tables and naming
cat README.md docs/                         # system names, integrations
cat .env.example docker-compose.yml         # database and upstream service names
```

Also extract from the first PRD/issue: segment codes, status values, and object names the feature touches. **Do not invent codes or table names** — copy what the repo or product owner already uses. If something is missing, ask in the issue and update this skill once confirmed.

## Systems

| Role | Name | Notes |
|---|---|---|
| Primary database | | main app database |
| Upstream / source of truth | | if any — ERP, legacy, SaaS |
| Other integration | | cache, queue, file store, etc. |

Treat upstream systems as **read-only** from this workspace unless the PRD explicitly allows write-back.

## Business segments / channels / categories

Canonical codes for routing, grouping, and filtering. Agents must use these exact values — do not invent new codes without team confirmation.

| Code | Meaning | UI label (optional) |
|---|---|---|
| | | |

Add separate tables for other code lists (status, type, region) when the project uses them.

## Key objects

Tables, views, models, or procedures agents are likely to encounter or build on.

| Name | Purpose |
|---|---|
| | |

## Naming conventions

Discover from existing schema and code, then record here:

- Tables / columns:
- Primary keys:
- Foreign keys:
- API JSON property casing:
- Date/time filter rules (e.g. half-open range on indexed columns):

## Notes

Policies, sync lag, data-quality caveats, and performance rules the team must follow.

---

When an agent encounters an object not listed here, it should ask before guessing — and propose updating this skill so the next agent has the context.
