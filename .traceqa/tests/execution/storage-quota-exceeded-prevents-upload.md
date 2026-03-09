---
id: TC-365
title: 'Artifact upload — storage quota exceeded returns 402 error'
status: active
priority: high
type: acceptance
automation_status: planned
tags: [execution, attachments, quota, negative]
files:
  - 'web/src/app/api/workspaces/[id]/artifacts/route.ts'
  - 'web/src/hooks/use-artifact-upload.ts'
  - 'web/src/lib/storage/index.ts'
---

## Preconditions

- User is logged in with workspace access
- Workspace storage usage is near or at the quota limit
- User is on the full-page execution page for a test case with steps
- Note: Both cookie-session and API key (Bearer token) auth paths enforce quota correctly

## Steps

| #   | Action                                           | Expected Result                                              |
| --- | ------------------------------------------------ | ------------------------------------------------------------ |
| 1   | Paste a screenshot onto step 1                   | Thumbnail preview appears with local blob URL                |
| 2   | Trigger sync (Ctrl/Cmd+S or Complete Session)    | Upload attempt begins                                        |
| 3   | Observe the error response                       | Upload fails with quota exceeded error                       |
| 4   | Observe the sync status indicator                | Shows error state — sync was not attempted (atomic behavior) |
| 5   | Observe that the screenshot preview is preserved | Blob URL thumbnail still visible (not lost on error)         |

## Final Expected Result

- Server returns 402 when upload would exceed workspace storage quota
- Presigned URL is not generated when quota is exceeded
- Atomic sync behavior: Git sync is skipped when upload fails
- User receives a clear error about storage quota
- Local preview is preserved so user does not lose their work
