---
id: TC-595
title: Settings > GitHub — "Configure repository access" link opens correct GitHub installation page
status: active
priority: high
type: acceptance
automation_status: planned
tags: [settings, github, repository-access, accessibility, ui]
files:
  - web/src/app/(dashboard)/settings/github/page.tsx
---

## Preconditions

- User is logged in to TraceQA
- At least two GitHub App installations are connected:
  - One for a **personal** account (e.g. `octocat`, installation ID `111`)
  - One for an **organisation** account (e.g. `acme-corp`, installation ID `222`)
- User navigates to **Settings > GitHub**

## Steps

| #   | Action                                                                                 | Expected Result                                                                                                                          |
| --- | -------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Navigate to `/settings/github`                                                         | GitHub Integration page loads; connected installations list is visible                                                                   |
| 2   | Observe each installation row                                                          | Each row shows a "Configure repository access" link (not just one shared link at the bottom)                                             |
| 3   | Hover over the "Configure repository access" link for the **personal** account row     | Link href is `https://github.com/settings/installations/111` (personal account pattern)                                                  |
| 4   | Click the "Configure repository access" link for the personal account                  | Opens `https://github.com/settings/installations/111` in a **new tab** (`target="_blank"`)                                               |
| 5   | Hover over the "Configure repository access" link for the **organisation** account row | Link href is `https://github.com/organizations/acme-corp/settings/installations/222` (org pattern with org login in path)                |
| 6   | Click the "Configure repository access" link for the organisation                      | Opens `https://github.com/organizations/acme-corp/settings/installations/222` in a **new tab**                                           |
| 7   | Inspect the link's `aria-label` attribute                                              | `aria-label` includes the account name, e.g. `"Configure repository access for acme-corp"` (screen-reader accessible)                    |
| 8   | Observe the helper text below the installations list                                   | Text reads: `"Can't see your repositories? Configure repository access for the relevant account above."`                                 |
| 9   | Connect a second organisation installation and reload the page                         | New installation row appears with its own correctly scoped "Configure repository access" link using the correct organisation URL pattern |

## Final Expected Result

- Every connected GitHub installation has its own "Configure repository access" link
- Personal account installations link to `/settings/installations/{id}`
- Organisation account installations link to `/organizations/{login}/settings/installations/{id}`
- All links open in a new browser tab
- Each link carries an `aria-label` naming the specific account for screen-reader accessibility
- Helper text below the list guides users who cannot see their repositories
