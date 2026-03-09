---
id: TC-25
title: 'Cycle header — status badges use design token colors'
status: active
priority: high
type: acceptance
automation_status: manual
tags: [cycles, status-badge, visual-redesign]
files:
  - web/src/components/cycles/cycle-header.tsx
  - web/src/components/cycles/execution-status-badge.tsx
---

## Preconditions

- User is logged in with workspace access
- Cycles exist in different statuses: active, draft, completed, archived

## Steps

| #   | Action                          | Expected Result                                                       |
| --- | ------------------------------- | --------------------------------------------------------------------- |
| 1   | Navigate to an active cycle     | Status badge renders with "Active" label and a distinct color         |
| 2   | Navigate to a draft cycle       | Status badge renders with "Draft" label and a distinct color          |
| 3   | Navigate to a completed cycle   | Status badge renders with "Completed" label and a distinct color      |
| 4   | Navigate to an archived cycle   | Status badge renders with "Archived" label and a distinct color       |
| 5   | Verify badge visual distinction | Each status uses a different design token color, not hardcoded values |

## Final Expected Result

- Status badge component is used for all cycle statuses in the header
- Badge text labels match the cycle status name
- Each status has a visually distinct color derived from design tokens
