---
id: TC-234
title: Pending invitations — empty state when no invitations exist
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [auth, onboarding, invitations, empty-state]
files:
  - web/src/components/onboarding/pending-invites.tsx
  - web/src/app/api/onboarding/route.ts
  - web/src/app/(auth)/onboarding/page.tsx
---

## Preconditions

- User is logged in via GitHub OAuth
- User has no organization
- User has zero pending invitations

## Steps

| #   | Action                                     | Expected Result                                       |
| --- | ------------------------------------------ | ----------------------------------------------------- |
| 1   | Navigate to `/onboarding`                  | Onboarding page loads with the create org form        |
| 2   | Observe the area below the create org form | No "or" divider is shown                              |
| 3   | Verify the invitations section             | No pending invitations section or cards are displayed |

## Final Expected Result

- When no invitations exist, the pending invitations section is hidden entirely
- The "or" divider between create org and invitations does not appear
- Only the "Create Organization" form is visible
