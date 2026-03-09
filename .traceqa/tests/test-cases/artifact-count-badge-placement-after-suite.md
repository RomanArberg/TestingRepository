---
id: TC-562
title: Test case list — artifact count paperclip badge appears after suite name not after title
status: active
priority: low
type: acceptance
automation_status: planned
tags: [test-cases, artifacts, list-view, ui, TRA-1031]
files:
  - web/src/components/test-cases/test-case-list-item.tsx
---

## Preconditions

- User is logged in with workspace access
- The workspace has test cases where:
  - At least one test case belongs to a suite (e.g., `cli/import`) AND has uploaded artifacts
  - At least one test case has NO suite but has uploaded artifacts

## Steps

| #   | Action                                                                                     | Expected Result                                                                                                                                 |
| --- | ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Navigate to the test case list page                                                        | Test case list loads with rows visible                                                                                                          |
| 2   | Locate a test case that belongs to a suite (e.g., `cli/import`) and has uploaded artifacts | The title row shows: test case title → suite name below the title → paperclip icon + count appears on the suite name line, after the suite name |
| 3   | Verify the layout: suite name line contains the paperclip badge                            | The artifact count `🖇 N` badge is positioned at the end of the suite name line, NOT inline after the test case title text                      |
| 4   | Locate a test case with no suite that has uploaded artifacts                               | The artifact count badge appears inline after the test case title (no suite line exists, so badge stays with the title)                         |
| 5   | Locate a test case with a suite but no uploaded artifacts                                  | Suite name is shown normally; no paperclip badge appears                                                                                        |
| 6   | Locate a test case with no suite and no artifacts                                          | Only the title text is shown; no suite line and no paperclip badge                                                                              |

## Final Expected Result

- For test cases with a suite: the artifact count badge (`🖇 N`) appears at the end of the suite name line, not adjacent to the title text
- For test cases without a suite: the artifact count badge remains inline after the title (no suite line to attach to)
- The visual hierarchy is: title (bold) on line 1, then suite path + artifact count on line 2 (muted text)
- This change prevents the badge from visually interrupting the test case title when a suite is present

> **Note (TRA-1031):** Current code places the paperclip badge inside the title flex container, before the suite name div. After the fix, the badge should move to the suite name div (shown after the suite text). This TC should fail on unfixed code and pass after TRA-1031 is implemented.
