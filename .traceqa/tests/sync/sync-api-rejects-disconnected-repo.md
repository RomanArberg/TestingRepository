---
id: TC-396
title: Sync API — rejects request when GitHub repository is disconnected
status: active
priority: high
type: regression
automation_status: planned
tags: [sync, api, negative, configuration]
files:
  - 'web/src/app/api/workspaces/[id]/sync/route.ts'
---

## Preconditions

- User is authenticated with workspace access
- Workspace exists but has no github_repo configured (null or empty)
- GitHub App is installed

## Steps

| #   | Action                                                   | Expected Result                                                 |
| --- | -------------------------------------------------------- | --------------------------------------------------------------- |
| 1   | Send POST to `/api/workspaces/{id}/sync` with valid body | Response returns 400 Bad Request                                |
| 2   | Verify error response body                               | Contains error code indicating missing repository configuration |
| 3   | Verify no GitHub API calls were made                     | Error occurs before any GitHub interaction                      |
| 4   | Check session buffer                                     | No syncing_at locks were acquired (buffer unchanged)            |

## Final Expected Result

- Missing repository configuration is caught before sync attempt
- Clear error message guides user to connect a repository first
- No partial state changes from rejected sync
