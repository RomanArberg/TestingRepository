---
id: TC-336
title: Status transition — Completed cycle reopened to Active
status: active
priority: high
type: acceptance
automation_status: planned
tags: [cycles, status-transition, lifecycle, reopen]
files:
  - 'web/src/components/cycles/cycle-header.tsx'
  - 'web/src/app/(dashboard)/workspaces/[slug]/cycles/[cycleId]/cycle-overview-client.tsx'
  - 'web/src/app/api/workspaces/[id]/cycles/[cycleId]/route.ts'
---

## Preconditions

- User is authenticated with workspace access
- A cycle named 'Reopened Smoke Suite' exists in Completed status with prior execution results
- User is viewing the cycle detail page

## Steps

| #   | Action                                       | Expected Result                                                 |
| --- | -------------------------------------------- | --------------------------------------------------------------- |
| 1   | Observe the status badge in the cycle header | Status badge reads 'Completed'                                  |
| 2   | Click the status badge to open the dropdown  | Dropdown opens                                                  |
| 3   | Select 'Active'                              | Loading indicator appears briefly                               |
| 4   | Wait for the update to complete              | Status badge updates to 'Active'                                |
| 5   | Observe the metrics and execution data       | Prior execution results are preserved — counts remain unchanged |
| 6   | Verify the edit button reappears             | Edit button is visible in the header                            |
| 7   | Refresh the page                             | Status remains 'Active', execution data intact                  |

## Final Expected Result

- A completed cycle can be reopened by changing status back to Active
- Prior execution results and metrics are not lost on reopening
- Edit functionality is restored after reopening
