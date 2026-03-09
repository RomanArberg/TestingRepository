---
id: TC-198
title: Workspace navigation tabs — links are visible
status: active
priority: high
type: acceptance
automation_status: planned
tags: [workspace, navigation]
files:
  - web/src/components/workspaces/workspace-nav.tsx
  - web/src/app/(dashboard)/workspaces/[slug]/layout.tsx
---

## Preconditions

- User is logged in with workspace access
- User is viewing a workspace

## Steps

| #   | Action             | Expected Result                                    |
| --- | ------------------ | -------------------------------------------------- |
| 1   | Click "Test Cases" | Browser navigates to /workspaces/{slug}/test-cases |
| 2   | Observe nav state  | "Test Cases" link has teal underline indicator     |
| 3   | Click "Cycles"     | Browser navigates to /workspaces/{slug}/cycles     |
| 4   | Observe nav state  | "Cycles" link has teal underline indicator         |
| 5   | Click "Results"    | Browser navigates to /workspaces/{slug}/results    |
| 6   | Observe nav state  | "Results" link has teal underline indicator        |

## Final Expected Result

- All workspace navigation links route to correct pages
- Active link is indicated with teal underline
- Navigation is consistent across all workspace pages
