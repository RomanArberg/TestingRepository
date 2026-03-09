---
id: TC-161
title: GitHub settings — linked account displays username with checkmark
status: active
priority: high
type: acceptance
automation_status: planned
tags: [settings, github, authentication]
files:
  [
    web/src/components/settings/github-account-card.tsx,
    web/src/app/(dashboard)/settings/github/page.tsx,
  ]
---

## Preconditions

- User is logged in to TraceQA
- User has a GitHub account linked (github_username is populated in database)
- User navigates to Settings > GitHub page

## Steps

| #   | Action                            | Expected Result                                         |
| --- | --------------------------------- | ------------------------------------------------------- |
| 1   | Navigate to /settings/github      | GitHub Integration page loads                           |
| 2   | Observe the "GitHub Account" card | Card is visible at the top of the page                  |
| 3   | Check the account status display  | Shows green checkmark icon with "Linked as @{username}" |
| 4   | Verify username is displayed      | Username is shown in monospace font with @ prefix       |

## Final Expected Result

- User sees their linked GitHub username displayed prominently
- Green checkmark indicates successful link status
- No "Link GitHub Account" button is shown for linked users
