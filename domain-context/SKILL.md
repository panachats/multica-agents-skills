---
name: domain-context
description: Team-specific domain context — which systems are the source of truth, what business segments or categories exist, key objects agents are likely to encounter, and naming conventions. Use this skill before writing queries, designing schemas, or routing data so every agent uses the same vocabulary. Fill the sections below once per project; leave blank rows for domains that do not apply.
---

# Domain context

> This skill is filled in once per project. Keep it as a **local** or **private** workspace skill if it contains internal system names.

## Systems

| Role | Name | Notes |
|---|---|---|
| Primary database | `[YOUR_DATABASE]` | main app database |
| Upstream / source of truth | `[YOUR_UPSTREAM_SYSTEM]` | e.g. ERP, legacy system |
| [Other integration] | `[NAME]` | |

Treat upstream systems as **read-only** from this workspace. Data flows upstream → local only.

## Business segments / channels / categories

The canonical codes used for routing, grouping, and filtering. Agents must use these exact values — do not invent new codes without team confirmation.

| Code | Meaning |
|---|---|
| `[CODE_A]` | [Description] |
| `[CODE_B]` | [Description] |

## Key objects

Tables, views, or procedures agents are likely to encounter or build on.

| Name | Purpose |
|---|---|
| `[TABLE_OR_PROC]` | [What it does and any important behaviour] |

## Naming conventions

- Stored procedures / functions: `[your prefix pattern]`
- Tables: `[convention]`
- Other: `[convention]`

## Notes

[Performance caveats, data-quality issues, policies the team needs to know.]

---

When an agent encounters an object not listed here, it should ask before guessing — and propose updating this skill so the next agent has the context.
