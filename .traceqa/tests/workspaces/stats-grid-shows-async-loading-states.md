---
id: TC-204
title: Stats grid — async loading states before final values
status: active
priority: medium
type: acceptance
automation_status: manual
tags: [workspace, overview, stats, loading]
files:
  - web/src/components/workspaces/workspace-stats-grid.tsx
  - web/src/app/(dashboard)/workspaces/[slug]/page.tsx
---

## Preconditions

- User is logged in with workspace access
- Workspace has GitHub connected with cycles and tasks
- User is on workspace overview page (`/workspaces/{slug}`)

## Steps

| #   | Action                                | Expected Result                                     |
| --- | ------------------------------------- | --------------------------------------------------- |
| 1   | Hard refresh the page (Ctrl+Shift+R)  | Page begins loading                                 |
| 2   | Observe "Test Cases" stat immediately | Shows numeric value instantly (server-rendered)     |
| 3   | Observe "Active Cycles" stat          | May show loading skeleton briefly, then shows count |
| 4   | Observe "My Tasks" stat               | May show loading skeleton briefly, then shows count |
| 5   | Observe "Pass Rate" stat              | Shows "—" placeholder (no execution data yet)       |
| 6   | Wait for all stats to load            | All four stat cards show their final values         |

## Final Expected Result

- Test Cases count appears instantly (database query)
- Active Cycles and My Tasks load asynchronously (may show skeleton)
- Pass Rate shows placeholder until execution data is available
- No errors or broken states during loading
- Final state shows all four metrics clearly
