---
id: TC-34
title: Filter state — scoped independently per workspace and cycle
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [cycles, filters, persistence]
files:
  - 'web/src/app/(dashboard)/workspaces/[slug]/cycles/[cycleId]/cycle-overview-client.tsx'
---

## Preconditions

- User is logged in with access to at least two different cycles (Cycle A and Cycle B)
- Both cycles have multiple assignments with varying statuses

## Steps

| #   | Action                                     | Expected Result                                       |
| --- | ------------------------------------------ | ----------------------------------------------------- |
| 1   | Navigate to Cycle A overview page          | Page loads with default filters (All tab, no filters) |
| 2   | Click "Incomplete" tab on Cycle A          | Table filters to incomplete assignments               |
| 3   | Navigate to Cycle B overview page          | Cycle B shows default filters (All tab, no filters)   |
| 4   | Click the "Failed" status badge on Cycle B | Cycle B table filters to failed assignments           |
| 5   | Navigate back to Cycle A overview page     | Cycle A still shows "Incomplete" tab (not "Failed")   |
| 6   | Navigate back to Cycle B overview page     | Cycle B still shows "Failed" status filter            |

## Final Expected Result

- Each cycle maintains its own independent filter state
- Changing filters on one cycle does not affect another
- Filter state is correctly keyed by workspace and cycle combination
