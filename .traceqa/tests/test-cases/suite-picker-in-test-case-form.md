---
id: TC-187
title: Suite picker — dropdown lists available suites in editor
status: active
priority: high
type: acceptance
automation_status: planned
tags: [test-cases, suite-picker, editor]
files:
  - web/src/components/test-cases/test-case-editor-form.tsx
  - web/src/lib/suites/types.ts
---

## Preconditions

- User is logged in with workspace access
- Workspace has at least one suite created (e.g., "Smoke Tests")
- User has permission to create/edit test cases

## Steps

| #   | Action                              | Expected Result                                                        |
| --- | ----------------------------------- | ---------------------------------------------------------------------- |
| 1   | Navigate to Create Test Case page   | Test case editor form loads with all fields                            |
| 2   | Locate the Suite dropdown field     | Suite picker is visible with placeholder "Select suite..."             |
| 3   | Click the Suite dropdown            | Dropdown opens and lists all available suites in the workspace         |
| 4   | Select a suite from the dropdown    | Selected suite name displays in the dropdown, form updates suite value |
| 5   | Submit the form with suite selected | Test case is created with the selected suite association               |
| 6   | Verify suite association            | Created test case appears in the selected suite's test case list       |

## Final Expected Result

- Suite picker displays all workspace suites in dropdown
- Selected suite is properly associated with the test case
- Suite selection persists after form submission
- Suite picker integrates with form validation
