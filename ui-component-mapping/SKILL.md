---
name: ui-component-mapping
description: Mapping from design-spec UI element names to the actual component library components used in this workspace, so handoffs are unambiguous. Use this skill when writing a design handoff or implementing a spec. If the table is blank or incomplete, read package.json and look at existing components to infer the mapping, fill it in, and propose an update to this skill.
---

# UI component mapping

A shared vocabulary so designer and developer mean the same component when they say "dropdown" or "data table."

> Fill in the **Component used** column for this project. Extend the table as the team standardises new elements. This becomes the single source of truth for every handoff.

## Component mapping

| Design element | Component used | Notes |
|---|---|---|
| Single-line text field | `` | wrap in the form field wrapper for validation |
| Multi-line text area | `` | |
| Number field | `` | for quantities, prices |
| Dropdown / select | `` | options list; async loading state |
| Date picker | `` | agree output format with backend |
| Date range picker | `` | half-open range downstream |
| Data table | `` | server-side pagination when data is large |
| Primary action button | `` | one primary per view |
| Secondary / ghost button | `` | |
| Modal / dialog | `` | confirm destructive actions |
| Inline field error | `` | adjacent to the field |
| Page-level feedback | `` | toast / notification after mutation |
| Loading state | `` | spinner or skeleton in every async region |
| Empty state | `` | when a query returns nothing |
| Status label / badge | `` | colour by status |
| Tabs | `` | |

## Rules

- Always use this table when picking components — do not choose on the fly.
- If a needed element is missing, add it here before introducing something new to the codebase.
- For spacing, colour, and typography, see `design-system-tokens`.
- For form wiring and data-fetching patterns, see `frontend-component`.
