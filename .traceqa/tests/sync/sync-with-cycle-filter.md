---
id: TC-176
title: Execution sync — filters results by cycle when specified
status: active
priority: medium
type: acceptance
automation_status: manual
files:
  - 'web/src/lib/sync/execution-sync.ts'
  - 'web/src/app/api/workspaces/[id]/sync/route.ts'
tags: [sync, cycles, filtering]
---

## Preconditions

- User is logged in with workspace access
- Workspace has GitHub repository configured
- User has results for multiple cycles (Cycle-1, Cycle-2, Cycle-3)
- At least 3 results per cycle in session buffer

## Steps

| #   | Action                                | Expected Result                                           |
| --- | ------------------------------------- | --------------------------------------------------------- |
| 1   | Open sync dialog                      | Shows all pending results grouped by cycle                |
| 2   | Select "Sync specific cycle" option   | Cycle dropdown appears                                    |
| 3   | Select "Cycle-2" from dropdown        | Preview shows only Cycle-2 results                        |
| 4   | Confirm sync with cycle filter        | Sync starts for Cycle-2 only                              |
| 5   | Wait for completion                   | Success: "3 results from Cycle-2 synced"                  |
| 6   | Check GitHub `traceqa-results` branch | Only Cycle-2 results added to `.traceqa/results/cycle-2/` |
| 7   | Check session buffer                  | Cycle-1 and Cycle-3 results still pending                 |

## Final Expected Result

- Cycle filter correctly limits sync to selected cycle
- Results are organized in cycle-specific directories
- Other cycles' results remain in buffer for later sync
- File paths follow pattern: `.traceqa/results/{cycle-id}/{assignee}/{test-case}.json`
