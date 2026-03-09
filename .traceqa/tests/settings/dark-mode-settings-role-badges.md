---
id: TC-157
title: Dark mode — team role badges maintain readability
status: active
priority: medium
type: regression
automation_status: manual
tags: [settings, dark-mode, team, color-tokens]
files:
  [web/src/components/settings/team-members-list.tsx, web/src/components/layout/theme-toggle.tsx]
---

## Preconditions

- User is logged in with workspace access
- Team settings page is accessible with members in different roles (owner, admin, member)
- Application is set to dark mode

## Steps

| #   | Action                               | Expected Result                                           |
| --- | ------------------------------------ | --------------------------------------------------------- |
| 1   | Navigate to Settings → Team          | Team settings page loads with member list                 |
| 2   | Toggle to dark mode (if not already) | UI switches to dark theme                                 |
| 3   | Check owner badge (purple)           | Badge maintains readability with purple tint in dark mode |
| 4   | Check admin badge (blue)             | Badge maintains readability with blue tint in dark mode   |
| 5   | Check member badge (muted)           | Badge uses muted colors that adapt to dark theme          |

## Final Expected Result

- All role badges maintain readability in dark mode
- Badge colors adapt to the dark theme without losing distinction
- Member badge uses theme-aware muted colors
