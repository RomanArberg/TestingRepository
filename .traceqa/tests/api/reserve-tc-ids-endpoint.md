---
id: TC-452
title: Reserve TC IDs — atomic ID reservation via API endpoint
status: active
priority: high
type: acceptance
automation_status: planned
tags: [api, test-cases, id-counter, concurrency]
files:
  - 'web/src/app/api/workspaces/[id]/test-cases/reserve-ids/route.ts'
  - web/src/lib/test-cases/id-counter.ts
---

## Preconditions

- User is logged in as org member with workspace access
- Workspace exists with GitHub repository connected
- Workspace has `tc_id_counter` initialized (e.g., at 450)

## Steps

| #   | Action                                                                  | Expected Result                                                      |
| --- | ----------------------------------------------------------------------- | -------------------------------------------------------------------- |
| 1   | Send POST /api/workspaces/{id}/test-cases/reserve-ids with { count: 1 } | Response 200 with { start: 451, end: 451 }                           |
| 2   | Send POST /api/workspaces/{id}/test-cases/reserve-ids with { count: 5 } | Response 200 with { start: 452, end: 456 }                           |
| 3   | Verify reserved IDs are sequential and non-overlapping                  | Start of second call equals end of first call + 1                    |
| 4   | Send POST with no body (defaults to count: 1)                           | Response 200 with { start: 457, end: 457 }                           |
| 5   | Send POST with { count: 0 }                                             | Response 400 with error "Count must be an integer between 1 and 100" |
| 6   | Send POST with { count: 101 }                                           | Response 400 with validation error about count range                 |
| 7   | Send POST without authentication                                        | Response 401 Unauthorized                                            |
| 8   | Send POST as user who is not a member of the workspace's organization   | Response 500 with error from RPC (org membership check fails)        |

## Final Expected Result

- Endpoint atomically reserves sequential TC IDs via PostgreSQL counter
- Reserved ID ranges never overlap even under concurrent requests
- Count defaults to 1 when no body is provided
- Count validation rejects values outside 1-100 range
- Authentication and organization membership are enforced
