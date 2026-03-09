---
id: TC-138
title: Result detail sheet — closes on overlay click or Escape key
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [results, detail-view, slide-over, ux]
files:
  [web/src/components/results/result-detail-sheet.tsx, web/src/components/results/results-list.tsx]
---

## Preconditions

- User is logged in with workspace access
- User is on Results page with at least one result
- Result detail sheet is open

## Steps

| #   | Action                                      | Expected Result                               |
| --- | ------------------------------------------- | --------------------------------------------- |
| 1   | With sheet open, observe dimmed background  | Background overlay visible behind sheet       |
| 2   | Click on the dimmed background/overlay area | Sheet closes                                  |
| 3   | Observe results list                        | Results list is fully visible and interactive |
| 4   | Open sheet by clicking a result             | Sheet opens                                   |
| 5   | Press Escape key                            | Sheet closes                                  |

## Final Expected Result

- Sheet can be dismissed by clicking outside
- Sheet can be dismissed with Escape key
- Filter state on results list is preserved after closing sheet
