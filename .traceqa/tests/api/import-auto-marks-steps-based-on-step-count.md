---
id: TC-576
title: Import — auto-marks test case steps based on step_count metadata
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [import, api, execution, steps, auto-mark]
files:
  - web/src/app/api/workspaces/[id]/import-results/route.ts
  - supabase/migrations/20260303120000_add_step_count_to_metadata.sql
---

## Preconditions

- User is authenticated with a valid API key
- Workspace `traceqa-main` is accessible
- Cycle `sprint-24` exists
- Test case `TC-42` has 3 steps defined (reflected in `test_case_metadata.step_count = 3`)

## Steps

| #   | Action                                                                                                      | Expected Result                                                                                                                                            |
| --- | ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | POST `import-results` with `{ results: [{ testCaseId: "TC-42", status: "passed" }], cycleId: "sprint-24" }` | HTTP 200; import succeeds                                                                                                                                  |
| 2   | Check the execution result stored for `TC-42`                                                               | The RPC call to store the result includes `testCaseStepCount: 3` — allowing the server to auto-generate step results (pass for steps 1-2, pass for step 3) |
| 3   | View the execution panel for `TC-42` in `sprint-24`                                                         | All 3 steps are marked as "passed" (auto-filled based on the import verdict and step count)                                                                |
| 4   | POST `import-results` with `{ results: [{ testCaseId: "TC-42", status: "failed" }], cycleId: "sprint-24" }` | Import succeeds; execution panel shows steps 1 and 2 as "passed", step 3 (last step) as "failed" — matching the standard "fail on last step" pattern       |
| 5   | POST `import-results` for a test case with no `step_count` metadata (step_count = 0)                        | Import succeeds; no steps are auto-marked (no step count available); verdict is stored at the test case level only                                         |

## Final Expected Result

- When importing a test result, the `step_count` field from `test_case_metadata` is read and passed to the RPC function
- The RPC auto-generates step results for all steps based on the overall verdict: for `passed`, all steps are `pass`; for `failed`, all steps except the last are `pass` and the last is `fail`
- Test cases with `step_count = 0` or no metadata are imported without step auto-marking
- Step count metadata is maintained separately from the test case content and does not require re-parsing the test case file
