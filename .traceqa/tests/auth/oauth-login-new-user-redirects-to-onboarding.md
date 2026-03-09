---
id: TC-230
title: OAuth login — new user without org redirected to onboarding
status: active
priority: critical
type: smoke
automation_status: planned
tags: [auth, login, onboarding, redirect, new-user]
files:
  - web/src/app/api/auth/callback/route.ts
  - web/src/middleware.ts
  - web/src/lib/supabase/middleware.ts
  - web/src/app/(auth)/onboarding/page.tsx
---

## Preconditions

- No existing user account for the GitHub identity being used
- Browser has no active session

## Steps

| #   | Action                             | Expected Result                                                  |
| --- | ---------------------------------- | ---------------------------------------------------------------- |
| 1   | Navigate to `/login`               | Login page displays with "Continue with GitHub" button           |
| 2   | Click "Continue with GitHub"       | GitHub OAuth flow initiates                                      |
| 3   | Complete GitHub authorization      | Auth callback creates a new user record in the database          |
| 4   | Observe the redirect destination   | User is redirected to `/onboarding` (middleware detects no org)  |
| 5   | Verify the onboarding page content | "Welcome to TraceQA" heading is displayed with org creation form |

## Final Expected Result

- New users who complete OAuth are created in the database with GitHub metadata (username, avatar, github_id)
- Middleware detects no organization membership and redirects to `/onboarding`
- Onboarding page loads with the "Create Organization" form
