---
id: TC-308
title: API — rejects path traversal in suite path
status: active
priority: critical
type: acceptance
automation_status: planned
tags: [test-cases, api, security, path-traversal, negative]
files:
  - web/src/app/api/workspaces/[id]/test-cases/route.ts
---

## Preconditions

- TraceQA API is running
- User is authenticated and authorized for workspace
- API includes `validateSuitePath()` security check
- Suite paths must be safe relative paths within workspace

## Steps

| Step | Action                                                        | Expected Result                                                                      |
| ---- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| 1    | Send POST request with `suite: "../../../etc"`                | Response status code is 400 Bad Request with error about invalid suite path          |
| 2    | Send POST request with `suite: "/absolute/path"`              | Response status code is 400 Bad Request (absolute paths rejected)                    |
| 3    | Send POST request with suite path containing null byte (`\0`) | Response status code is 400 Bad Request (null bytes rejected)                        |
| 4    | Send POST request with `suite: "valid\\path"`                 | Response status code is 400 Bad Request (backslashes rejected, forward slashes only) |
| 5    | Send POST request with `suite: "valid/relative/path"`         | Request succeeds (valid suite path)                                                  |

## Final Expected Result

All path traversal attempts and unsafe path patterns are rejected with 400 status code. The API prevents directory traversal attacks, absolute path access, null byte injection, and Windows-style paths. Only safe relative paths within the workspace are accepted.
