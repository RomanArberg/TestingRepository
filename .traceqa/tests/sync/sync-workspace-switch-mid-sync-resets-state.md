---
id: TC-552
title: Workspace sync — switching workspaces mid-sync resets state for new workspace
status: active
priority: medium
type: regression
automation_status: manual
tags: [sync, workspace, state-management, regression]
files:
  - web/src/hooks/use-workspace-sync.ts
---

## Preconditions

- User is logged in with access to at least two workspaces (Workspace A and Workspace B)
- Both workspaces are connected to GitHub repositories
- User is on Workspace A's page

## Steps

| #   | Action                                                        | Expected Result                                                                        |
| --- | ------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| 1   | Click the sync button in Workspace A's header                 | "Syncing..." loading toast appears                                                     |
| 2   | Immediately navigate to Workspace B before the sync completes | Workspace B loads with its own data and sync state                                     |
| 3   | Observe Workspace B's sync button tooltip                     | Tooltip shows Workspace B's own "Last synced" timestamp (not Workspace A's)            |
| 4   | Wait for any pending operations to complete                   | No stale sync result from Workspace A appears in Workspace B                           |
| 5   | Trigger sync on Workspace B                                   | Sync runs for Workspace B's repository, success toast appears with Workspace B context |

## Final Expected Result

- Switching workspaces mid-sync discards the pending sync result for the previous workspace
- The new workspace shows its own independent sync state
- No cross-workspace state pollution occurs
- Sync results from Workspace A never appear in Workspace B's UI
