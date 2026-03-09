---
id: TC-418
title: Loading skeleton — test case list shows table skeleton during fetch
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [loading-state, skeleton, test-cases, cross-cutting]
files:
  [web/src/components/test-cases/test-case-list-skeleton.tsx, web/src/components/ui/skeleton.tsx]
---

## Preconditions

- User is logged in as org member with workspace access
- Workspace has test cases synced from GitHub
- Network is throttled to simulate slow loading (e.g., Slow 3G in DevTools)

## Steps

| #   | Action                                               | Expected Result                                                                  |
| --- | ---------------------------------------------------- | -------------------------------------------------------------------------------- |
| 1   | Navigate to the Test Cases list page                 | A loading skeleton appears with table structure                                  |
| 2   | Observe the skeleton layout                          | Skeleton shows column headers: Status, ID, Test Case, Priority, Automation, Tags |
| 3   | Observe the skeleton rows                            | At least 5 animated placeholder rows are visible                                 |
| 4   | Verify the skeleton has accessible loading indicator | Element has role='status' and aria-label='Loading test cases'                    |
| 5   | Wait for data to load                                | Skeleton is replaced by actual test case data in the table                       |

## Final Expected Result

- Loading skeleton matches the layout of the loaded table (same columns, similar widths)
- Skeleton shows animated pulse effect to indicate loading
- Skeleton transitions smoothly to loaded content
- Accessible status is communicated to screen readers
