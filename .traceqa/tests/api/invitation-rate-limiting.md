---
id: TC-439
title: Invitations API — rejects when pending invitation limit reached
status: active
priority: medium
type: regression
automation_status: planned
tags: [api, invitations, rate-limiting, negative]
files: [web/src/app/api/invitations/route.ts, web/src/lib/validations/invitation.ts]
---

## Preconditions

- User is logged in as org admin
- Organization already has the maximum number of pending invitations

## Steps

| #   | Action                                                     | Expected Result                                |
| --- | ---------------------------------------------------------- | ---------------------------------------------- |
| 1   | Call POST /api/invitations with a new email and valid role | Response 429 Too Many Requests                 |
| 2   | Verify the error message                                   | Message indicates too many pending invitations |
| 3   | Cancel one existing pending invitation                     | Invitation is removed                          |
| 4   | Retry POST /api/invitations with the same new email        | Response 201 Created (slot freed up)           |

## Final Expected Result

- Pending invitation count is enforced
- 429 status code is returned when limit is reached
- Freeing up an invitation slot allows new invitations
