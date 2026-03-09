---
id: TC-162
title: Settings cards — panel-style layout with design token borders
status: active
priority: high
type: acceptance
automation_status: planned
tags: [settings, cards, visual-redesign, design-tokens]
files:
  [
    web/src/app/(dashboard)/settings/github/page.tsx,
    web/src/components/settings/storage-usage-card.tsx,
    web/src/app/(dashboard)/settings/storage/page.tsx,
  ]
---

## Preconditions

- User is logged in with workspace access
- User has access to settings pages (GitHub, Storage, Workspace Settings)

## Steps

| #   | Action                                  | Expected Result                                                                       |
| --- | --------------------------------------- | ------------------------------------------------------------------------------------- |
| 1   | Navigate to the GitHub Settings page    | Page renders with panel-style cards                                                   |
| 2   | Observe the "GitHub App" card           | Uses panel layout with rounded corners, design token border, and shadow               |
| 3   | Observe the card title                  | Uses panel-title color with small font size, semibold weight, and wide letter spacing |
| 4   | Navigate to the Storage Settings page   | Storage usage card uses same panel styling                                            |
| 5   | Navigate to the Workspace Settings page | "Git Configuration" card uses panel styling                                           |
| 6   | Observe card inner dividers             | Inner borders use design token border color                                           |
| 7   | Navigate to Storage with no workspaces  | "No Workspaces" empty state uses panel styling                                        |

## Final Expected Result

- All settings cards use plain divs with design tokens instead of generic Card components
- Card titles use panel-title token color with wide letter spacing
- Shadows and borders use design tokens consistently
- Inner content dividers use the border token
