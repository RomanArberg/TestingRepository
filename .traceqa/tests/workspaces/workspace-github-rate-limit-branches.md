---
id: TC-286
title: Branch listing — handles GitHub API rate limit gracefully
status: active
priority: medium
type: regression
automation_status: manual
tags: [workspaces, github, rate-limit, error-handling]
files:
  - web/src/app/api/workspaces/[id]/branches/route.ts
  - web/src/components/workspaces/branch-selector.tsx
---

## Preconditions

- User is logged in with workspace access
- Workspace is connected to a GitHub repository
- GitHub API rate limit is approaching or exceeded

## Steps

| #   | Action                                            | Expected Result                                            |
| --- | ------------------------------------------------- | ---------------------------------------------------------- |
| 1   | Open branch selector on workspace settings        | Selector attempts to fetch branches                        |
| 2   | Observe behavior when rate limited (429 response) | Error state shown with retry button instead of branch list |
| 3   | Click "Retry" button                              | Selector attempts to fetch branches again                  |
| 4   | Wait for rate limit to reset                      | Branches load successfully on next attempt                 |

## Final Expected Result

- Rate limit errors from GitHub API are caught and displayed as user-friendly error
- Retry mechanism allows recovery without page refresh
- No unhandled errors or blank dropdowns
