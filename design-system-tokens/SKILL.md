---
name: design-system-tokens
description: The design tokens (color, typography, spacing, radius) for this workspace's UI, so every design and component uses the same values. Use this skill whenever specifying or building UI — choosing a color, spacing, or text style. Start by reading the project's existing theme or style sources; then record the values here. Consult it instead of inventing ad-hoc values so the product stays visually consistent.
---

# Design system tokens

The single source of truth for visual values. Designer and frontend agents pull from here; never hard-code one-off values.

## Step 0 — discover the project's tokens

Before specifying or building UI, find where this project already defines styles:

```shell
cat package.json                              # UI library, Tailwind, CSS-in-JS
ls tailwind.config.* src/styles/ theme/       # theme files, CSS variables
grep -r "theme\|tokens\|variables" src/ --include="*.ts" --include="*.css" -l | head
```

Common sources (use whichever exists — do not introduce a new design system):

| Signal in repo | Where tokens usually live |
|---|---|
| Tailwind | `tailwind.config.js` → `theme.extend` |
| Component library theme | e.g. provider `theme` prop, `theme.ts`, SCSS variables |
| CSS variables | `:root { --color-* }` in global CSS |
| Design tool export | `tokens.json`, Figma variables doc linked in README |

Copy discovered values into the tables below. If the project has no theme yet, ask which source of truth to use before picking colors or fonts.

## Color

| Token | Value | Use |
|---|---|---|
| `color-primary` | | primary actions, brand |
| `color-success` | | success states |
| `color-warning` | | warnings |
| `color-error` | | errors, destructive |
| `color-text` | | body text |
| `color-text-secondary` | | secondary text, hints |
| `color-border` | | borders, dividers |
| `color-bg` | | page background |
| `color-bg-surface` | | cards, panels, modals |

## Typography

| Token | Value |
|---|---|
| `font-family` | include a Thai-capable fallback if the product serves Thai users |
| `font-size-base` | |
| `font-size-heading-1` | |
| `font-size-heading-2` | |
| `font-size-heading-3` | |
| `font-weight-regular` | |
| `font-weight-medium` | |
| `line-height-base` | |

## Spacing & radius

| Token | Value |
|---|---|
| `space-xs` | |
| `space-sm` | |
| `space-md` | |
| `space-lg` | |
| `space-xl` | |
| `radius-sm` | |
| `radius-md` | |
| `radius-lg` | |

## Rules

- Wire these tokens through whatever mechanism the project already uses (theme config, CSS variables, design tokens file) — do not add a second parallel system.
- Sentence case for UI text unless the project's existing screens use a different convention.
- When a needed token is missing, propose adding it here rather than inventing a local value.
- For which component renders a given element, see `ui-component-mapping`.
