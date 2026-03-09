---
id: TC-208
title: Workspace header — displays correct workspace name
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [workspace, layout]
files:
  - web/src/app/(dashboard)/workspaces/[slug]/layout.tsx
---

## Preconditions

- User is logged in
- User has access to a workspace named "My Test Project"

## Steps

| #   | Action                                        | Expected Result                                    |
| --- | --------------------------------------------- | -------------------------------------------------- |
| 1   | Navigate to the workspace                     | Workspace page loads                               |
| 2   | Observe the header area above navigation tabs | Header displays "My Test Project" (workspace name) |
| 3   | Navigate to different tabs within workspace   | Header remains visible with same workspace name    |

## Final Expected Result

- Workspace name is displayed prominently in header
- Header is consistent across all workspace pages
