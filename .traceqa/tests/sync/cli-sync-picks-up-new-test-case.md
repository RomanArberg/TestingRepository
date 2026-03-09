---
id: TC-999
title: Manual CLI sync picks up new test cases
status: active
priority: high
type: functional
tags: [cli, sync, smoke-test]
---

## Description
Verify that running `traceqa sync` from the CLI correctly detects and imports test cases that were added directly to the git repository.

## Steps
1. Add a new test case markdown file directly to the `.traceqa/tests/` directory in the repo
2. Push the commit to the main branch
3. Run `traceqa sync --workspace my-workspace`

## Expected Result
The sync command reports the new test case was imported and it appears in the web UI.
