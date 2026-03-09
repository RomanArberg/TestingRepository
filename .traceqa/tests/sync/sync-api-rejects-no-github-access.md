---
id: TC-401
title: Sync API — returns 403 when user lacks GitHub write access
status: active
priority: high
type: regression
automation_status: planned
tags: [sync, api, authorization, github, negative]
files:
  - 'web/src/app/api/workspaces/[id]/sync/route.ts'
  - 'web/src/lib/github/access.ts'
---

## Preconditions

- User is authenticated as 'viewer@example.com'
- User is member of workspace organization
- User has read-only access to GitHub repository (not admin or write)

## Steps

| #   | Action                                   | Expected Result                                      |
| --- | ---------------------------------------- | ---------------------------------------------------- |
| 1   | Send POST to `/api/workspaces/{id}/sync` | requireGitHubAccess() checks repository permissions  |
| 2   | Verify response status                   | Returns 403 Forbidden                                |
| 3   | Verify error message                     | Indicates insufficient GitHub repository permissions |
| 4   | Verify no sync operations occurred       | No buffer locks, no Git commits                      |

## Final Expected Result

- Users without GitHub write permission cannot trigger sync
- Permission check uses GitHub's collaborator permission API
- Clear error message distinguishes from organization membership issues
