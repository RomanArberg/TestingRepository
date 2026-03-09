---
id: TC-426
title: API routing — nonexistent workspace ID returns 404
status: active
priority: high
type: acceptance
automation_status: planned
tags: [api, routing, negative, cross-cutting]
files:
  - 'web/src/app/api/workspaces/[id]/route.ts'
  - 'web/src/app/api/workspaces/[id]/test-cases/route.ts'
  - 'web/src/app/api/workspaces/[id]/cycles/route.ts'
---

## Preconditions

- User is logged in as org member
- Workspace ID '00000000-0000-0000-0000-000000000000' does not exist

## Steps

| #   | Action                                                                            | Expected Result                                               |
| --- | --------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| 1   | Call GET /api/workspaces/00000000-0000-0000-0000-000000000000/test-cases          | Response 404 with error message                               |
| 2   | Call GET /api/workspaces/00000000-0000-0000-0000-000000000000/cycles              | Response 404 with error message                               |
| 3   | Call GET /api/workspaces/00000000-0000-0000-0000-000000000000                     | Response 404 with error message                               |
| 4   | Verify error response does not reveal whether the workspace exists in another org | Error message is generic 'Not found' or 'Workspace not found' |

## Final Expected Result

- Nonexistent workspace IDs return 404 Not Found
- Error messages do not distinguish between 'does not exist' and 'no access' to prevent enumeration
- Response format matches the standard error structure
