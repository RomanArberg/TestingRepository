---
id: TC-527
title: My Tasks inline status triage — optimistic update with cross-cycle support
status: active
priority: high
type: acceptance
automation_status: planned
tags: [dashboard, my-tasks, triage, execution, optimistic-ui, tabular-layout]
files:
  - web/src/components/my-tasks/my-tasks-list.tsx
  - web/src/components/my-tasks/my-tasks-list-item.tsx
  - web/src/components/cycles/execution-status-badge.tsx
---

## Preconditions

- User is logged in with workspace access
- At least 3 tasks assigned across 2+ different cycles
- Tasks have varying execution statuses (not executed, passed, failed)

## Steps

| #   | Action                                                     | Expected Result                                                                                     |
| --- | ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| 1   | Navigate to the My Tasks page                              | Table renders with tasks from multiple cycles                                                       |
| 2   | Click the status badge of a "Not Executed" task in Cycle A | Dropdown opens with: Passed, Failed, Blocked, Skipped                                               |
| 3   | Select "Passed"                                            | Badge immediately shows "Passed" (optimistic); loading spinner appears briefly next to badge        |
| 4   | Observe the API request in Network tab                     | POST to /api/workspaces/{id}/quick-triage with `cycleId` matching Cycle A's ID                      |
| 5   | Click the status badge of a "Not Executed" task in Cycle B | Dropdown opens (same options)                                                                       |
| 6   | Select "Failed"                                            | Badge shows "Failed" optimistically; API call uses Cycle B's ID (different from step 4)             |
| 7   | Simulate a network error (disconnect or server error)      | Optimistic status reverts to previous value; red error icon (AlertCircle) appears next to the badge |
| 8   | Click the error retry button                               | API call retries; on success, badge updates and error icon disappears                               |
| 9   | Change a "Passed" task to "Blocked"                        | Badge flips from Passed to Blocked optimistically; API confirms                                     |
| 10  | Reload the page                                            | All status changes are persisted (fetched fresh from API/Git)                                       |

## Final Expected Result

- Each task's triage call uses the correct cycle.id (tasks span multiple cycles)
- Optimistic status keyed by "cycleId:testCaseId" composite key (no collisions across cycles)
- Loading spinner (Loader2) shows during API call, disappears on completion
- Error state shows AlertCircle icon with retry button; clicking retries the same status change
- On error, optimistic status reverts to previous value
- Task list refreshes (refetch) after successful triage
