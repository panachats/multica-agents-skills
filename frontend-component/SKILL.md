---
name: frontend-component
description: Front-end component conventions for this workspace. Use this skill for any UI task — building components, forms, or data-fetching. Start by reading the project's package.json and a few existing components to identify the actual stack (framework, component library, form lib, data-fetching lib); then apply the principles here using those tools. Works for any stack — React, Vue, Svelte, or other.
---

# Front-end component conventions

## Step 0 — discover the project stack

Before writing a component, understand what the project already uses:

```shell
cat package.json       # find: framework, UI library, form lib, data-fetching lib
ls src/components      # look at 1-2 existing components for established patterns
```

Key things to identify: framework (React / Vue / Svelte / …), component library (Ant Design / MUI / shadcn / …), form handling (React Hook Form / Formik / VeeValidate / …), server state (React Query / TanStack / SWR / …). If the project has no established library for something, ask in the issue before introducing one.

## Component principles

- Keep components small and single-purpose. Prefer composition over monolithic components.
- Follow the pattern of existing components — consistency beats personal preference.
- Co-locate types and interfaces with the component they belong to.
- Map every UI element to the component library already in use (see `ui-component-mapping`).
- Honour the design system tokens (see `design-system-tokens`).

## Forms

- Use the form library already in the project.
- Validate through a schema (Zod, Yup, Valibot, or equivalent) rather than ad-hoc if-checks.
- Surface field errors inline, adjacent to the field.
- Never submit without passing through the form's submit handler.

## Server / async state

- Use the data-fetching library already in the project.
- Stable, descriptive cache/query keys — prefer array form when the library supports it, e.g. `['orders', { status, page }]`.
- Invalidate relevant cache after mutations so the UI reflects server state.
- Keep server state in the data-fetching library; use local state only for UI-only concerns (open/closed, selected row, etc.).

## Handle all four UI states

Every data-driven region must handle all of these — do not assume data exists:

| State | What to show |
|---|---|
| Loading | spinner or skeleton while fetching |
| Error | clear message, retry option if feasible |
| Empty | meaningful message, not a blank screen |
| Data | the happy path |

## Accessibility

Labels tied to inputs. Keyboard-operable controls. Sensible focus order. UI copy in sentence case.

## Domain

For business data meaning (segments, data sources), see `domain-context`.
