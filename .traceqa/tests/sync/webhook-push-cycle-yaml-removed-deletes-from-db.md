---
id: TC-532
title: Webhook push — cycle YAML removed deletes cycle from database
status: active
priority: high
type: acceptance
automation_status: manual
tags: [sync, webhooks, cycles, yaml]
files:
  - web/src/app/api/github/webhooks/route.ts
  - web/src/lib/github/webhooks.ts
  - web/src/lib/cycles/cycle-sync.ts
---

## Preconditions

- A TraceQA workspace is connected to GitHub repo `acme/qa-repo`, default branch `main`
- The GitHub App is installed with a valid installation ID
- `GITHUB_WEBHOOK_SECRET` is configured in the environment
- A cycle with ID `sprint-41` already exists in the database (previously synced from `.traceqa/cycles/sprint-41.yaml`)
- The file `.traceqa/cycles/sprint-41.yaml` currently exists in the `main` branch of the repo

## Steps

| #   | Action                                                                                                        | Expected Result                                                                           |
| --- | ------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| 1   | Delete the file `.traceqa/cycles/sprint-41.yaml` from the `main` branch of `acme/qa-repo` and push the commit | The file is removed from the repository on `main`                                         |
| 2   | Observe that GitHub delivers a push webhook to the TraceQA webhook endpoint                                   | The webhook endpoint receives the push event with the removed file in `commits[].removed` |
| 3   | Confirm webhook delivery is accepted                                                                          | The webhook endpoint returns HTTP 200 with `{ "status": "accepted" }`                     |
| 4   | Poll the Cycles API or refresh the page every 2–3 seconds for up to 30 seconds                                | The cycle `sprint-41` eventually disappears from the list                                 |
| 5   | Look for a cycle named "Sprint 41" or with ID `sprint-41`                                                     | No cycle with ID `sprint-41` appears in the list                                          |
| 6   | Use the search or filter to confirm `sprint-41` is gone                                                       | Search for "Sprint 41" returns no results                                                 |
| 7   | Query the cycles API directly: `GET /api/workspaces/{id}/cycles` and search for `sprint-41`                   | No record exists for cycle ID `sprint-41` in the API response                             |

## Final Expected Result

- The cycle `sprint-41` is removed from the database
- The cycle no longer appears anywhere in the web UI for that workspace
- The webhook endpoint returns `{ "status": "accepted" }` with HTTP 200
