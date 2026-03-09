---
id: TC-166
title: Theme toggle — cycles light/dark/system with persistence
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [settings, user-menu, theme, dark-mode, accessibility]
files:
  [
    web/src/components/layout/theme-toggle.tsx,
    web/src/components/layout/theme-provider.tsx,
    web/src/components/layout/header.tsx,
  ]
---

## Preconditions

- User is logged in
- User is on any page within the application

## Steps

| #   | Action                                                | Expected Result                                                |
| --- | ----------------------------------------------------- | -------------------------------------------------------------- |
| 1   | Locate the theme toggle in the header (sun/moon icon) | Theme toggle button is visible next to the branch selector     |
| 2   | Click the theme toggle                                | UI immediately switches between light and dark themes          |
| 3   | Refresh the page                                      | Theme preference persists                                      |
| 4   | Open user menu (click avatar in header)               | Dropdown opens showing Profile, Settings, and Sign out options |
| 5   | Click "Settings" from user menu                       | Navigates to /settings page                                    |
| 6   | Toggle theme again                                    | UI switches theme; all settings page elements adapt            |

## Final Expected Result

- Theme toggle is accessible from the header on every page
- Theme changes apply immediately without page refresh
- Theme preference persists across page refreshes and navigation
- Both light and dark themes render all page elements correctly
