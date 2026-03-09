---
id: TC-209
title: Workspace overview — displays all sections with GitHub connected
status: active
priority: high
type: smoke
automation_status: planned
tags: [workspace, overview]
files:
  - web/src/app/(dashboard)/workspaces/[slug]/page.tsx
  - web/src/components/workspaces/workspace-stats-grid.tsx
---

## Preconditions

- User is logged in with workspace access
- Workspace exists with GitHub repository connected
- User has organization membership for the workspace

## Steps

| #   | Action                                      | Expected Result                                                                     |
| --- | ------------------------------------------- | ----------------------------------------------------------------------------------- |
| 1   | Navigate to `/workspaces/{slug}`            | Workspace overview page loads (no redirect to my-tasks)                             |
| 2   | Observe workspace header at top of page     | Shows workspace name as heading with gear icon on right                             |
| 3   | Observe GitHub Connection card below header | Shows repository name (e.g., "org/repo") and branch info                            |
| 4   | Scroll to Overview section                  | Section heading "Overview" is visible                                               |
| 5   | Observe WorkspaceStatsGrid below heading    | Four stat cards displayed in a row (Test Cases, Active Cycles, My Tasks, Pass Rate) |

## Final Expected Result

- Page displays without redirect
- Workspace header shows name and settings gear icon
- GitHub connection card shows repo and branch information
- Settings is accessible via gear icon in the workspace header
- WorkspaceStatsGrid shows 4 metrics
- Layout is clean and matches TraceQA design system
