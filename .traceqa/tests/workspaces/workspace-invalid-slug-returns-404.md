---
id: TC-279
title: Workspace page — 404 for non-existent workspace slug
status: active
priority: high
type: acceptance
automation_status: planned
tags: [workspaces, navigation, error-handling, negative]
files:
  - web/src/app/(dashboard)/workspaces/[slug]/layout.tsx
  - web/src/app/(dashboard)/workspaces/[slug]/page.tsx
---

## Preconditions

- User is logged in as an organization member

## Steps

| #   | Action                                                        | Expected Result                              |
| --- | ------------------------------------------------------------- | -------------------------------------------- |
| 1   | Navigate directly to `/workspaces/nonexistent-workspace-slug` | Browser shows a 404 Not Found page           |
| 2   | Navigate directly to `/workspaces/`                           | Browser handles gracefully (404 or redirect) |
| 3   | Navigate directly to `/workspaces/DROP TABLE workspaces`      | Browser shows 404, no SQL injection          |
| 4   | Navigate directly to `/workspaces/<script>alert(1)</script>`  | Browser shows 404, no XSS execution          |

## Final Expected Result

- Non-existent workspace slugs return a clear 404 page
- Malicious slug inputs are safely handled without injection
- No server errors or sensitive data are exposed
