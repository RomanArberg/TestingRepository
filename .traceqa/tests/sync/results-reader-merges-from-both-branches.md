---
id: TC-171
title: Results reader — merges data from results branch and default branch
status: active
priority: medium
type: regression
automation_status: manual
files: [web/src/lib/github/results-reader.ts]
tags: [results-reading, backward-compatibility]
---

## Preconditions

- Workspace has GitHub repository configured
- Legacy results exist in default branch at `.traceqa/results/`
- New results exist in `traceqa-results` branch
- User is viewing test execution history

## Steps

| #   | Action                                 | Expected Result                                                   |
| --- | -------------------------------------- | ----------------------------------------------------------------- |
| 1   | Navigate to Test Cases page            | Page loads successfully                                           |
| 2   | Select a test case with legacy results | Test case details show                                            |
| 3   | Click "Execution History" tab          | History tab opens                                                 |
| 4   | Observe results list                   | Shows BOTH old results (from main) and new (from traceqa-results) |
| 5   | Check result dates                     | Results sorted by date, regardless of source branch               |
| 6   | Click on a legacy result               | Legacy result details display correctly                           |
| 7   | Click on a new result                  | New result details display correctly                              |

## Final Expected Result

- Results from both branches are merged and displayed together
- No duplicate results appear
- Results maintain correct chronological order
- User experience is seamless regardless of result source
