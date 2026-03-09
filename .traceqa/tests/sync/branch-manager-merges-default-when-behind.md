---
id: TC-391
title: Branch manager — merges default branch into results branch when behind
status: active
priority: high
type: acceptance
automation_status: manual
tags: [sync, branch-management, merge]
files: [web/src/lib/sync/branch-manager.ts]
---

## Preconditions

- Workspace has GitHub repository configured
- traceqa-results branch exists but is 3 commits behind default branch
- Default branch has new test case definitions added since last sync

## Steps

| #   | Action                                       | Expected Result                                         |
| --- | -------------------------------------------- | ------------------------------------------------------- |
| 1   | Trigger execution result sync                | BranchManager.ensureResultsBranch() checks divergence   |
| 2   | Observe branch status before sync            | traceqa-results is behind by 3 commits                  |
| 3   | Wait for sync to complete                    | Sync merges default into results branch before writing  |
| 4   | Check GitHub traceqa-results branch history  | Shows merge commit bringing in default branch changes   |
| 5   | Verify new test case definitions available   | Files from default branch now present in results branch |
| 6   | Verify execution results written after merge | New result files committed on top of merge              |

## Final Expected Result

- Results branch is kept up to date with default branch automatically
- Merge happens before writing new results to prevent conflicts
- Response includes branchMerged: true flag
- No manual branch maintenance required
