---
id: TC-251
title: Accept invitation — non-existent invitation returns 404
status: active
priority: medium
type: regression
automation_status: planned
tags: [auth, onboarding, invitations, error-handling]
files:
  - web/src/app/api/onboarding/accept/route.ts
---

## Preconditions

- User is logged in via GitHub OAuth
- No invitation exists with the provided ID (or invitation was already accepted/cancelled)

## Steps

| #   | Action                                                          | Expected Result                            |
| --- | --------------------------------------------------------------- | ------------------------------------------ |
| 1   | Attempt to accept an invitation using a non-existent or used ID | API returns 404 error                      |
| 2   | Observe the error message                                       | Message: "Invitation not found" or similar |

## Final Expected Result

- Non-existent or already-used invitation IDs return a 404 error
- The error message does not leak information about other invitations
- Only invitations with status "pending" can be accepted
