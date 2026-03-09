---
id: TC-572
title: Data tables — full name shown in tooltip on hover when text is truncated
status: active
priority: low
type: acceptance
automation_status: planned
tags: [ui, tables, tooltip, truncation]
files:
  - web/src/components/cycles/cycle-list-item.tsx
  - web/src/components/test-cases/test-case-list-item.tsx
  - web/src/components/results/results-list-item.tsx
---

## Preconditions

- User is logged in with workspace access
- The workspace has cycles and test cases with long names that get truncated in their respective table columns

## Steps

| #   | Action                                                                                                 | Expected Result                                                                                                                                 |
| --- | ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Navigate to the Cycles list page                                                                       | Cycles table renders                                                                                                                            |
| 2   | Identify a cycle with a long name that is visually truncated (ellipsis visible in the Name column)     | Name text is clipped with ellipsis                                                                                                              |
| 3   | Hover the cursor over the truncated cycle name                                                         | Browser native tooltip appears showing the full, untruncated cycle name                                                                         |
| 4   | Navigate to the Test Cases list page; locate a test case with a truncated title                        | Hovering the title cell shows the full test case title in a native tooltip                                                                      |
| 5   | Navigate to a cycle detail page (assignments table); identify a truncated test case title in the table | Hovering the truncated test case title shows the full title                                                                                     |
| 6   | Navigate to the Results page; identify a truncated test case name or cycle name column                 | Hovering shows full text for both test case name and cycle name columns                                                                         |
| 7   | Resize the browser window so that previously truncated names now fit fully without ellipsis            | The `title` attribute is still present on the element; the browser's native tooltip displays the full text (which now matches the visible text) |

## Final Expected Result

- All data table columns that truncate text with `overflow: hidden; text-overflow: ellipsis` also have a `title` attribute on the cell element containing the full text
- Hovering a truncated cell shows the full name via the browser's native tooltip
- This applies to: cycle name, test case title, suite path, and result test case columns across all data tables
