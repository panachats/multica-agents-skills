---
name: ui-component-mapping
description: Mapping from design-spec UI element names to the actual component library components used in this workspace, so handoffs are unambiguous. Use this skill when writing a design handoff or implementing a spec. Start by reading package.json and existing components to identify the UI library; fill the Component used column from what the project already uses.
---

# UI component mapping

A shared vocabulary so designer and developer mean the same component when they say "dropdown" or "data table."

## Step 0 — discover the UI library

Before picking components, identify what this project already uses:

```shell
cat package.json                    # framework + UI library
ls src/components                   # 1–2 existing screens for patterns
```

Match the **Component used** column to imports already in the codebase (e.g. from `antd`, `@mui/material`, `@/components/ui`, Vant, etc.). If the column is empty, infer from existing files and update this skill before the first handoff. Do not introduce a new UI library without team confirmation.

## Component mapping

| Design element | Component used | Notes |
|---|---|---|
| Single-line text field | | wrap in the project's form field wrapper for validation |
| Multi-line text area | | |
| Number field | | quantities, prices |
| Dropdown / select | | static or async options |
| Date picker | | agree date output format with backend |
| Date range picker | | half-open range downstream if applicable |
| Data table | | server-side pagination when data is large |
| Primary action button | | one primary per view |
| Secondary / ghost button | | |
| Modal / dialog | | confirm destructive actions |
| Inline field error | | adjacent to the field |
| Page-level feedback | | toast / notification after mutation |
| Loading state | | spinner or skeleton in every async region |
| Empty state | | when a query returns nothing |
| Status label / badge | | colour by status |
| Tabs | | |
| Page layout / content area | | filter area + main content |
| Form (group) | | project's standard form wrapper |

## Rules

- Always use this table when picking components — do not choose on the fly.
- If a needed element is missing, add it here before introducing something new to the codebase.
- For spacing, colour, and typography, see `design-system-tokens`.
- For form wiring and data-fetching patterns, see `frontend-component`.
- UI labels for business codes come from `domain-context`; APIs still send canonical codes from that skill.
