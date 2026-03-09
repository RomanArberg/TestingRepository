---
id: TC-339
title: Status transition — Archived cycle rejects all status changes
status: active
priority: critical
type: acceptance
automation_status: planned
tags: [cycles, status-transition, lifecycle, negative]
files:
  - 'web/src/components/cycles/cycle-header.tsx'
  - 'web/src/app/(dashboard)/workspaces/[slug]/cycles/[cycleId]/edit/page.tsx'
  - 'web/src/app/api/workspaces/[id]/cycles/[cycleId]/route.ts'
---

## Preconditions

- User is authenticated with workspace access
- A cycle named 'Retired Q4 Regression' exists in Archived status
- User is viewing the cycle detail page

## Steps

| #   | Action                                                              | Expected Result                                                           |
| --- | ------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| 1   | Observe the status badge in the cycle header                        | Status badge reads 'Archived' as static text (no dropdown)                |
| 2   | Attempt to click the status badge                                   | No dropdown opens — the badge is not interactive                          |
| 3   | Navigate to the edit page URL directly                              | Browser redirects back to the cycle detail page                           |
| 4   | Send a PATCH request to the cycle API endpoint with status 'active' | API returns 403 Forbidden with message 'Archived cycles cannot be edited' |

## Final Expected Result

- Archived cycles are fully locked — no status changes possible from UI or API
- The status badge is rendered as static text with no click handler
- Direct URL access to the edit page is intercepted and redirected
- The API enforces the archived lock independently of the UI
