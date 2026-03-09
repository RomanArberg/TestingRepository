---
id: TC-295
title: Parser — case-insensitive heading matching
status: active
priority: medium
type: regression
automation_status: planned
tags: [test-cases, parser, headings, case-sensitivity]
files:
  - web/src/lib/test-cases/parser.ts
---

## Preconditions

- Parser module is available at `web/src/lib/test-cases/parser.ts`
- Parser implements case-insensitive heading matching logic

## Steps

| Step | Action                                                                 | Expected Result                                         |
| ---- | ---------------------------------------------------------------------- | ------------------------------------------------------- |
| 1    | Create test case content with `## PRECONDITIONS` in all caps           | Content prepared with uppercase heading                 |
| 2    | Parse the test case content                                            | Parse completes successfully                            |
| 3    | Verify preconditions array is populated correctly                      | Preconditions data is extracted despite case difference |
| 4    | Create test case content with `## preconditions` in all lowercase      | Content prepared with lowercase heading                 |
| 5    | Parse the test case content                                            | Parse completes successfully                            |
| 6    | Verify preconditions array is populated correctly                      | Preconditions data is extracted despite case difference |
| 7    | Create test case content with `## steps` in lowercase                  | Content prepared with lowercase heading                 |
| 8    | Parse the test case content                                            | Steps table is parsed correctly                         |
| 9    | Create test case content with `## FINAL EXPECTED RESULT` in all caps   | Content prepared with uppercase heading                 |
| 10   | Parse the test case content                                            | Final expected result is extracted correctly            |
| 11   | Create test case content with `## Final Expected Result` in mixed case | Content prepared with mixed case heading                |
| 12   | Parse the test case content                                            | Final expected result is extracted correctly            |

## Final Expected Result

Section headings are recognized regardless of case (uppercase, lowercase, mixed case), and all content is extracted correctly for PRECONDITIONS, STEPS, and FINAL EXPECTED RESULT sections.
