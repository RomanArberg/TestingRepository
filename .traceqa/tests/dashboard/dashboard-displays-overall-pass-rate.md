---
id: TC-49
title: Hero section — pass rate percentage with color coding and glow
status: active
priority: high
type: acceptance
automation_status: planned
tags: [dashboard, hero-section, pass-rate, design-tokens]
files:
  [
    web/src/components/dashboard/hero-section.tsx,
    web/src/components/command-center/hero-metric.tsx,
    web/src/lib/dashboard/calculations.ts,
  ]
---

## Preconditions

- User is logged in with access to at least one workspace
- Workspace "QA-Team" has 100 test cases with execution results: 87 passed, 13 failed (87% pass rate)
- User navigates to `/dashboard`

## Steps

| #   | Action                     | Expected Result                                              |
| --- | -------------------------- | ------------------------------------------------------------ |
| 1   | Navigate to /dashboard     | Dashboard page loads                                         |
| 2   | Observe hero section       | Large pass rate number is prominently displayed              |
| 3   | Check pass rate formatting | Number shows percentage (e.g., "87%")                        |
| 4   | Check pass rate color      | Green if >= 80%, red if < 80%                                |
| 5   | Check glow effect          | Subtle teal glow visible behind number when healthy (>= 80%) |
| 6   | Verify subtitle            | Shows "Across X tests in Y workspaces" text                  |

## Final Expected Result

- Pass rate is the dominant visual element in the hero section
- Color coding accurately reflects health status
- Glow effect appears only for healthy pass rates (>= 80%)
- Test count and workspace count are accurate
