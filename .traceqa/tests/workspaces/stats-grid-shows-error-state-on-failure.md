---
id: TC-205
title: Stats grid — error indicator when API fails
status: active
priority: medium
type: regression
automation_status: manual
tags: [workspace, overview, stats, error-handling]
files:
  - web/src/components/workspaces/workspace-stats-grid.tsx
---

## Preconditions

- User is logged in with workspace access
- Network conditions can be simulated (DevTools > Network > Offline)
- User is on workspace overview page (`/workspaces/{slug}`)

## Steps

| #   | Action                               | Expected Result                                   |
| --- | ------------------------------------ | ------------------------------------------------- |
| 1   | Open browser DevTools (F12)          | DevTools panel opens                              |
| 2   | Go to Network tab                    | Network panel visible                             |
| 3   | Enable "Offline" mode                | Network requests will fail                        |
| 4   | Hard refresh the page (Ctrl+Shift+R) | Page attempts to reload                           |
| 5   | Observe "Test Cases" stat            | May show value (cached) or error                  |
| 6   | Observe "Active Cycles" stat         | Shows "!" error indicator (red/destructive color) |
| 7   | Observe "My Tasks" stat              | Shows "!" error indicator (red/destructive color) |
| 8   | Disable "Offline" mode in DevTools   | Network restored                                  |
| 9   | Hard refresh the page again          | Page reloads normally                             |
| 10  | Observe all stats                    | All stats show correct values                     |

## Final Expected Result

- Stats dependent on client-side API calls show error indicator when network fails
- Error indicator is visually distinct (red "!" symbol)
- Screen readers can identify error state (aria-label present)
- Errors are recoverable — refreshing when network is restored shows correct data
- Test Cases stat (server-rendered) may still show if page HTML cached
