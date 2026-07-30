---
name: kolide-fleet-reporting
description: >-
  Answer fleet-inventory and posture questions from Kolide's reporting tables, saved
  report queries, live osquery campaigns and software package inventory.
api: Kolide K2 API
base_url: https://api.kolide.com
api_version: '2026-04-07'
generated: '2026-07-19'
method: generated
source: openapi/kolide-k2-openapi.json, https://www.kolide.com/docs/developers/api
operations:
  - GET /reporting/tables
  - GET /reporting/tables/{name}
  - GET /reporting/tables/{tableName}/table_records
  - GET /reporting/queries
  - GET /reporting/queries/{id}
  - GET /reporting/queries/{queryId}/results
  - GET /packages
  - GET /packages/{id}
  - GET /live_query_campaigns
  - POST /live_query_campaigns
  - GET /live_query_campaigns/{liveQueryCampaignId}/query_results
  - GET /devices
  - GET /people
---

# Kolide fleet reporting

Three ways to ask the fleet a question, in increasing cost: **reporting tables**
(pre-materialised), **saved report queries**, and **live query campaigns** (real osquery
executed on endpoints). Reach for live queries last.

Paths are verbatim from `openapi/kolide-k2-openapi.json`; the spec declares no
`operationId` values.

## Setup

```
Authorization: Bearer $KOLIDE_API_TOKEN
X-Kolide-Api-Version: 2026-04-07
```

## Steps

1. **Discover what is already collected.** `GET /reporting/tables` lists the available
   reporting tables; `GET /reporting/tables/{name}` returns one table's schema. Read the
   schema before querying — column names differ per table.

2. **Read records.** `GET /reporting/tables/{tableName}/table_records` returns rows.
   Filter with `query` (`:` exact, `~` substring, `>` / `<` datetime, `AND` / `OR`)
   instead of pulling everything and filtering client-side.

3. **Use saved queries when one already answers the question.**
   `GET /reporting/queries` lists them, `GET /reporting/queries/{id}` describes one, and
   `GET /reporting/queries/{queryId}/results` fetches results.

   **Breaking change to know:** on the `2026-04-07` line, reporting query responses no
   longer embed a `results` field — results come only from the separate results endpoint.
   Code written against `2023-05-26` that reads `results` inline will break when pinned
   forward.

4. **Software inventory.** `GET /packages` and `GET /packages/{id}` cover installed
   software across the fleet.

5. **Live osquery, only when nothing above answers it.**
   `POST /live_query_campaigns` starts a campaign (a **write** — Kolide Max key required),
   `GET /live_query_campaigns` and `GET /live_query_campaigns/{id}` track it, and
   `GET /live_query_campaigns/{liveQueryCampaignId}/query_results` collects results, each
   carrying a `device_information` link-object. `DELETE /live_query_campaigns/{id}` stops
   and removes one.

6. **Join to owners.** Results reference devices; `GET /devices/{id}` gives
   `registered_owner_info` and `GET /people/{personId}/registered_devices` goes the other
   way. There is no `expand`/`include` parameter — resolving owners means a second call
   per device, so batch it against `GET /people` rather than fanning out.

## Rules

- **Cursor pagination everywhere.** `per_page` default 25, max 100; follow
  `pagination.next_cursor` until `next` is blank. Reporting tables are the largest
  collections in the API — a single page is never the answer to a fleet-wide question.
- **Rate limit 270 req/min.** Per-device fan-out will exhaust it. Prefer one filtered list
  call over N detail calls; honour `Retry-After` on 429.
- **Live query campaigns cost endpoint CPU.** They execute on real user machines. Scope
  them tightly and delete campaigns you are finished with.
- **No idempotency keys** — a retried `POST /live_query_campaigns` starts a second
  campaign against the fleet. Retry only on connection failure.
- `GET /custom_check_drafts` exists on the `2026-04-07` line only; it is absent from
  `2023-05-26`.
- 403 on any write means the key lacks Kolide Max write permission.
