---
name: design-system-tokens
description: The design tokens (color, typography, spacing, radius) for this workspace's UI, so every design and component uses the same values. Use this skill whenever specifying or building UI — choosing a color, spacing, or text style. Consult it instead of inventing ad-hoc values so the product stays visually consistent.
---

# Design system tokens

The single source of truth for visual values. Designer and frontend agents pull from here; never hard-code one-off values.

> **TODO — fill in your team's real values.** The values below are placeholders. Replace them with the actual tokens from your design source (Figma variables, AntD theme config, or your CSS variables). Once filled, this becomes authoritative.

## Color

| Token | Value | Use |
|---|---|---|
| `color-primary` | `#____` | primary actions, brand |
| `color-success` | `#____` | success states |
| `color-warning` | `#____` | warnings |
| `color-error` | `#____` | errors, destructive |
| `color-text` | `#____` | body text |
| `color-text-secondary` | `#____` | secondary text |
| `color-border` | `#____` | borders, dividers |
| `color-bg` | `#____` | page background |
| `color-bg-surface` | `#____` | cards, panels |

## Typography

| Token | Value |
|---|---|
| `font-family` | `____` (include a Thai-capable fallback) |
| `font-size-base` | `__px` |
| `font-size-heading-1..3` | `__ / __ / __ px` |
| `font-weight-regular / medium` | `400 / 500` |
| `line-height-base` | `__` |

## Spacing & radius

| Token | Value |
|---|---|
| `space-xs / sm / md / lg / xl` | `_ / _ / _ / _ / _ px` |
| `radius-sm / md / lg` | `_ / _ / _ px` |

## Rules

- Map these tokens to the AntD theme (`ConfigProvider` `theme.token`) so AntD components inherit them automatically.
- Sentence case for all UI text.
- When a needed token is missing, propose adding it here rather than inventing a local value.
- For which component renders a given element, see `antd-component-mapping`.
