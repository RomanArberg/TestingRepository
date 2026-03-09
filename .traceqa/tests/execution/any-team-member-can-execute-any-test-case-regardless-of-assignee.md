---
id: TC-96
title: Execution permissions — any team member can execute regardless of assignee
status: active
priority: high
type: acceptance
automation_status: manual
tags: [execution, cycles, permissions]
files:
  - 'web/src/app/(dashboard)/workspaces/[slug]/execute/[cycleId]/[testCaseId]/page.tsx'
  - 'web/src/app/(dashboard)/workspaces/[slug]/execute/[cycleId]/[testCaseId]/execution-client.tsx'
---

## Preconditions

- User A is logged in with workspace access
- A cycle exists with test cases
- Test case TC-001 is assigned to User B (different user)
- User A is not the assignee

## Steps

| #   | Action                                     | Expected Result                                              |
| --- | ------------------------------------------ | ------------------------------------------------------------ |
| 1   | Navigate to the Cycle page as User A       | Cycle page loads                                             |
| 2   | Find test case TC-001 (assigned to User B) | Test case row shows User B as assignee                       |
| 3   | Click on the test case row                 | Quick Execution Sheet opens for TC-001                       |
| 4   | Execute steps and mark as "Pass"           | Steps can be completed normally                              |
| 5   | Save the execution result                  | Result is saved successfully                                 |
| 6   | Verify the execution result                | Executor is recorded as User A, assignee unchanged as User B |
| 7   | Alternatively, use quick triage on TC-001  | Status can be changed via dropdown                           |

## Final Expected Result

- Any workspace member can execute any test case in the cycle
- Execution is not restricted to original assignee
- Actual executor is correctly recorded (User A, not User B)
- Original assignee remains unchanged in the assignment
