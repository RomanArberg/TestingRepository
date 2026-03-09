---
id: TC-32
title: Filter state — clear all resets and persists defaults
status: active
priority: medium
type: regression
automation_status: planned
tags: [cycles, filters, persistence]
files:
  - 'web/src/app/(dashboard)/workspaces/[slug]/cycles/[cycleId]/cycle-overview-client.tsx'
---

## Preconditions

- User is logged in with workspace access
- A cycle exists with assignments in at least two different statuses (e.g., failed and blocked)
- User is on the cycle overview page with active filters applied (e.g., "Incomplete" tab selected and "Failed" status filter active)

## Steps

| #   | Action                                              | Expected Result                                                      |
| --- | --------------------------------------------------- | -------------------------------------------------------------------- |
| 1   | Verify filters are active (e.g., "Showing: Failed") | Filtered view is displayed with "Clear all filters" link visible     |
| 2   | Click "Clear all filters"                           | All assignments shown, "All" tab selected, no status/assignee filter |
| 3   | Navigate away from the cycle overview page          | User leaves the cycle overview                                       |
| 4   | Navigate back to the same cycle overview            | Page loads with default state (All tab, no filters)                  |

## Final Expected Result

- "Clear all filters" resets all three filter dimensions (tab, status, assignee)
- The reset state is persisted -- returning to the page shows defaults, not the old filters
