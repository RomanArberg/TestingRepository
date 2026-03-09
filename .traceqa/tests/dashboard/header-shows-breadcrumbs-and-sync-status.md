---
id: TC-58
title: Header breadcrumbs — context-aware workspace name and controls
status: active
priority: high
type: acceptance
automation_status: planned
tags: [dashboard, header, breadcrumbs, sync-status]
files: [web/src/components/layout/header.tsx, web/src/components/layout/theme-toggle.tsx]
---

## Preconditions

- User is logged in with access to at least one workspace (e.g., slug "qa-sprint")
- Browser viewport is desktop width (768px+)

## Steps

| #   | Action                                       | Expected Result                                                               |
| --- | -------------------------------------------- | ----------------------------------------------------------------------------- |
| 1   | Navigate to /dashboard                       | Header shows breadcrumb with "Projects" link; no workspace name in breadcrumb |
| 2   | Observe the right side of the header         | Branch selector, theme toggle, sync status badge, and user menu are visible   |
| 3   | Navigate to /workspaces/qa-sprint            | Breadcrumb updates to show "Projects" > "Qa Sprint"                           |
| 4   | Observe the sync status badge                | Shows "All synced" with green indicator                                       |
| 5   | Navigate to /workspaces/qa-sprint/test-cases | Breadcrumb still shows "Projects" > "Qa Sprint"                               |
| 6   | Open the user menu (click the avatar button) | Dropdown shows Profile, Settings, and Sign out options                        |

## Final Expected Result

- Breadcrumb displays "Projects" link on all pages; adds workspace name when inside a workspace
- Sync status badge shows current state: synced (green), syncing (spinning indicator), or unsaved (amber)
- Branch selector, theme toggle, and user menu are always present in the header
- Workspace name is derived from the URL slug (formatted as title case)
