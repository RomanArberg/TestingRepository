---
id: TC-186
title: Priority badges — display design token colors per level
status: active
priority: high
type: acceptance
automation_status: manual
tags: [test-cases, priority-badge, design-system, visual]
files:
  - web/src/components/test-cases/test-case-list-item.tsx
---

## Preconditions

- User is logged in with workspace access
- Test cases exist with all four priority levels: critical, high, medium, low

## Steps

| #   | Action                            | Expected Result                                                                                                           |
| --- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| 1   | Navigate to the Test Case Library | Test case list loads with priority badges visible                                                                         |
| 2   | Observe a critical priority badge | Badge displays in red color (--status-failed token) with 10% background tint and 20% border tint                          |
| 3   | Observe a high priority badge     | Badge displays in amber color (--status-blocked token) with 10% background tint and 20% border tint                       |
| 4   | Observe a medium priority badge   | Badge displays in teal color (--brand-teal token) with 10% background tint and 20% border tint                            |
| 5   | Observe a low priority badge      | Badge displays in gray color (--status-skipped token) with 10% background tint and 20% border tint                        |
| 6   | Inspect any badge element         | Badge has `data-testid="priority-badge"` and `data-priority` attributes with corresponding priority level                 |
| 7   | Inspect badge CSS in dev tools    | Background uses `color-mix()` with 10% opacity, border uses `color-mix()` with 20% opacity, no hardcoded Tailwind classes |

## Final Expected Result

- Each priority level maps to a specific design token color (critical=red, high=amber, medium=teal, low=gray)
- Badges use consistent background and border tints via `color-mix()` CSS function
- All badges have testable attributes (`data-testid` and `data-priority`)
- No hardcoded Tailwind color classes used
