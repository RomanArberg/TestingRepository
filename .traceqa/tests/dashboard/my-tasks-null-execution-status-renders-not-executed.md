---
id: TC-542
title: My Tasks — null executionStatus renders 'Not Executed' badge
status: active
priority: high
type: regression
automation_status: manual
tags: [my-tasks, execution-status, error-handling]
files:
  - web/src/components/my-tasks/my-tasks-list-item.tsx
  - web/src/app/api/workspaces/[id]/my-tasks/route.ts
---

## Preconditions

- A user is logged in and has at least one task assigned to them in an active cycle
- The task has no execution results yet (never run), or the GitHub results fetch will be made to fail
- The My Tasks page is accessible at `/workspaces/<slug>/my-tasks`

## Steps

| #   | Action                                                                                                                                                                | Expected Result                                                                             |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1   | Simulate a GitHub API failure by temporarily revoking the GitHub App installation token or blocking the results API call (e.g. via environment flag or network proxy) | The My Tasks API will return tasks with `executionStatus: null`                             |
| 2   | Navigate to the My Tasks page for the workspace                                                                                                                       | The page loads without crashing                                                             |
| 3   | Observe the status column for the task with `executionStatus: null`                                                                                                   | A "Not Executed" badge is displayed in the status column                                    |
| 4   | Confirm the badge is visible and has the correct label                                                                                                                | The badge reads exactly "Not Executed" (not blank, not undefined, not an error)             |
| 5   | Confirm the rest of the row renders correctly                                                                                                                         | The test case title, cycle name, priority badge, and actions menu all display normally      |
| 6   | Restore normal GitHub API access                                                                                                                                      | N/A                                                                                         |
| 7   | Refresh the My Tasks page                                                                                                                                             | The task now shows its actual execution status (e.g. "Not Executed" or another real status) |

## Final Expected Result

- A `null` `executionStatus` value never causes the page to crash or render a blank status cell
- The "Not Executed" badge is shown as a safe fallback for `null` status
- The `ExecutionStatusBadge` component handles `null`/`undefined` status gracefully
