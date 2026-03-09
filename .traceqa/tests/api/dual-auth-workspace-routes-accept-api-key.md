---
id: TC-587
title: API — All workspace routes accept API key Bearer token (dual auth)
status: active
priority: critical
type: acceptance
automation_status: planned
tags: [api, auth, dual-auth, api-key, security, workspaces]
files:
  - web/src/app/api/workspaces/route.ts
  - web/src/app/api/workspaces/[id]/route.ts
  - web/src/app/api/workspaces/[id]/cycles/route.ts
  - web/src/app/api/workspaces/[id]/test-cases/route.ts
  - web/src/app/api/workspaces/[id]/results/route.ts
  - web/src/lib/auth.ts
---

## Preconditions

- A valid API key (`TRACEQA_API_KEY`) is issued for organization `org-123` with owner role
- A valid API key (`TRACEQA_MEMBER_API_KEY`) is issued for organization `org-123` with member role
- A workspace `ws-abc` belongs to a project in `org-123`
- A second workspace `ws-xyz` belongs to a different organization

## Steps

| #   | Action                                                                                                          | Expected Result                                                      |
| --- | --------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| 1   | Send `GET /api/workspaces` with `Authorization: Bearer $TRACEQA_API_KEY`                                        | HTTP 200; returns workspaces scoped to org-123 only                  |
| 2   | Send `GET /api/workspaces/ws-abc` with `Authorization: Bearer $TRACEQA_API_KEY`                                 | HTTP 200; returns workspace detail                                   |
| 3   | Send `GET /api/workspaces/ws-xyz` with `Authorization: Bearer $TRACEQA_API_KEY` (different org)                 | HTTP 404; workspace from another org is not accessible with this key |
| 4   | Send `GET /api/workspaces/ws-abc/cycles` with `Authorization: Bearer $TRACEQA_API_KEY`                          | HTTP 200; cycles returned                                            |
| 5   | Send `GET /api/workspaces/ws-abc/test-cases` with `Authorization: Bearer $TRACEQA_API_KEY`                      | HTTP 200; test cases returned                                        |
| 6   | Send `GET /api/workspaces/ws-abc/results` with `Authorization: Bearer $TRACEQA_API_KEY`                         | HTTP 200; results returned                                           |
| 7   | Send `PATCH /api/workspaces/ws-abc` with API key and `{ "name": "New Name" }`                                   | HTTP 200; workspace name updated                                     |
| 8   | Send `GET /api/workspaces/ws-abc` with valid session cookie (cookie auth still works)                           | HTTP 200; cookie auth continues to function alongside API key auth   |
| 9   | Send any workspace route with `Authorization: Bearer invalid-key`                                               | HTTP 401; `{ "error": "Invalid API key" }` or equivalent             |
| 10  | Send `DELETE /api/workspaces/ws-abc` with `Authorization: Bearer $TRACEQA_MEMBER_API_KEY` and valid confirmName | HTTP 403; DELETE requires owner role                                 |
| 11  | Send `DELETE /api/workspaces/ws-abc` with owner API key and `{ "confirmName": "New Name" }`                     | HTTP 204; workspace deleted                                          |

## Technical Verification

```bash
# Test API key auth on multiple routes
curl -s -o /dev/null -w "%{http_code}" \
  -H "Authorization: Bearer $TRACEQA_API_KEY" \
  $BASE_URL/api/workspaces

curl -s -o /dev/null -w "%{http_code}" \
  -H "Authorization: Bearer $TRACEQA_API_KEY" \
  -X DELETE -d '{"confirmName":"New Name"}' \
  $BASE_URL/api/workspaces/$WORKSPACE_ID
```

## Final Expected Result

- All covered workspace API routes accept either cookie session auth or API key Bearer auth
- API key auth is organization-scoped: a key from org A cannot access workspaces of org B
- DELETE endpoint requires owner role via API key (member-role keys get 403)
- PATCH and DELETE operations work with API key auth when role requirements are met
- Requests authenticated by API key return only organization-allowed resources
- Cookie (session) auth continues to work unchanged — dual auth is additive, not breaking
