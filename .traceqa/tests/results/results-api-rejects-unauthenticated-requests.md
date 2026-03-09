---
id: TC-381
title: Results API — returns 401 for unauthenticated requests
status: active
priority: high
type: regression
automation_status: planned
tags: [results, api, auth, security]
files:
  - 'web/src/app/api/workspaces/[id]/results/route.ts'
---

## Preconditions

- No active user session (no auth cookie/token)
- Valid workspace exists

## Steps

| #   | Action                                                         | Expected Result                                                  |
| --- | -------------------------------------------------------------- | ---------------------------------------------------------------- |
| 1   | Send GET to `/api/workspaces/{id}/results` without auth header | Response returns 401 Unauthorized                                |
| 2   | Verify response body contains error code                       | Body includes `code: "UNAUTHORIZED"` or equivalent error message |
| 3   | Send GET with expired session token                            | Response returns 401 Unauthorized                                |

## Final Expected Result

- Unauthenticated requests are rejected with 401
- No result data is leaked in error responses
- Error response follows consistent error format
