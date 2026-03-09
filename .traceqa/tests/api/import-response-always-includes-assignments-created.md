---
id: TC-565
title: Import API — assignmentsCreated is always present in the response (never omitted)
status: active
priority: low
type: regression
automation_status: planned
tags: [import, api, json-response, TRA-998]
files:
  - web/src/app/api/workspaces/[id]/import-results/route.ts
---

## Preconditions

- User is authenticated with a valid API key
- Workspace is accessible

## Steps

| #   | Action                                                                                      | Expected Result                                                                                |
| --- | ------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| 1   | POST `import-results` where all test cases are already assigned to the cycle                | Response contains `"assignmentsCreated": 0` — the field is present with value `0`, not omitted |
| 2   | POST `import-results` where one new test case is assigned for the first time                | Response contains `"assignmentsCreated": 1`                                                    |
| 3   | POST `import-results` with a dry-run (`dryRun: true`)                                       | Response still includes `"assignmentsCreated": 0` (no actual assignments in dry-run mode)      |
| 4   | POST `import-results` where cycle is auto-created (new cycle) with 3 new assignments        | Response contains `"assignmentsCreated": 3` and `"cycleCreated": true`                         |
| 5   | Parse the response with a strict JSON schema that requires `assignmentsCreated` as a number | Schema validation passes — the field is always a `number`, never `undefined`                   |

## Final Expected Result

- `assignmentsCreated` is always a number in the import API response (`0` when no new assignments were made)
- The field is never conditionally omitted — CI/CD pipelines can safely read it without optional chaining
- This applies to successful import scenarios: new cycle, existing cycle, dry-run. For validation failures, only error responses are returned
