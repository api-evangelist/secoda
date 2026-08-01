---
name: Document data assets in Secoda
description: Find tables in the Secoda catalog and enrich them with descriptions and tags.
api: https://docs.secoda.co/api/reference
method: generated
source: https://docs.secoda.co/api/reference/tables
operations:
  - 'GET /api/v1/table/tables'
  - 'GET /api/v1/table/tables/{table_id}'
  - 'PATCH /api/v1/table/tables/{table_id}'
  - 'GET /api/v1/tag'
---

# Document data assets in Secoda

Use this to keep the Secoda catalog well-documented by adding descriptions and
tags to tables.

## Auth
All requests send `Authorization: Bearer <API_KEY>`. Generate a key in workspace
Settings > API. Use the base host for your region (`api.secoda.co` US,
`eapi.secoda.co` EU, `aapi.secoda.co` APAC).

## Conventions
- Pagination: list responses return `{ links, meta, count, total_pages }`.
  Follow `links.next` until null.
- Write rate limit: 30 calls/min on POST/PUT/PATCH — back off on HTTP 429.
- If a request fails unexpectedly, append a trailing slash to the path.

## Steps
1. `GET /api/v1/table/tables` — list tables (paginate via `links.next`). Note the
   `(deprecated)` marker; prefer the v2 equivalent where available.
2. `GET /api/v1/table/tables/{table_id}` — fetch the table to inspect current
   description and metadata.
3. `PATCH /api/v1/table/tables/{table_id}` — update the description (and other
   editable metadata fields).
4. Attach tags via the Tags resource (`GET /api/v1/tag` to resolve tag ids).

## Errors
- 400 invalid body, 404 unknown table id, 429 rate limited, 500 server error.
