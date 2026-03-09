---
id: TC-398
title: Results reader — handles corrupt JSON in result files
status: active
priority: medium
type: regression
automation_status: manual
tags: [results, reading, corrupt-data, negative]
files: [web/src/lib/github/results-reader.ts, web/src/lib/results/serializer.ts]
---

## Preconditions

- Workspace has GitHub repository with traceqa-results branch
- Branch contains 5 result files: 3 valid JSON, 1 with truncated JSON, 1 with invalid YAML-like content

## Steps

| #   | Action                   | Expected Result                                               |
| --- | ------------------------ | ------------------------------------------------------------- |
| 1   | Navigate to Results page | Page loads and fetches results                                |
| 2   | Observe results list     | Shows 3 valid results (corrupt files are skipped)             |
| 3   | Verify no error banner   | Page shows results normally without error state               |
| 4   | Open any valid result    | Detail view displays correctly with all metadata and steps    |
| 5   | Check browser console    | Corrupt files logged as parse errors but don't crash the page |

## Final Expected Result

- Corrupt result files are silently skipped during reading
- Valid results from the same directory still load correctly
- No user-facing error for partially corrupt data
- Page remains functional even with some bad files in repository
