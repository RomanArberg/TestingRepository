---
id: TC-149
title: Step card — displays comment text when present
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [results, detail-view, steps, comments]
files: [web/src/components/results/result-step-card.tsx]
---

## Preconditions

- User is logged in with workspace access
- Execution result exists with at least one step that has a comment
- User has opened result detail view

## Steps

| #   | Action                            | Expected Result                                             |
| --- | --------------------------------- | ----------------------------------------------------------- |
| 1   | Locate step card with comment     | Step card is visible in steps list                          |
| 2   | Observe comment section           | Comment icon (message square) appears below expected result |
| 3   | Observe comment text              | Comment text is displayed in muted color next to icon       |
| 4   | Compare with step without comment | Steps without comments do not show comment section          |

## Final Expected Result

- Comments are displayed only when present
- Comment icon provides visual indicator
- Comment text is readable and properly formatted
