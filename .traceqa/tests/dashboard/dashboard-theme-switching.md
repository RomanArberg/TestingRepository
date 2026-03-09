---
id: TC-56
title: Theme toggle — dashboard switches between dark and light modes
status: active
priority: medium
type: acceptance
automation_status: manual
tags: [dashboard, theme, dark-mode, light-mode]
files:
  - web/src/components/layout/theme-toggle.tsx
  - web/src/components/layout/theme-provider.tsx
  - 'web/src/app/(dashboard)/dashboard/dashboard-content.tsx'
---

## Preconditions

- User is logged in with dashboard access
- Theme toggle is available in header

## Steps

| #   | Action                                  | Expected Result                                         |
| --- | --------------------------------------- | ------------------------------------------------------- |
| 1   | Navigate to /dashboard                  | Dashboard loads in current theme                        |
| 2   | Toggle to dark theme                    | Background changes to dark palette                      |
| 3   | Check hero section in dark mode         | Pass rate number contrasts well against dark background |
| 4   | Check workspace cards in dark mode      | Cards have elevated background with subtle borders      |
| 5   | Toggle to light theme                   | Background changes to light palette                     |
| 6   | Check hero section in light mode        | Pass rate number is clearly visible                     |
| 7   | Hover over workspace card in light mode | Card lifts with shadow effect                           |

## Final Expected Result

- Theme toggle works without page refresh
- All dashboard components respect the active theme
- Color contrast meets accessibility standards
- Theme persists across page navigation
