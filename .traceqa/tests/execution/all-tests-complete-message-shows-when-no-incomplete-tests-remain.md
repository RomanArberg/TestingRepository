---
id: TC-94
title: Execution footer — all tests complete message when no incomplete tests remain
status: active
priority: medium
type: acceptance
automation_status: manual
tags: [execution, cycles, navigation, completion]
files:
  - 'web/src/components/execution/execution-footer.tsx'
  - 'web/src/app/(dashboard)/workspaces/[slug]/execute/[cycleId]/[testCaseId]/execution-client.tsx'
---

## Preconditions

- User is logged in with workspace access
- A cycle exists with 3 test cases
- 2 test cases are already "Passed"
- 1 test case is "Not Executed"
- "Skip completed" toggle is enabled

## Steps

| #   | Action                                                  | Expected Result                            |
| --- | ------------------------------------------------------- | ------------------------------------------ |
| 1   | Navigate to execution mode for the incomplete test case | Execution page loads                       |
| 2   | Complete the test case by marking all steps as "Pass"   | Test status becomes "Passed"               |
| 3   | Observe the footer navigation                           | "All tests complete!" message is displayed |
| 4   | Verify Previous/Next buttons                            | Both buttons are disabled or hidden        |
| 5   | Click "Back to Cycle"                                   | Returns to cycle page                      |
| 6   | Verify cycle page shows all passed                      | All test cases show green checkmark        |

## Final Expected Result

- Clear indication when all tests in cycle are complete
- Navigation buttons appropriately disabled when no more tests
- User can return to cycle page to see completion status
- Completion message only shows when skip completed is enabled
