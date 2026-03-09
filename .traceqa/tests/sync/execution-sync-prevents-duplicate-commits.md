---
id: TC-389
title: Execution sync — prevents duplicate commits via syncing_at lock
status: active
priority: critical
type: regression
automation_status: manual
tags: [sync, execution-results, concurrency, data-integrity]
files: [web/src/lib/sync/execution-sync.ts, web/src/lib/sync/session-buffer.ts]
---

## Preconditions

- User A and User B share workspace 'acme-corp'
- Both have pending execution results in session buffers for the same cycle
- GitHub repository is configured and accessible

## Steps

| #   | Action                                                 | Expected Result                              |
| --- | ------------------------------------------------------ | -------------------------------------------- |
| 1   | User A triggers execution result sync                  | Sync starts, sets syncing_at on buffer rows  |
| 2   | User B triggers execution result sync within 2 seconds | Sync starts for User B's buffer              |
| 3   | Verify User A's buffer rows have syncing_at set        | Lock timestamp prevents re-processing        |
| 4   | Verify User B's buffer rows process independently      | Each user's buffer has independent lock      |
| 5   | Wait for both syncs to complete                        | Both succeed with separate commits           |
| 6   | Check GitHub traceqa-results branch                    | Two distinct commits, one per user's results |
| 7   | Verify no duplicate result files                       | Each result file appears exactly once        |

## Final Expected Result

- Row-level syncing_at lock prevents the same buffer from being synced twice
- Concurrent syncs for different users process independently
- Each sync creates a separate atomic commit
- No duplicate or missing result files in the repository
