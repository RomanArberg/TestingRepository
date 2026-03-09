---
id: TC-282
title: Workspace settings — three sections visible and functional
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [workspaces, settings, navigation]
files:
  - web/src/app/(dashboard)/workspaces/[slug]/settings/page.tsx
  - web/src/components/workspaces/workspace-settings-form.tsx
  - web/src/components/workspaces/workspace-name-form.tsx
  - web/src/app/(dashboard)/workspaces/[slug]/settings/danger-zone-section.tsx
---

## Preconditions

- User is logged in with workspace access
- Workspace "Performance Suite" has GitHub connected with default branch "main"
- User is on any workspace page

## Steps

| #   | Action                                    | Expected Result                                                   |
| --- | ----------------------------------------- | ----------------------------------------------------------------- |
| 1   | Navigate to `/workspaces/{slug}/settings` | Settings page loads with General, Repository, and Danger Zone     |
| 2   | Observe General section                   | Shows Workspace Name input, Slug (read-only), and Created date    |
| 3   | Observe Repository section                | Shows connected repo, last synced, Default Branch input, and Save |
| 4   | Observe Danger Zone section               | Red-bordered section with Delete button                           |
| 5   | Change Default Branch to "release/v2.1"   | Field updates, Save button becomes enabled                        |
| 6   | Click "Save"                              | Button shows "Saving...", then success message appears            |
| 7   | Navigate away to Test Cases tab           | Test Cases page loads                                             |
| 8   | Navigate back to Settings                 | Default Branch field shows "release/v2.1" (persisted)             |

## Final Expected Result

- Settings page displays three distinct sections (General, Repository, Danger Zone)
- Default branch value persists across navigation
- Save button state correctly reflects unsaved changes
