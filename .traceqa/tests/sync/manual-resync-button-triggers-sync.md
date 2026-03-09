---
id: TC-170
title: Manual re-sync — triggers test case metadata sync from repository
status: active
priority: high
type: acceptance
automation_status: planned
files:
  - 'web/src/app/api/workspaces/[id]/test-cases/sync/route.ts'
  - 'web/src/lib/sync/service.ts'
  - 'web/src/components/layout/sync-button.tsx'
  - 'web/src/hooks/use-workspace-sync.ts'
tags: [sync, resync, manual-trigger, pr-135]
---

## Preconditions

- User is logged in with workspace access
- Workspace has GitHub App installed
- Test cases page is loaded with existing test cases (or empty state)

## Steps

| #   | Action                                                                                                              | Expected Result                                                                    |
| --- | ------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| 1   | Navigate to the test cases page                                                                                     | Page loads showing test cases or empty state                                       |
| 2   | Locate the sync button (RefreshCw icon button) in the workspace header                                              | Button is visible in the header; hovering shows a tooltip with "Last synced X ago" |
| 3   | Click the RefreshCw icon button in the workspace header (or use ⌘+Shift+S on Mac / Ctrl+Shift+S on other platforms) | Syncing indicator appears (spinner with "Syncing..." text)                         |
| 4   | Wait for sync to complete                                                                                           | Test case list updates with synced data from the repository                        |
| 5   | Check the sync status indicator in the header                                                                       | Shows last synced timestamp ("Last synced X ago")                                  |

## Final Expected Result

- Manual sync button is available when sync status is idle or pending
- Clicking triggers a POST to the sync API endpoint
- UI shows syncing state with spinner during the operation
- Test case list refreshes after sync completes
