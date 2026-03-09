---
id: TC-181
title: Unsaved changes — browser close shows native warning dialog
status: active
priority: high
type: acceptance
automation_status: manual
files:
  - web/src/components/test-cases/test-case-editor-form.tsx
  - web/src/hooks/use-unsaved-changes.ts
tags: [test-cases, unsaved-changes, beforeunload]
---

## Preconditions

- User is logged in with workspace access
- User is on the test case editor page (create or edit mode)
- Test case editor form is loaded and ready for input
- User has made changes to the form (isDirty = true)

## Steps

| #   | Action                                                     | Expected Result                                                        |
| --- | ---------------------------------------------------------- | ---------------------------------------------------------------------- |
| 1   | Make a change to the form (e.g., edit title or add a step) | Form state becomes dirty, unsaved changes indicator appears if present |
| 2   | Attempt to close the browser tab (Ctrl+W or click X)       | Browser shows "Leave site?" confirmation dialog                        |
| 3   | Click "Cancel" or "Stay"                                   | Tab remains open, all changes are preserved in the form                |
| 4   | Attempt to close the tab again                             | Browser shows confirmation dialog again                                |
| 5   | Click "Leave" or confirm                                   | Tab closes, unsaved changes are lost                                   |

## Final Expected Result

- Browser's native "Leave site?" dialog appears when closing tab with unsaved changes
- User can cancel to stay on page and keep their changes
- User can confirm to leave and lose unsaved changes
- beforeunload event handler correctly detects dirty form state
