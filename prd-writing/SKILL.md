---
name: prd-writing
description: Template and rules for writing product requirement documents (PRDs) in this workspace. Use this skill whenever turning a requirement, feature request, or rough idea into a structured PRD. Consult it before breaking work into tasks so every PRD has the same sections — problem, goals, non-goals, user stories, and acceptance criteria.
---

# PRD writing

Write PRDs in a consistent structure so downstream agents can plan and build from them without guessing.

## Template

ALWAYS use this exact structure, saved to `/docs/prd/<issue-key>.md`:

```markdown
# <Feature name>

## Problem
What pain or need this addresses, and for whom.

## Goals
What success looks like (measurable where possible).

## Non-goals
What is explicitly out of scope, to prevent scope creep.

## User stories
- As a <role>, I want <capability>, so that <benefit>.

## Acceptance criteria
- [ ] Given <context>, when <action>, then <result>.
- [ ] ...

## Open questions
Anything needing a decision before build starts.
```

## Rules

- Write acceptance criteria as testable Given/When/Then statements — QA derives test cases directly from these, so vague criteria block testing.
- If the requirement is ambiguous, fill the "Open questions" section and post a comment instead of assuming.
- Keep it concise; link to design specs and API contracts rather than duplicating them.
- For business meaning (segments, data sources), reference `domain-context`.

After the PRD is approved, hand off using the `task-breakdown` skill.
