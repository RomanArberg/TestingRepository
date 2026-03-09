---
id: TC-139
title: Result detail — shows reassignment info when applicable
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [results, detail-view, reassignment]
files: [web/src/components/results/result-detail-content.tsx]
---

## Preconditions

- User is logged in with workspace access
- Execution result exists that was reassigned (has reassignment data)
- User has opened result detail view

## Steps

| #   | Action                                       | Expected Result                                         |
| --- | -------------------------------------------- | ------------------------------------------------------- |
| 1   | Open result detail for a reassigned result   | Detail view opens                                       |
| 2   | Observe metadata section                     | Reassignment section visible with refresh icon          |
| 3   | Observe reassignment details                 | Shows "From:", "To:", "By:" fields with email addresses |
| 4   | If reassignment has reason, observe reason   | "Reason:" field shows the reassignment reason           |
| 5   | Open result detail for non-reassigned result | No reassignment section visible                         |

## Final Expected Result

- Reassignment info only displayed when result was reassigned
- All reassignment fields (from, to, by, reason) display correctly
- Reassignment section has visual separator from main metadata
