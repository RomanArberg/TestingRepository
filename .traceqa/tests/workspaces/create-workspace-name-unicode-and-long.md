---
id: TC-285
title: Create workspace — handles unicode names and boundary lengths
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [workspaces, create, validation, boundary, unicode]
files:
  - web/src/app/api/workspaces/route.ts
  - web/src/components/workspaces/create-workspace-dialog.tsx
---

## Preconditions

- User is logged in as an organization member
- GitHub App is installed
- Create Workspace dialog is open

## Steps

| #   | Action                                                     | Expected Result                                                  |
| --- | ---------------------------------------------------------- | ---------------------------------------------------------------- |
| 1   | Type "テスト管理 — 日本語ワークスペース" in the name field | Name field shows the Japanese characters                         |
| 2   | Select a repository and branch                             | Repo and branch selected                                         |
| 3   | Click "Create Workspace"                                   | Workspace created successfully with a slug derived from the name |
| 4   | Observe the workspace card                                 | Card shows the Japanese workspace name correctly                 |
| 5   | Open Create Workspace dialog again                         | Dialog opens with empty form                                     |
| 6   | Type exactly 100 characters in name field                  | Name field accepts all characters                                |
| 7   | Select a repository and click "Create Workspace"           | Workspace created successfully (100 char boundary)               |
| 8   | Open dialog again, type 101 characters                     | Name field accepts input                                         |
| 9   | Click "Create Workspace"                                   | Validation error about max 100 characters                        |

## Final Expected Result

- Unicode workspace names (CJK, emoji, accented chars) are stored and displayed correctly
- Names at exactly 100 characters are accepted
- Names exceeding 100 characters are rejected with validation error
- Slug generation handles non-Latin characters gracefully
