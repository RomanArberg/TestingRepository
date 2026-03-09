---
id: TC-141
title: Result detail — displays correct StatusBadge for each execution status
status: active
priority: high
type: acceptance
automation_status: planned
tags: [results, detail-view, status-badge, visual-redesign]
files:
  [
    web/src/components/results/result-detail-content.tsx,
    web/src/components/command-center/status-badge.tsx,
  ]
---

## Preconditions

- User is logged in with workspace access
- Results exist for each execution status: passed, failed, blocked, skipped, in_progress

## Steps

| #   | Action                                        | Expected Result                                                        |
| --- | --------------------------------------------- | ---------------------------------------------------------------------- |
| 1   | Open a passed result detail                   | StatusBadge shows "Passed" in green                                    |
| 2   | Open a failed result detail                   | StatusBadge shows "Failed" in red                                      |
| 3   | Open a blocked result detail                  | StatusBadge shows "Blocked" in amber                                   |
| 4   | Open a skipped result detail                  | StatusBadge shows "Skipped" in gray                                    |
| 5   | Open an in-progress result detail             | StatusBadge shows "In Progress" with pulse animation                   |
| 6   | Observe the metadata section                  | Metadata panel displays with consistent border styling                 |
| 7   | Observe the assignee name                     | Formatted from email (e.g., "alice.smith@example.com" → "Alice Smith") |
| 8   | Observe the reassignment section (if present) | Divider separates reassignment info from main metadata                 |

## Final Expected Result

- StatusBadge component used throughout result detail view
- In-progress status maps to "active" badge variant with custom label "In Progress" and pulse animation
- Metadata section styled as a panel with consistent border styling
- All status-to-badge mappings are correct
- Reassignment section visually separated from main metadata
