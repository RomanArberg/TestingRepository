---
id: TC-156
title: Dark mode — execution panel footer and error text are readable
status: active
priority: high
type: regression
automation_status: manual
tags: [settings, dark-mode, execution, color-tokens]
files: [web/src/components/layout/theme-toggle.tsx, web/src/components/layout/theme-provider.tsx]
---

## Preconditions

- User is logged in with workspace access
- A test execution page is accessible
- Application is set to dark mode

## Steps

| #   | Action                                            | Expected Result                                       |
| --- | ------------------------------------------------- | ----------------------------------------------------- |
| 1   | Navigate to test execution page                   | Execution panel loads                                 |
| 2   | Toggle to dark mode (if not already)              | UI switches to dark theme                             |
| 3   | Check footer background and text                  | Footer background and text colors adapt to dark theme |
| 4   | Trigger an error state (e.g., disconnect network) | Error message appears                                 |
| 5   | Verify error message styling                      | Error text is readable against dark background        |

## Final Expected Result

- Footer uses theme-aware background and text colors
- Error text is clearly readable in dark mode
- No light-mode-only colors bleed through
