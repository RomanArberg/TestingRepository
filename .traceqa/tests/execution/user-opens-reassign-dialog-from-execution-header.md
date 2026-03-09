---
id: TC-112
title: Reassign dialog — opens from execution header
status: active
priority: high
type: acceptance
automation_status: manual
tags: [execution, reassign, dialog]
files:
  [
    web/src/components/execution/reassign-dialog.tsx,
    web/src/components/execution/execution-header.tsx,
  ]
---

## Preconditions

- User is logged in with workspace access
- User is on the test execution page for a test case within a cycle
- The test case has an assigned user

## Steps

| #   | Action                                                                                | Expected Result                                                       |
| --- | ------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| 1   | Navigate to a test execution page (/workspaces/{slug}/execute/{cycleId}/{testCaseId}) | Execution page loads with header visible                              |
| 2   | Locate the "Re-assign" button in the execution header                                 | Button is visible in the header area                                  |
| 3   | Click the "Re-assign" button                                                          | Dialog opens with title "Re-assign Test Case"                         |
| 4   | Observe the dialog content                                                            | Search input for filtering members is visible                         |
| 5   | Observe the member list area                                                          | Team members list displays (or loading state while fetching)          |
| 6   | Observe the current assignee in the list                                              | Current assignee is pre-selected with checkmark and "(Current)" label |
| 7   | Observe the dialog footer                                                             | "Cancel" and "Re-assign" buttons are visible                          |

## Final Expected Result

- Re-assign dialog opens with proper title and description
- Search input is available for filtering team members
- Current assignee is highlighted and labeled as "(Current)"
- Re-assign button is disabled when current assignee is selected (no-op prevention)
- Cancel button allows closing the dialog without changes
