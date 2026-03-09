---
id: TC-361
title: 'Network loss — buffering continues locally during offline period'
status: active
priority: critical
type: regression
automation_status: planned
tags: [execution, session-buffer, network, offline, negative]
files:
  - 'web/src/hooks/use-session-buffer.ts'
  - 'web/src/app/api/workspaces/[id]/session-buffer/route.ts'
  - 'web/src/components/execution/sync-status-indicator.tsx'
---

## Preconditions

- User is logged in with workspace access
- User is on the full-page execution page for a test case with 6 steps
- Steps 1-2 have been marked as Pass and synced (indicator shows "Saved")
- Browser developer tools are available to simulate network conditions

## Steps

| #   | Action                                               | Expected Result                                           |
| --- | ---------------------------------------------------- | --------------------------------------------------------- |
| 1   | Open browser DevTools and set network to "Offline"   | Network requests will fail                                |
| 2   | Mark step 3 as Pass using the P key                  | Step 3 shows green pass locally, focus advances to step 4 |
| 3   | Mark step 4 as Fail using the F key                  | Step 4 shows red fail locally, focus stays on step 4      |
| 4   | Observe the sync status indicator                    | Shows error state (red) — buffer POST failed              |
| 5   | Add comment 'Expected 200 but got 503' to step 4     | Comment appears in the UI (local state)                   |
| 6   | Restore network in DevTools (set to "No throttling") | Network connectivity restored                             |
| 7   | Click the error indicator to retry sync              | Status shows "Saving..." then "Saved"                     |
| 8   | Refresh the page                                     | Steps 1-4 all show their correct statuses and comments    |

## Final Expected Result

- Step status changes are applied locally even when offline
- UI remains interactive and responsive during network outage
- Sync error is clearly communicated via the status indicator
- Manual retry after network restoration recovers all buffered changes
- No data loss for changes made during the offline period
- Steps 5-6 remain pending (not affected by the offline period)
