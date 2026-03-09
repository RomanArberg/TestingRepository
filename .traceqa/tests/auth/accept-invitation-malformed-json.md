---
id: TC-261
title: Accept invitation API — malformed JSON returns 400
status: active
priority: medium
type: regression
automation_status: planned
tags: [auth, onboarding, invitations, api, validation]
files:
  - web/src/app/api/onboarding/accept/route.ts
---

## Preconditions

- User is logged in via GitHub OAuth
- Request is made directly to the API with invalid JSON

## Steps

| #   | Action                                                                           | Expected Result                        |
| --- | -------------------------------------------------------------------------------- | -------------------------------------- |
| 1   | Send POST to `/api/onboarding/accept` with body `{not valid json`                | API returns 400 Bad Request            |
| 2   | Observe the error message                                                        | Message indicates malformed JSON       |
| 3   | Send POST to `/api/onboarding/accept` with body `{"invitationId": "not-a-uuid"}` | API returns 400 (validation failed)    |
| 4   | Send POST to `/api/onboarding/accept` with empty body `{}`                       | API returns 400 (missing invitationId) |

## Final Expected Result

- Malformed JSON is rejected with 400 before any business logic runs
- Invalid UUID format for invitationId is caught by Zod validation
- Missing required fields return 400 with specific field errors
- No database queries are made for invalid input
