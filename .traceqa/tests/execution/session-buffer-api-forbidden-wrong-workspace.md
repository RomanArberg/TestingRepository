---
id: TC-375
title: 'Session buffer API — non-member workspace access returns 403'
status: active
priority: high
type: regression
automation_status: planned
tags: [execution, session-buffer, api, security, negative]
files:
  - 'web/src/app/api/workspaces/[id]/session-buffer/route.ts'
---

## Preconditions

- User is logged in with workspace access to Workspace A
- Workspace B exists but user is NOT a member
- A cycle with execution data exists in Workspace B

## Steps

| #   | Action                                                                           | Expected Result                             |
| --- | -------------------------------------------------------------------------------- | ------------------------------------------- |
| 1   | Send a POST to /api/workspaces/{workspaceB}/session-buffer with valid auth       | Response returns 403 Forbidden              |
| 2   | Send a GET to /api/workspaces/{workspaceB}/session-buffer/status with valid auth | Response returns 403 Forbidden              |
| 3   | Observe the error message                                                        | Error indicates user lacks workspace access |

## Final Expected Result

- Authenticated users cannot access session buffers in workspaces they are not members of
- Server validates workspace membership before processing any buffer operation
- Error response returns 403 with FORBIDDEN code
- No execution data from Workspace B is leaked to the non-member
