---
id: TC-366
title: 'Execution page — empty test case with no steps defined'
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [execution, empty-state, edge-case]
files:
  - 'web/src/components/execution/step-card-list.tsx'
  - 'web/src/app/(dashboard)/workspaces/[slug]/execute/[cycleId]/[testCaseId]/execution-client.tsx'
---

## Preconditions

- User is logged in with workspace access
- A test case exists in an active cycle that has no steps defined (empty steps array)
- User navigates to the full-page execution page for this test case

## Steps

| #   | Action                                  | Expected Result                                         |
| --- | --------------------------------------- | ------------------------------------------------------- |
| 1   | Observe the execution page content area | Message displays: "This test case has no steps defined" |
| 2   | Observe the progress bar                | Progress bar shows 0/0 steps (or is not rendered)       |
| 3   | Press P, F, S, B keyboard shortcuts     | No action occurs — there are no steps to mark           |
| 4   | Press Shift+P to attempt Quick Complete | Quick Complete dialog opens but describes 0 steps       |
| 5   | Observe the Complete Session button     | Button is still functional                              |
| 6   | Click "Complete Session"                | Sync completes, user is navigated to My Tasks           |

## Final Expected Result

- Empty test case shows a meaningful message instead of a blank page
- Keyboard shortcuts do not cause errors when no steps exist
- User can still complete the session and navigate away
- No JavaScript errors in the console for the empty state
