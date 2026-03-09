---
id: TC-57
title: Workspace grid — cards with health indicators and progress bars
status: active
priority: high
type: acceptance
automation_status: planned
tags: [dashboard, workspace-grid, health-status, progress]
files:
  [
    web/src/components/dashboard/workspace-grid.tsx,
    web/src/components/command-center/workspace-card.tsx,
    web/src/types/dashboard.ts,
  ]
---

## Preconditions

- User is logged in with access to multiple workspaces
- Workspaces have varying health statuses (healthy, failing, empty)
- User is on dashboard page

## Steps

| #   | Action                           | Expected Result                                                                                          |
| --- | -------------------------------- | -------------------------------------------------------------------------------------------------------- |
| 1   | Navigate to /dashboard           | Dashboard page loads showing HeroSection, stats grid, and WorkspaceGrid                                  |
| 2   | Observe the overall page layout  | HeroSection at top, 3-column stats grid (LatestAutomation, ActiveCycle, WeeklyStats), then WorkspaceGrid |
| 3   | Scroll to workspace grid section | Grid of workspace cards is visible                                                                       |
| 4   | Observe workspace card layout    | Cards display in a responsive grid                                                                       |
| 5   | Check a healthy workspace card   | Green left border, pass rate badge shown                                                                 |
| 6   | Check a failing workspace card   | Red left border, "Failing" badge with pulsing dot, failing count shown                                   |
| 7   | Check an empty workspace card    | Gray left border, "Empty" badge                                                                          |
| 8   | Verify progress bar on a card    | Multi-color segments for passed/failed/blocked/skipped                                                   |
| 9   | Click on a workspace card        | Navigates to the workspace detail page                                                                   |

## Final Expected Result

- Dashboard uses HeroSection + WorkspaceGrid + StatsPanel layout
- All workspaces are displayed in the grid
- Health status is clearly indicated by left border color and badges
- Progress bars accurately show test result distribution
- Workspace cards are clickable and navigate to workspace detail
