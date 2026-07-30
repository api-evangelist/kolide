---
name: kolide-device-compliance-triage
description: >-
  Triage the Kolide device-trust fleet — find failing security checks, identify which
  devices and people are affected, and drive issues to resolution using the Kolide K2 API.
api: Kolide K2 API
base_url: https://api.kolide.com
api_version: '2026-04-07'
generated: '2026-07-19'
method: generated
source: openapi/kolide-k2-openapi.json, https://www.kolide.com/docs/developers/api
operations:
  - GET /checks
  - GET /checks/{id}
  - GET /checks/{checkId}/results
  - GET /issues
  - GET /issues/{id}
  - GET /devices
  - GET /devices/{id}
  - GET /devices/{deviceId}/open_issues
  - POST /devices/{deviceId}/check_refreshes
  - GET /people/{personId}/open_issues
---

# Kolide device compliance triage

The Kolide 2026-04-07 OpenAPI declares **no `operationId` values**, so operations are
referenced by method + path throughout. Every path below is verbatim from
`openapi/kolide-k2-openapi.json`.

## Setup

```
Authorization: Bearer $KOLIDE_API_TOKEN      # k2sk_v1_... key
X-Kolide-Api-Version: 2026-04-07             # optional; omitting it floats to latest
```

Pin the version header. Kolide ships breaking changes as new dated version lines, and an
unpinned client silently moves onto them.

## Steps

1. **List the checks that are failing.** `GET /checks` returns every security check.
   On the 2026-04-07 line each check carries `percent_passing` (integer 0–100), so sort
   ascending on it to find the weakest controls first.

2. **Pull the failures for a check.** `GET /checks/{checkId}/results` returns per-device
   results. Narrow with the `query` parameter using Kolide's grammar —
   `status:"fail"` for exact match, `~` for substring, `>` / `<` for datetimes, combined
   with `AND` / `OR`.

3. **Or start from the issue side.** `GET /issues` lists open compliance issues; each
   issue is a failing check on a specific device and carries `device_information` and
   `check_information` link-objects. `GET /issues/{id}` fetches one.

4. **Scope to a device or a person.** `GET /devices/{deviceId}/open_issues` for one
   device; `GET /people/{personId}/open_issues` for everything a human owns.
   `GET /devices/{id}` and `GET /devices` give device detail — device records carry a
   `registered_owner_info` link-object back to the person.

5. **Force a re-evaluation after remediation.** `POST /devices/{deviceId}/check_refreshes`
   triggers a fresh check run on that device rather than waiting for the next cycle. This
   is a **write** operation — see the permissions note below.

## Rules

- **Pagination is cursor-based.** Send `per_page` (default 25, max 100) and follow
  `pagination.next_cursor` until `next` is blank. Never assume one page is the whole
  fleet — this is the most common triage error.
- **Rate limit is 270 requests/minute.** On 429 back off for `Retry-After`; pace using
  `Ratelimit-Remaining` and `Ratelimit-Reset`. Fanning out per-device calls across a
  large fleet will hit this — prefer list endpoints with `query` filters.
- **Write access is Kolide Max only**, granted explicitly per API key. A key without it
  gets **403 Forbidden** on `POST /devices/{deviceId}/check_refreshes`. A **401** means
  either a bad token or a feature your organization's plan does not include.
- **There are no idempotency keys.** A retried `POST .../check_refreshes` creates another
  refresh. Retry only on connection failure, never blindly on timeout.
- Errors are plain `application/json` with no problem+json envelope and no error codes —
  branch on HTTP status, not on a body field.
