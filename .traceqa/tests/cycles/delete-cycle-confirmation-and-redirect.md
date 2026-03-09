---
id: TC-515
title: Delete cycle — confirmation dialog and redirect after deletion
status: active
priority: high
type: acceptance
automation_status: planned
tags: [cycles, delete, confirmation, TRA-912]
files:
  - web/src/components/cycles/delete-cycle-dialog.tsx
  - web/src/components/cycles/cycle-header.tsx
  - web/src/app/api/workspaces/[id]/cycles/[cycleId]/route.ts
  - web/src/lib/cycles/cycle-db.ts
---

## Preconditions

- User is logged in with workspace access
- Workspace `traceqa-main` exists with at least 2 cycles
- Cycle `alpha-regression` exists in draft status with 3 assigned test cases

## Steps

| #   | Action                                           | Expected Result                                                                                                                         |
| --- | ------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Navigate to cycle `alpha-regression` detail page | Cycle overview page loads with header showing cycle name and delete button                                                              |
| 2   | Click the delete button in the cycle header      | Confirmation dialog appears with title "Delete alpha-regression?"                                                                       |
| 3   | Read the dialog description                      | Text warns: "This will permanently delete the cycle definition, all execution results, and related data. This action cannot be undone." |
| 4   | Click "Cancel"                                   | Dialog closes, cycle page remains unchanged                                                                                             |
| 5   | Click the delete button again                    | Confirmation dialog appears again                                                                                                       |
| 6   | Click "Delete Cycle"                             | Loading spinner appears on the button, button is disabled                                                                               |
| 7   | Wait for deletion to complete                    | Dialog closes, user is redirected to the cycles list page                                                                               |
| 8   | Verify the cycles list                           | Cycle `alpha-regression` no longer appears in the list                                                                                  |

## Final Expected Result

- Delete requires explicit confirmation via dialog
- Successful deletion removes cycle, all assignments, and execution results
- User is redirected to cycles list after deletion
- Deleted cycle no longer appears in any listing
