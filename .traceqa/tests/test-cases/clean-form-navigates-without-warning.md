---
id: TC-183
title: Unsaved changes — clean form navigates without warning
status: active
priority: medium
type: acceptance
automation_status: manual
files:
  - web/src/components/test-cases/test-case-editor-form.tsx
tags: [test-cases, unsaved-changes, navigation]
---

## Preconditions

- User is logged in with workspace access
- User is on the test case editor page
- User has NOT made any changes (isDirty = false)

## Steps

| #   | Action                                   | Expected Result                                               |
| --- | ---------------------------------------- | ------------------------------------------------------------- |
| 1   | Load the page without making any changes | Form state is clean (not dirty), no unsaved changes indicator |
| 2   | Click a sidebar navigation link          | User navigates immediately, no confirmation dialog            |
| 3   | Navigate back to the original page       | Page loads normally                                           |
| 4   | Attempt to close the browser tab         | Tab closes immediately, no confirmation dialog                |
| 5   | Re-open the page and press F5 to refresh | Page refreshes immediately, no confirmation dialog            |

## Final Expected Result

- No warning dialogs appear when form has no unsaved changes
- Navigation (both programmatic and browser-level) proceeds immediately
- User experience is not interrupted when there's nothing to lose
- beforeunload event handler is not triggered when form is clean
