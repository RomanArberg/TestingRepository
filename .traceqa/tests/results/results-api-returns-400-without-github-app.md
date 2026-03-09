---
id: TC-383
title: Results API — returns 400 when GitHub App not installed
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [results, api, github-app, configuration]
files:
  - 'web/src/app/api/workspaces/[id]/results/route.ts'
---

## Preconditions

- User is authenticated and member of workspace organization
- Workspace exists but does NOT have GitHub App installed (no `github_installation_id`)

## Steps

| #   | Action                                                                         | Expected Result                                            |
| --- | ------------------------------------------------------------------------------ | ---------------------------------------------------------- |
| 1   | Send GET to `/api/workspaces/{id}/results`                                     | Response returns 400 Bad Request                           |
| 2   | Verify error message                                                           | Body indicates GitHub App installation is required         |
| 3   | Send GET to `/api/workspaces/{id}/results` for workspace with no `github_repo` | Response returns 400 with message about missing repository |

## Final Expected Result

- API clearly communicates when GitHub integration is not configured
- Different error messages for missing installation vs missing repo
- No attempt to fetch from GitHub when config is incomplete
