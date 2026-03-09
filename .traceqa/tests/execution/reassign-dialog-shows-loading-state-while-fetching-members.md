---
id: TC-117
title: Reassign dialog — loading state while fetching members
status: active
priority: medium
type: acceptance
automation_status: manual
tags: [execution, reassign, loading]
files: [web/src/components/execution/reassign-dialog.tsx]
---

## Preconditions

- User is logged in with workspace access
- User is on a test execution page

## Steps

| #   | Action                                               | Expected Result                                                 |
| --- | ---------------------------------------------------- | --------------------------------------------------------------- |
| 1   | Click the "Re-assign" button in the execution header | Dialog opens immediately                                        |
| 2   | Observe the dialog while members are being fetched   | Member list area shows a spinner with "Loading members..." text |
| 3   | Observe the search input                             | Search input is visible and functional during loading           |
| 4   | Observe the Cancel button                            | Cancel button is functional during loading                      |
| 5   | Observe the Re-assign button                         | Re-assign button is disabled during loading                     |
| 6   | Wait for members to load                             | Spinner disappears, member list populates                       |

## Final Expected Result

- Dialog opens immediately without waiting for members to load
- Loading state shows spinner and "Loading members..." text
- Search input is visible during loading but list is not populated yet
- Cancel button is functional during loading
- Re-assign button is disabled during loading
