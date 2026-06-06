---
name: task-breakdown
description: Rules for breaking a PRD into Epics, Stories, and assignable tasks, then routing them to the right agent. Use this skill whenever decomposing approved requirements into issues. Consult it so each task is independently shippable, has clear acceptance criteria, and is mentioned to the correct downstream agent.
---

# Task breakdown

Turn an approved PRD into a tree of issues that downstream agents can pick up independently.

## Hierarchy

- **Epic** — a large outcome spanning multiple deliverables.
- **Story** — a single user-facing capability.
- **Task** — one concrete, independently shippable unit of work (one PR's worth).

Break down until each task is small enough to complete and review on its own.

## Each task must have

- A clear, action-oriented title.
- A short description with context and links (PRD, design spec, API contract).
- Acceptance criteria carried down from the PRD (Given/When/Then).
- A clear owner — route by `@`-mention:

| Work type | Route to |
|---|---|
| UI/UX spec | `@ui-designer` |
| Architecture, schema, API contract | `@solution-architect` |
| Server logic, data, SP | `@backend-dev` |
| React UI | `@frontend-dev` |
| Testing | `@qa-engineer` |
| Deploy, infra | `@devops` |
| Security review (always, pre-merge) | `@security-analyst` |
| Documentation | `@tech-writer` |

## Ordering

Respect dependencies: architecture/contract before implementation; backend endpoints before frontend integration; QA after a PR is ready; security review before merge; docs after merge. Note blockers explicitly so parallel work (e.g. designer + architect) can start at once.

## Priority

Rank by business value vs effort. State the priority on each issue so the board reflects what to pick up first.
