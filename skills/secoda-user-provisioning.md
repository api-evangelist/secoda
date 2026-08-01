---
name: Provision and manage Secoda users
description: Create, list, update, and deactivate workspace users via the Secoda API.
api: https://docs.secoda.co/api/reference
method: generated
source: https://docs.secoda.co/api/reference/users
operations:
  - 'GET /api/v1/user'
  - 'POST /api/v1/user'
  - 'GET /api/v1/user/{id}'
  - 'PATCH /api/v1/user/{id}'
  - 'DELETE /api/v1/user/{id}'
---

# Provision and manage Secoda users

Automate workspace membership: onboard, update, and offboard users.

## Auth
Send `Authorization: Bearer <API_KEY>` (a workspace key grants the same access as
its creating user, so use an Admin key for user management).

## Conventions
- Pagination: `GET /api/v1/user` returns `{ links, meta, count, total_pages }`.
- Write rate limit: 30 calls/min on POST/PATCH — back off on 429.

## Steps
1. `GET /api/v1/user` — list existing users; reconcile against your source of truth.
2. `POST /api/v1/user` — create a user with `first_name`, `last_name`, `email`,
   and `role` (Admin | Editor | Viewer | Guest). For `role: Guest`, `teams` is
   mandatory; `user_groups` is optional.
3. `PATCH /api/v1/user/{id}` — update `first_name` / `last_name`.
4. `DELETE /api/v1/user/{id}` — remove a user (returns 204 No Content).

## Errors
- 400 invalid body, 404 unknown user id, 429 rate limited, 500 server error.
