---
id: TC-136
title: Result detail page — shows loading skeleton during data fetch
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [results, detail-view, loading]
files:
  - 'web/src/app/(dashboard)/workspaces/[slug]/results/[cycleId]/[testCaseId]/[assignee]/loading.tsx'
  - 'web/src/components/results/result-detail-content.tsx'
---

## Preconditions

- User is logged in with workspace access
- Valid result exists in the workspace
- Network is available but slow (can be simulated with throttling)

## Steps

| #   | Action                                                   | Expected Result                                            |
| --- | -------------------------------------------------------- | ---------------------------------------------------------- |
| 1   | Enable network throttling in browser dev tools (Slow 3G) | Network simulation active                                  |
| 2   | Navigate directly to a valid result detail URL           | Loading skeleton appears immediately                       |
| 3   | Observe loading skeleton structure                       | Shows skeleton for breadcrumb, header, metadata, and steps |
| 4   | Wait for data to load                                    | Content replaces skeleton smoothly                         |
| 5   | Disable network throttling                               | Normal speed restored                                      |

## Final Expected Result

- Loading state provides visual feedback during data fetch
- Skeleton structure matches final content layout
- No layout shift when content loads
