---
id: TC-556
title: Result detail — shows total attachment count in metadata section
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [results, detail-view, attachments]
files:
  - web/src/components/results/result-detail-content.tsx
---

## Preconditions

- User is logged in with workspace access
- Execution result exists with steps that have attachments
- User has opened result detail view

## Steps

| #   | Action                                                      | Expected Result                                                          |
| --- | ----------------------------------------------------------- | ------------------------------------------------------------------------ |
| 1   | Open result detail for an execution with step attachments   | Metadata section shows "Attachments" field with paperclip icon and count |
| 2   | Verify the count matches total attachments across all steps | Count equals the sum of attachments from all steps                       |
| 3   | Open result detail for an execution with no attachments     | No "Attachments" field appears in the metadata section                   |

## Final Expected Result

- Attachment count displays in the metadata section when execution has attachments
- Count is omitted when there are no attachments across any steps
- Count accurately reflects the total number of files across all steps
