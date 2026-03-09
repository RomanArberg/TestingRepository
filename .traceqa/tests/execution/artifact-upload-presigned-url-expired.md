---
id: TC-360
title: 'Artifact upload — presigned URL expired before upload completes'
status: active
priority: high
type: regression
automation_status: planned
tags: [execution, attachments, presigned-url, negative]
files:
  - 'web/src/hooks/use-artifact-upload.ts'
  - 'web/src/app/api/workspaces/[id]/artifacts/route.ts'
---

## Preconditions

- User is logged in with workspace access
- User is on the full-page execution page for a test case with steps
- The presigned URL expiration is 15 minutes (900 seconds) per the server configuration
- User has a large screenshot (e.g., 8MB WebP) copied to clipboard

## Steps

| #   | Action                                                                     | Expected Result                                                       |
| --- | -------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| 1   | Click "Add attachment" on step 1, then paste the screenshot                | Thumbnail preview appears with local blob URL (no presigned URL yet)  |
| 2   | Trigger sync (e.g., click "Complete Session") to request presigned URL     | Upload process begins — presigned URL is generated at sync time       |
| 3   | Simulate a scenario where the presigned URL expires before upload finishes | Upload to R2 fails because presigned URL has expired (403 or similar) |
| 4   | Observe the sync status indicator                                          | Shows error state with message about upload failure                   |
| 5   | Observe that user stays on the execution page                              | Navigation is blocked — sync failed atomically                        |
| 6   | Click the error indicator to retry                                         | A new presigned URL is requested and upload succeeds                  |
| 7   | Wait for sync to complete                                                  | Status shows "Saved", user is navigated to My Tasks                   |

## Final Expected Result

- Presigned URLs are generated at sync time (not at paste time) — paste only creates a local blob URL
- Expired presigned URL causes upload failure (R2 returns 403 or similar)
- Atomic sync behavior prevents Git sync when upload fails
- User stays on execution page with error visible
- Retry generates a fresh presigned URL and succeeds
- No data loss — the screenshot preview is preserved during error
- No orphaned artifacts in R2 storage
