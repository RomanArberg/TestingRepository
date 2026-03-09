---
id: TC-272
title: Create workspace — dialog with repo selection creates initialized workspace
status: active
priority: high
type: smoke
automation_status: planned
tags: [workspaces, create, github, initialization]
files:
  - web/src/components/workspaces/create-workspace-dialog.tsx
  - web/src/components/workspaces/repository-selector.tsx
  - web/src/app/api/workspaces/route.ts
---

## Preconditions

- User is logged in as an organization member
- GitHub App is installed for user's organization
- Project "Acme QA" exists with no workspaces
- User is on the project detail page for "Acme QA"

## Steps

| #   | Action                                              | Expected Result                                                            |
| --- | --------------------------------------------------- | -------------------------------------------------------------------------- |
| 1   | Click the "Add Workspace" button                    | Create Workspace dialog opens with empty form                              |
| 2   | Type "Nightly Regression — Sprint 42" in name field | Name field shows the entered text (em dash preserved)                      |
| 3   | Click the repository selector dropdown              | List of available GitHub repositories loads                                |
| 4   | Select "acme/qa-tests" from the list                | Repository field shows "acme/qa-tests", branch auto-fills with "main"      |
| 5   | Observe the Default Branch field                    | Pre-filled with "main" (repository default)                                |
| 6   | Click "Create Workspace"                            | Button shows "Creating...", form inputs disabled                           |
| 7   | Wait for creation and initialization to complete    | Dialog closes automatically                                                |
| 8   | Observe project detail page                         | New workspace card "Nightly Regression — Sprint 42" appears                |
| 9   | Click on the new workspace card                     | Browser navigates to workspace overview, GitHub card shows "acme/qa-tests" |

## Final Expected Result

- Workspace is created with correct name, repo, and branch
- Repository initialization completes (`.traceqa/` directory created in Git)
- Workspace card appears on project detail page immediately
- Workspace overview shows GitHub connection info
