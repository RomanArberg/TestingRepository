---
id: TC-239
title: Auth middleware — authenticated user without org redirected to onboarding
status: active
priority: critical
type: acceptance
automation_status: planned
tags: [auth, middleware, onboarding, redirect]
files:
  - web/src/middleware.ts
  - web/src/lib/supabase/middleware.ts
---

## Preconditions

- User is logged in with a valid session
- User does NOT have any organization membership
- User completed OAuth but has not created or joined an organization

## Steps

| #   | Action                                  | Expected Result                                       |
| --- | --------------------------------------- | ----------------------------------------------------- |
| 1   | Navigate to `/dashboard`                | User is redirected to `/onboarding`                   |
| 2   | Navigate to `/projects`                 | User is redirected to `/onboarding`                   |
| 3   | Navigate to `/onboarding`               | Onboarding page loads normally (exempt route)         |
| 4   | Navigate to `/api/organizations` (POST) | API responds normally (exempt route for org creation) |

## Final Expected Result

- Authenticated users without an organization are redirected to `/onboarding` on all protected routes
- Organization-exempt routes (`/onboarding`, `/api/organizations`, `/api/onboarding`) are accessible
- The redirect is server-side (no flash of protected content before redirect)
