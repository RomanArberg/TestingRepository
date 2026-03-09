---
id: TC-59
title: My Tasks table rows — clean row styling without left border accent
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [dashboard, my-tasks, visual-redesign, tabular-layout]
files:
  - web/src/components/my-tasks/my-tasks-list-item.tsx
---

## Preconditions

- User is logged in with workspace access
- Tasks are assigned to the user in cycles with different statuses (active, draft, completed, archived)

## Steps

| #   | Action                                   | Expected Result                                                                         |
| --- | ---------------------------------------- | --------------------------------------------------------------------------------------- |
| 1   | Navigate to the My Tasks page            | Task table renders with assigned tasks in rows                                          |
| 2   | Observe table rows across all cycles     | No left border accent is present on any row                                             |
| 3   | Compare with the Cycles detail page      | Cycles page shows conditional left borders (failed/blocked/selected); My Tasks does not |
| 4   | Click a task row                         | Navigation occurs to the execution page for that task                                   |
| 5   | Use keyboard (Tab + Enter) on a task row | Task activates correctly; visible focus ring appears                                    |
| 6   | Hover over a task row                    | Row shows subtle background color transition                                            |

## Final Expected Result

- Table rows have no left border accent (CYCLE_BORDER_TOKENS removed)
- Row styling is clean: cursor pointer, hover transition, focus ring
- Consistent with standard table row patterns (unlike Cycles which uses conditional borders for triage signals)
- Both click and keyboard activation work correctly
