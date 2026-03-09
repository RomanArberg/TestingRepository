---
id: TC-163
title: Settings sidebar — active link uses brand teal with aria-current
status: active
priority: high
type: acceptance
automation_status: planned
tags: [settings, sidebar, navigation, visual-redesign, accessibility]
files: [web/src/components/settings/settings-sidebar.tsx]
---

## Preconditions

- User is logged in
- User is on a settings page

## Steps

| #   | Action                                | Expected Result                                                  |
| --- | ------------------------------------- | ---------------------------------------------------------------- |
| 1   | Navigate to Settings → Storage page   | Settings sidebar is visible with navigation links                |
| 2   | Observe the active "Storage" link     | Text color is brand teal with tinted background                  |
| 3   | Observe inactive links (Team, GitHub) | Text is muted with no teal tint                                  |
| 4   | Hover over an inactive link           | Background changes to muted; text changes to foreground          |
| 5   | Click "Team" link                     | Navigation occurs; "Team" becomes active with brand teal styling |
| 6   | Click "GitHub" link                   | Navigation occurs; "GitHub" becomes active                       |

## Final Expected Result

- Active sidebar link uses brand teal color with tinted background
- Navigation between settings sections updates the active state
- Accessibility attribute `aria-current="page"` is present on the active link
