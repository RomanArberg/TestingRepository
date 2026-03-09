---
id: TC-233
title: Pending invitations — displays list with role badges and inviter
status: active
priority: high
type: acceptance
automation_status: planned
tags: [auth, onboarding, invitations, display]
files:
  - web/src/components/onboarding/pending-invites.tsx
  - web/src/app/api/onboarding/route.ts
  - web/src/app/(auth)/onboarding/page.tsx
---

## Preconditions

- User is logged in via GitHub OAuth
- User has no organization
- User has 2 pending invitations:
  - "DevOps United" with role "admin", invited by "jane@example.com"
  - "QA Collective" with role "member", invited by "Carlos Mendez"

## Steps

| #   | Action                                    | Expected Result                                                            |
| --- | ----------------------------------------- | -------------------------------------------------------------------------- |
| 1   | Navigate to `/onboarding`                 | Onboarding page loads with create org form and pending invitations section |
| 2   | Observe the "or" divider between sections | Divider appears separating the create org form from the invitations list   |
| 3   | Observe the first invitation card         | Shows "DevOps United" with a purple "admin" role badge                     |
| 4   | Observe the inviter on the first card     | Displays "jane@example.com" (email shown when name is unavailable)         |
| 5   | Observe the second invitation card        | Shows "QA Collective" with a blue "member" role badge                      |
| 6   | Observe the inviter on the second card    | Displays "Carlos Mendez" (name shown when available)                       |
| 7   | Verify each card has an "Accept" button   | Both cards show an "Accept" button                                         |

## Final Expected Result

- Pending invitations are listed in order (newest first)
- Admin role badges use purple styling; member badges use blue styling
- Inviter name is shown when available; email is used as fallback
- Each invitation card has a distinct "Accept" button
- The "or" divider only appears when invitations exist
