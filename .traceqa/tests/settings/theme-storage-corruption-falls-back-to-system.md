---
id: TC-411
title: Theme toggle — corrupted localStorage falls back to system default
status: active
priority: medium
type: regression
automation_status: planned
tags: [settings, theme, negative-test, localStorage, error-handling]
files: [web/src/components/layout/theme-toggle.tsx, web/src/components/layout/theme-provider.tsx]
---

## Preconditions

- User is logged in
- Browser DevTools console is accessible
- User is on any page within the application

## Steps

| #   | Action                                                          | Expected Result                                                        |
| --- | --------------------------------------------------------------- | ---------------------------------------------------------------------- |
| 1   | Open browser DevTools → Application → Local Storage             | localStorage entries are visible                                       |
| 2   | Find the theme key (typically "theme" or "next-themes-theme")   | Current theme value is visible (e.g., "light", "dark", or "system")    |
| 3   | Manually edit the value to an invalid string: "invalidTheme123" | Value is changed in localStorage                                       |
| 4   | Hard-refresh the page (Ctrl+Shift+R)                            | Page reloads                                                           |
| 5   | Observe the rendered theme                                      | Page renders in system default theme (not broken/unstyled)             |
| 6   | Observe the theme toggle icon                                   | Shows the correct icon for the active theme (not stuck in error state) |
| 7   | Click the theme toggle                                          | Theme cycles normally to the next valid mode                           |
| 8   | Hard-refresh the page again                                     | Page loads in the newly selected valid theme                           |

## Final Expected Result

- Corrupted or invalid theme value in localStorage does not crash the application
- The theme provider falls back to system default when encountering an invalid value
- After one valid toggle cycle, the localStorage is overwritten with a correct value
- No flash of unstyled content (FOUC) or visible error state
