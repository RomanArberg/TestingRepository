---
id: TC-23
title: 'Cycle detail — test case titles displayed instead of IDs'
status: active
priority: high
type: acceptance
automation_status: planned
tags: [cycles, cycle-detail, titles]
files:
  - web/src/app/(dashboard)/workspaces/[slug]/cycles/[cycleId]/page.tsx
  - web/src/app/(dashboard)/workspaces/[slug]/cycles/[cycleId]/cycle-assignments-section.tsx
---

## Preconditions

- User is logged in with workspace access
- A cycle exists with assigned test cases
- Test cases have been synced so that title metadata is available

## Steps

| #   | Action                                          | Expected Result                                                   |
| --- | ----------------------------------------------- | ----------------------------------------------------------------- |
| 1   | Navigate to the cycle detail page               | Page loads showing all assigned test cases                        |
| 2   | Observe the test case rows                      | Each row displays the test case title (not just the test case ID) |
| 3   | Verify titles match the actual test case titles | Titles correspond to the synced test case metadata                |
| 4   | Check a test case with a long title             | Title is displayed without truncation or overflow issues          |

## Final Expected Result

- All test case assignments show their human-readable titles
- If a title is unavailable (metadata not yet synced), the row degrades gracefully by showing the test case ID instead
