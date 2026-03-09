---
id: TC-429
title: Concurrency — simultaneous test case creation uses atomic ID counter
status: active
priority: high
type: regression
automation_status: planned
tags: [api, concurrency, test-cases, cross-cutting]
files:
  - 'web/src/app/api/workspaces/[id]/test-cases/route.ts'
  - web/src/lib/test-cases/id-counter.ts
---

## Preconditions

- User is logged in as org member with workspace access
- Workspace exists with GitHub repository connected and synced test cases
- Workspace has `tc_id_counter` initialized (via sync or prior test case creation)

## Steps

| #   | Action                                                                                      | Expected Result                                                   |
| --- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| 1   | Send two POST /api/workspaces/{id}/test-cases requests simultaneously with different titles | Both requests are processed                                       |
| 2   | Wait for both responses                                                                     | Both return 201 Created with unique sequential test case IDs      |
| 3   | Verify both test cases have distinct IDs                                                    | IDs are sequential (e.g., TC-452 and TC-453) with no collision    |
| 4   | Check workspace tc_id_counter value                                                         | Counter reflects both reservations (incremented by 2 total)       |
| 5   | Send a third POST request to create another test case                                       | Returns 201 with ID continuing the sequence (e.g., TC-454)        |
| 6   | Simulate counter reservation failure (e.g., workspace not found)                            | Server returns 500 with error "Failed to generate test case ID"   |
| 7   | Verify no partial test case was created from the failed attempt                             | Test case count is unchanged; no orphaned files in Git repository |

## Final Expected Result

- Concurrent test case creation never produces duplicate IDs
- Atomic counter (tc_id_counter) guarantees unique sequential IDs without retry logic
- Each reservation atomically increments the counter via PostgreSQL row-level lock
- Counter reservation failure returns 500 without creating partial records
- No data corruption occurs from concurrent requests
