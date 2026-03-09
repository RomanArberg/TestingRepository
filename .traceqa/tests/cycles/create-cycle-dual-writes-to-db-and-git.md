---
id: TC-223
title: Create cycle — dual-writes to database and Git
status: active
priority: medium
type: acceptance
tags: [cycles, dual-write, db-migration]
automation_status: planned
files:
  - 'web/src/components/cycles/create-cycle-dialog.tsx'
  - 'web/src/app/api/workspaces/[id]/cycles/route.ts'
  - 'web/src/lib/cycles/cycle-db.ts'
---

## Preconditions

- User is logged in with workspace access and permission to create cycles

## Steps

| #   | Action                                               | Expected Result                                                   |
| --- | ---------------------------------------------------- | ----------------------------------------------------------------- |
| 1   | Navigate to the Cycles list page                     | Page loads with existing cycles                                   |
| 2   | Click the "Create Cycle" button                      | Cycle creation form appears                                       |
| 3   | Fill in cycle name, description, and select a status | Form fields accept input without errors                           |
| 4   | Add at least 2 test case assignments                 | Test cases appear in the assignment list                          |
| 5   | Submit the cycle creation form                       | Success feedback shown; redirected to the new cycle detail page   |
| 6   | Verify the new cycle appears in the Cycles list      | Cycle list includes the newly created cycle with correct metadata |
| 7   | Refresh the page                                     | New cycle persists after refresh                                  |
| 8   | Verify Git YAML file in `.traceqa/cycles/` directory | YAML file exists with matching cycle ID and metadata              |

## Final Expected Result

- New cycle is created and immediately visible in the UI
- Cycle data persists across page loads (stored in Supabase)
- Git YAML file is also created (dual-write)
- If Git write fails, the cycle still exists in the DB (Git failure is non-blocking)
