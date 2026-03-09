---
id: TC-258
title: Create organization API — unauthenticated request returns 401
status: active
priority: critical
type: acceptance
automation_status: planned
tags: [auth, org-creation, api, security]
files:
  - web/src/app/api/organizations/route.ts
---

## Preconditions

- No active authentication session
- Request is made directly to the API (not through the UI)

## Steps

| #   | Action                                                                                           | Expected Result               |
| --- | ------------------------------------------------------------------------------------------------ | ----------------------------- |
| 1   | Send a POST request to `/api/organizations` with body `{"name": "Hack Corp"}` but no auth cookie | API returns 401 Unauthorized  |
| 2   | Verify the response body                                                                         | Error message: "Unauthorized" |

## Final Expected Result

- The organizations API rejects unauthenticated requests with 401
- No organization is created
- The error does not leak information about existing organizations
