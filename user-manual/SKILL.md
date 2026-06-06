---
name: user-manual
description: Style and structure for end-user manuals and user-facing documentation in this workspace. Use this skill whenever documenting a user-facing feature or writing how-to guides for end users (not API docs). Consult it so manuals follow one structure, use plain language, and match the team's tone.
---

# User manual style

Write for the reader who has to get a task done, not for the engineer who built it. Keep it task-oriented and free of jargon.

## Structure

Save manual sections under `/docs/manual/<area>/<feature>.md` using:

```markdown
# <Feature name>

## What it does
One or two sentences in plain language.

## Before you start
Prerequisites, permissions, or data needed.

## Steps
1. Numbered, action-first steps. One action per step.
2. ...

## Tips
Shortcuts, gotchas, common mistakes.

## Troubleshooting
| Problem | Likely cause | Fix |
|---|---|---|
```

## Style rules

- Plain language; if a business-specific code or segment name appears, gloss it on first use (see `domain-context`).
- Address the reader as "you". Imperative steps ("Click Save", not "The user should click Save").
- One action per numbered step; show the result of the step.
- Add a screenshot where it removes ambiguity; describe what to look for.
- Sentence case for headings and UI labels.

## TODO — team specifics

> Fill these in: preferred language (Thai / English / bilingual?), product/app name to use in titles, screenshot conventions (tool, annotation style), and where published manuals live (wiki/Confluence/Notion). Once set, note them here so every manual matches.

For release notes and API documentation, use the `release-notes` and `api-docs` skills instead.
