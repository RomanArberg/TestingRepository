---
id: TC-263
title: Create organization API — malformed JSON returns 400
status: active
priority: medium
type: regression
automation_status: planned
tags: [auth, org-creation, api, validation]
files:
  - web/src/app/api/organizations/route.ts
---

## Preconditions

- User is logged in via GitHub OAuth
- Request is made directly to the API

## Steps

| #   | Action                                                     | Expected Result                                     |
| --- | ---------------------------------------------------------- | --------------------------------------------------- |
| 1   | Send POST to `/api/organizations` with body `{malformed`   | API returns 400 Bad Request                         |
| 2   | Observe the error message                                  | Message indicates malformed JSON                    |
| 3   | Send POST to `/api/organizations` with empty body `{}`     | API returns 400 (validation failed — name required) |
| 4   | Send POST to `/api/organizations` with body `{"name": ""}` | API returns 400 (name too short)                    |

## Final Expected Result

- Malformed JSON is rejected with 400 before business logic runs
- Empty or missing name field returns a validation error
- No database operations occur for invalid requests
