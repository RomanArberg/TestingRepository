---
id: TC-529
title: Search input — filters test cases by partial ID match
status: active
priority: high
type: acceptance
automation_status: planned
tags: [test-cases, search, multi-field, id-match]
files:
  - web/src/components/test-cases/test-case-filters.tsx
  - web/src/lib/test-cases/metadata-queries.ts
  - web/src/lib/test-cases/api-types.ts
---

## Preconditions

- User is logged in with workspace access
- Workspace contains test cases with known IDs (e.g., TC-100, TC-101, TC-200)
- Test case list page is loaded with all test cases visible

## Steps

| #   | Action                                     | Expected Result                                               |
| --- | ------------------------------------------ | ------------------------------------------------------------- |
| 1   | Navigate to the Test Cases list page       | Test case list loads with search input visible                |
| 2   | Observe the search input placeholder       | Placeholder reads "Search by ID, title, tags..."              |
| 3   | Type "TC-1" into the search input          | List filters to show only test cases whose ID contains "TC-1" |
| 4   | Verify TC-100 and TC-101 appear in results | Both test cases are visible in the filtered list              |
| 5   | Verify TC-200 does not appear in results   | TC-200 is not shown (ID does not contain "TC-1")              |
| 6   | Clear the search input                     | Full test case list is restored                               |
| 7   | Type "TC-200" into the search input        | List filters to show only TC-200                              |
| 8   | Verify exact single result                 | Exactly one test case is displayed matching the ID            |

## Final Expected Result

- Search input accepts partial TC IDs and filters the list using case-insensitive partial matching
- Results update as the user types (debounced)
- Clearing the search restores the full list
- Search placeholder accurately describes searchable fields
