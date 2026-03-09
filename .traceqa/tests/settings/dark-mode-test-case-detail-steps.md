---
id: TC-159
title: Dark mode — test case step cards maintain contrast
status: active
priority: medium
type: regression
automation_status: manual
tags: [settings, dark-mode, test-cases, color-tokens]
files: [web/src/components/layout/theme-toggle.tsx, web/src/components/layout/theme-provider.tsx]
---

## Preconditions

- User is logged in with workspace access
- A test case with at least 3 steps exists (e.g., "Login Smoke Test")
- Application is set to dark mode

## Steps

| #   | Action                                    | Expected Result                                        |
| --- | ----------------------------------------- | ------------------------------------------------------ |
| 1   | Navigate to any test case detail page     | Test case detail loads with step cards                 |
| 2   | Toggle to dark mode (if not already)      | UI switches to dark theme                              |
| 3   | Check step card backgrounds               | Cards use theme-aware background color                 |
| 4   | Verify step numbers and text are readable | Proper contrast maintained between text and background |

## Final Expected Result

- Step cards use theme-aware background colors in dark mode
- Step numbers and text maintain proper contrast
- No light-mode-only background values appear
