---
id: TC-415
title: Auth middleware — user without organization redirected to onboarding
status: active
priority: high
type: acceptance
automation_status: planned
tags: [auth, middleware, onboarding, cross-cutting]
files: [web/src/lib/supabase/middleware.ts]
---

## Preconditions

- User is authenticated via GitHub OAuth
- User has no organization membership (new user)

## Steps

| #   | Action                                              | Expected Result                          |
| --- | --------------------------------------------------- | ---------------------------------------- |
| 1   | Navigate to /dashboard                              | Browser redirects to /onboarding         |
| 2   | Navigate to /settings                               | Browser redirects to /onboarding         |
| 3   | Navigate to /onboarding                             | Onboarding page loads normally           |
| 4   | Navigate to /api/organizations (POST to create org) | API processes request (org-exempt route) |
| 5   | Navigate to /api/invitations/accept                 | API processes request (org-exempt route) |

## Final Expected Result

- Authenticated users without organization membership are redirected to /onboarding
- Org-exempt routes (/onboarding, /api/organizations, /api/invitations/accept) remain accessible
- After creating an organization, /onboarding redirects to /dashboard
