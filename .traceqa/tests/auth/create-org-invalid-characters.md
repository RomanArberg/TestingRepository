---
id: TC-246
title: Create organization — rejects name with invalid characters
status: active
priority: medium
type: acceptance
automation_status: planned
tags: [auth, onboarding, org-creation, validation]
files:
  - web/src/components/onboarding/create-org-form.tsx
  - web/src/app/api/organizations/route.ts
---

## Preconditions

- User is logged in via GitHub OAuth
- User has no organization
- User is on the onboarding page (`/onboarding`)

## Steps

| #   | Action                                                 | Expected Result                                                                                                    |
| --- | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| 1   | Type '<script>alert("xss")</script>' in the name input | Input accepts the text                                                                                             |
| 2   | Click outside the input field (trigger blur)           | Validation error: "Organization name can only contain letters, numbers, spaces, hyphens, apostrophes, and periods" |
| 3   | Clear and type '@@Hacker Corp!!'                       | Input accepts the text                                                                                             |
| 4   | Click outside the input field                          | Same validation error appears                                                                                      |
| 5   | Clear and type "Valid-Name's Inc."                     | Input accepts the text                                                                                             |
| 6   | Click outside the input field                          | No validation error (hyphens, apostrophes, and periods are allowed)                                                |

## Final Expected Result

- Names with HTML tags, special symbols (`@`, `!`, `<`, `>`), or script content are rejected
- Allowed special characters: hyphens (`-`), apostrophes (`'`), periods (`.`), spaces
- Validation prevents XSS payloads from reaching the server
