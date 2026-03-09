---
id: TC-50
title: Stats panels — LatestAutomation, ActiveCycle, and WeeklyStats display
status: active
priority: high
type: acceptance
automation_status: planned
tags: [dashboard, stats-panel, latest-automation, active-cycle, weekly-stats]
files:
  [
    web/src/components/dashboard/stats-panel.tsx,
    web/src/components/command-center/panel.tsx,
    web/src/components/command-center/metric-grid.tsx,
  ]
---

## Preconditions

- User is logged in with access to workspaces
- User is on the dashboard page

## Steps

| #   | Action                                        | Expected Result                                                                   |
| --- | --------------------------------------------- | --------------------------------------------------------------------------------- |
| 1   | Navigate to /dashboard                        | Dashboard page loads                                                              |
| 2   | Observe the stats grid below the hero section | Three panel cards are visible in a 3-column grid                                  |
| 3   | Check "Latest Automation" panel               | Shows most recent CI/automation run status with passed/failed badge               |
| 4   | Check "Active Cycle" panel                    | Shows currently active test cycle with completion progress                        |
| 5   | Check "Weekly Stats" panel                    | Shows weekly testing metrics with trend indicators                                |
| 6   | Verify panel styling                          | Each panel uses the Panel component with uppercase title and design token borders |

## Final Expected Result

- All three stats panels are visible and display accurate data
- LatestAutomationPanel shows automation run status and a "View Traces" link
- ActiveCyclePanel shows the current cycle's completion progress
- WeeklyStatsPanel shows weekly metrics with trend direction indicators
- Panels use consistent Command Center styling with design tokens
