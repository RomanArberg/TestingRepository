---
id: TC-44
title: Reassign dialog — cancel does not persist changes
status: active
priority: medium
type: regression
automation_status: planned
tags: [cycles, reassignment]
files:
  - 'web/src/app/(dashboard)/workspaces/[slug]/cycles/[cycleId]/cycle-assignments-table.tsx'
---

## Preconditions

- User is logged in with workspace member access
- User is viewing a cycle detail page with test case assignments

## Steps

| #   | Action                                      | Expected Result                      |
| --- | ------------------------------------------- | ------------------------------------ |
| 1   | Navigate to a cycle detail page             | Page loads with assignments table    |
| 2   | Note the current assignee for the first row | Record original assignee             |
| 3   | Click the three-dot menu on the first row   | Dropdown opens                       |
| 4   | Click "Re-assign"                           | Reassign dialog opens                |
| 5   | Select a different team member              | New member is selected               |
| 6   | Click "Cancel" button (or close dialog)     | Dialog closes without making changes |
| 7   | Verify the assignment row                   | Original assignee is still displayed |
| 8   | Refresh the page                            | Page reloads                         |
| 9   | Verify the assignment row again             | Assignee unchanged from original     |

## Final Expected Result

- Cancelling the dialog does not persist any changes
- Assignment remains with the original assignee
- No API calls made when cancelling
