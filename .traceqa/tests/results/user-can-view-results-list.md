---
id: TC-154
title: Results list — displays execution results with status badges and metadata
status: active
priority: high
type: acceptance
automation_status: planned
files:
  - web/src/app/(dashboard)/workspaces/[slug]/results/page.tsx
  - web/src/components/results/results-list.tsx
  - web/src/hooks/use-results.ts
tags: [results, page]
---

## Preconditions

- User is logged in with workspace access
- Workspace exists with GitHub App installed
- At least one test execution result exists in the workspace

## Steps

| #   | Action                                   | Expected Result                                       |
| --- | ---------------------------------------- | ----------------------------------------------------- |
| 1   | Navigate to `/workspaces/{slug}/results` | Results page loads with breadcrumb and header         |
| 2   | Observe page header                      | Shows "Execution Results" title and description       |
| 3   | Observe breadcrumb                       | Shows workspace slug > Results                        |
| 4   | Observe results list                     | Displays list of execution results with status badges |

## Final Expected Result

- Results page loads without errors
- Page displays list of execution results
- Each result shows: test case title, status badge, cycle, executed by, date
- Status badges use correct colors (green=passed, red=failed, amber=blocked, gray=skipped)
