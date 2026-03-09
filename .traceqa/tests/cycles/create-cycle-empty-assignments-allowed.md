---
id: TC-354
title: 'Create cycle — allows creation with zero test case assignments'
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [cycles, boundary, create]
files:
  - 'web/src/components/cycles/create-cycle-dialog.tsx'
  - 'web/src/app/api/workspaces/[id]/cycles/route.ts'
---

## Preconditions

- User is authenticated with workspace access
- Create cycle dialog is open

## Steps

| #   | Action                                               | Expected Result                                 |
| --- | ---------------------------------------------------- | ----------------------------------------------- |
| 1   | Enter name "Empty Planning Cycle"                    | Name is accepted                                |
| 2   | Do not select any test cases from the selection list | Test case selection remains empty               |
| 3   | Click 'Create'                                       | Cycle is created successfully                   |
| 4   | Navigate to the new cycle's detail page              | Empty state card shows "No test cases assigned" |

## Final Expected Result

- A cycle with zero assignments is valid and can be created
- The cycle detail page shows an appropriate empty state message
- Assignments can be added later via the edit page
