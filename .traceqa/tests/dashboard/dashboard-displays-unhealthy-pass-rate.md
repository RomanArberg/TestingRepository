---
id: TC-441
title: Hero section — pass rate below 80% shows red color without glow
status: active
priority: high
type: acceptance
automation_status: planned
tags: [dashboard, hero-section, pass-rate, design-tokens, negative]
files:
  - web/src/components/dashboard/hero-section.tsx
  - web/src/components/command-center/hero-metric.tsx
  - web/src/lib/dashboard/calculations.ts
---

## Preconditions

- User is logged in with access to at least one workspace
- Workspace "Support-Team" has 50 test cases with execution results: 30 passed, 20 failed (60% pass rate)
- User navigates to `/dashboard`

## Steps

| #   | Action                     | Expected Result                                    |
| --- | -------------------------- | -------------------------------------------------- |
| 1   | Navigate to /dashboard     | Dashboard page loads                               |
| 2   | Observe hero section       | Large pass rate number is prominently displayed    |
| 3   | Check pass rate formatting | Number shows "60%"                                 |
| 4   | Check pass rate color      | Red color displayed (pass rate < 80%)              |
| 5   | Check glow effect          | No glow effect visible (unhealthy pass rate < 80%) |
| 6   | Verify subtitle            | Shows "Across 50 tests in 1 workspace" text        |

## Final Expected Result

- Pass rate below 80% is displayed in red (unhealthy state)
- No glow effect for unhealthy pass rates
- Subtitle accurately reflects test count and workspace count
- Companion to TC-49 which covers the healthy (≥80%) scenario
