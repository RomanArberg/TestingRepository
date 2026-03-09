---
id: TC-173
title: Execution sync — writes to results branch when main is protected
status: active
priority: high
type: acceptance
automation_status: manual
files: [web/src/lib/sync/execution-sync.ts, web/src/lib/sync/branch-manager.ts]
tags: [sync, protected-branch]
---

## Preconditions

- User is logged in with workspace access
- Workspace has GitHub repository with PROTECTED main branch
- Main branch protection includes: require PR reviews, no direct pushes
- User has test execution results to sync

## Steps

| #   | Action                  | Expected Result                                                    |
| --- | ----------------------- | ------------------------------------------------------------------ |
| 1   | Execute a test case     | Result saved to session buffer                                     |
| 2   | Click "Sync" button     | Sync dialog appears                                                |
| 3   | Confirm sync            | Sync starts without errors                                         |
| 4   | Monitor sync progress   | No 422 or 403 errors appear                                        |
| 5   | Wait for completion     | Success message appears                                            |
| 6   | Check GitHub repository | Results written to `traceqa-results` branch, NOT to protected main |
| 7   | Verify main branch      | Main branch unchanged, still protected                             |

## Final Expected Result

- Sync completes successfully despite main branch protection
- Results are written to unprotected `traceqa-results` branch
- No permission errors or branch protection violations occur
- Main branch protection settings remain intact
