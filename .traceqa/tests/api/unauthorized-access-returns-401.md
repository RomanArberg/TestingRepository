---
id: TC-5
title: Results API — unauthenticated request returns 401
status: active
priority: high
type: acceptance
automation_status: planned
tags: [results, api, security, auth]
files:
  - 'web/src/app/api/workspaces/[id]/results/route.ts'
  - 'web/src/lib/supabase/middleware.ts'
---

## Preconditions

- No active user session (cookies cleared or no auth token)
- API endpoint exists: GET /api/workspaces/{id}/results

## Steps

| #   | Action                                                    | Expected Result                                           |
| --- | --------------------------------------------------------- | --------------------------------------------------------- |
| 1   | Clear all browser cookies and session storage             | No active session exists                                  |
| 2   | Call GET /api/workspaces/{id}/results without credentials | Response status 401 Unauthorized                          |
| 3   | Verify response body                                      | JSON contains error: 'Unauthorized'                       |
| 4   | Verify no data is leaked                                  | Response contains only the error object, no results array |

## Final Expected Result

- Unauthenticated requests return 401 Unauthorized
- No execution data is exposed to unauthenticated users
- Error response format is consistent with other API endpoints
