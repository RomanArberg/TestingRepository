---
id: TC-248
title: Accept invitation — expired invitation shows expiration error
status: active
priority: high
type: acceptance
automation_status: planned
tags: [auth, onboarding, invitations, expiration, error-handling]
files:
  - web/src/app/api/onboarding/accept/route.ts
  - web/src/components/onboarding/pending-invites.tsx
  - web/src/app/(auth)/onboarding/page.tsx
---

## Preconditions

- User is logged in via GitHub OAuth
- User has no organization
- An invitation exists but has expired (created more than 7 days ago)

## Steps

| #   | Action                                                                    | Expected Result                                                                             |
| --- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1   | Navigate to `/onboarding` (invitation was still cached or page was stale) | Page might display the stale invitation card                                                |
| 2   | Click "Accept" on the expired invitation                                  | API returns 400 error (invitation has expired)                                              |
| 3   | Observe the error display                                                 | Error banner: "This invitation has expired. Request a new one from the organization admin." |
| 4   | Verify the form is still usable                                           | Create organization form remains functional                                                 |

## Final Expected Result

- Expired invitations are rejected at the API level with a clear expiration message
- The error message suggests contacting the organization admin for a new invitation
- The onboarding page remains functional after the error (user can create their own org instead)
