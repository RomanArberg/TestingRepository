---
id: TC-164
title: Storage error — role=alert attribute for screen reader announcement
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [settings, storage, accessibility, visual-redesign]
files: [web/src/components/settings/storage-usage-card.tsx]
---

## Preconditions

- User is logged in
- Storage usage API returns an error (simulated or actual)

## Steps

| #   | Action                                              | Expected Result                                               |
| --- | --------------------------------------------------- | ------------------------------------------------------------- |
| 1   | Navigate to Settings → Storage with a storage error | Storage usage card renders with error message                 |
| 2   | Observe error message styling                       | Error text uses semantic error color within panel-styled card |
| 3   | Verify screen reader announces the error            | Error text is announced to assistive technology users         |

## Final Expected Result

- Error element has `role="alert"` for accessibility
- Screen readers properly announce the error when it appears
- Error is displayed within the same panel-styled card container
