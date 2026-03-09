---
id: TC-305
title: Parser — rejects object and array tags
status: active
priority: medium
type: regression
automation_status: planned
tags: [test-cases, parser, validation, negative, tags]
files:
  - web/src/lib/test-cases/validators.ts
  - web/src/lib/test-cases/parser.ts
---

## Preconditions

- Test case parser module is available
- Tags validation coerces numbers and booleans to strings (valid behavior)
- Tags validation rejects nested objects, arrays, and null values

## Steps

| Step | Action                                                             | Expected Result                                                          |
| ---- | ------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| 1    | Parse test case content with `tags: [{name: "tag"}]`               | ParseError thrown indicating object tags not allowed                     |
| 2    | Parse test case content with `tags: [[1, 2]]`                      | ParseError thrown indicating nested arrays not allowed                   |
| 3    | Parse test case content with `tags: [null]`                        | ParseError thrown indicating null values not allowed                     |
| 4    | Parse test case content with `tags: [42, true, "valid"]`           | Content parsed successfully with tags coerced to ["42", "true", "valid"] |
| 5    | Parse test case content with `tags: ["string-tag", "another-tag"]` | Content parsed successfully with all string tags                         |

## Final Expected Result

Tags containing nested objects, arrays, or null values are rejected with validation errors. Primitive values (numbers, booleans, strings) are accepted and coerced to strings. The parser ensures tags remain simple string arrays suitable for filtering and search.
