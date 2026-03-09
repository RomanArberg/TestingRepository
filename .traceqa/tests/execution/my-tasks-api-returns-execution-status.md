---
id: TC-526
title: My Tasks API — returns executionStatus field from Git results
status: active
priority: high
type: acceptance
automation_status: planned
tags: [execution, my-tasks, api, tabular-layout]
files:
  - web/src/app/api/workspaces/[id]/my-tasks/route.ts
  - web/src/lib/my-tasks/types.ts
---

## Preconditions

- User is logged in with workspace access
- An active cycle exists with 3 test cases assigned to the user:
  - TC-A: executed with status "passed" (result exists in Git)
  - TC-B: executed with status "failed" (result exists in Git)
  - TC-C: not executed (no result in Git)

## Steps

| #   | Action                                        | Expected Result                                                               |
| --- | --------------------------------------------- | ----------------------------------------------------------------------------- |
| 1   | Navigate to My Tasks page (API fetches tasks) | API returns tasks with executionStatus field populated                        |
| 2   | Observe TC-A in the task list                 | executionStatus is "passed"                                                   |
| 3   | Observe TC-B in the task list                 | executionStatus is "failed"                                                   |
| 4   | Observe TC-C in the task list                 | executionStatus is null (not executed)                                        |
| 5   | Disconnect GitHub or make results unreadable  | API returns tasks with executionStatus as null for all (graceful degradation) |

## Final Expected Result

- API always includes executionStatus field in the response (non-breaking addition)
- Execution results are fetched from Git on every request (not only when hideCompleted is true)
- When Git results fetch fails, executionStatus falls back to null (API doesn't error)
- Results are matched by composite key: cycle + assignee + testCaseId
