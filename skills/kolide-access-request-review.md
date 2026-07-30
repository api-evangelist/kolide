---
name: kolide-access-request-review
description: >-
  Review and act on Kolide device registration requests and issue exemption requests —
  the human-in-the-loop approval queue that gates device trust.
api: Kolide K2 API
base_url: https://api.kolide.com
api_version: '2026-04-07'
generated: '2026-07-19'
method: generated
source: openapi/kolide-k2-openapi.json, https://www.kolide.com/docs/developers/api
operations:
  - GET /registration_requests
  - GET /registration_requests/{id}
  - PATCH /registration_requests/{id}
  - GET /exemption_requests
  - GET /exemption_requests/{id}
  - PATCH /exemption_requests/{id}
  - PATCH /devices/{deviceId}/authentication_mode
  - DELETE /devices/{deviceId}/registration
  - GET /devices/{id}
---

# Kolide access request review

Two approval queues gate Kolide device trust: **registration requests** (a device asking
to be trusted) and **exemption requests** (a user asking to be excused from a failing
check). Both are read with `GET` and acted on with `PATCH`.

Paths are verbatim from `openapi/kolide-k2-openapi.json`; the spec declares no
`operationId` values, so method + path is the reference.

## Setup

```
Authorization: Bearer $KOLIDE_API_TOKEN
X-Kolide-Api-Version: 2026-04-07
```

Every `PATCH` here is a **write** — the key needs Kolide Max write permission or the call
returns 403.

## Steps

1. **Drain the registration queue.** `GET /registration_requests` lists pending device
   registrations. Each carries `requester_information` and `device_information`
   link-objects. `GET /registration_requests/{id}` fetches one.

2. **Check the requester and the device before deciding.** `GET /devices/{id}` for the
   device's current posture, and `GET /devices/{deviceId}/open_issues` for what is
   currently failing on it. Approving a device with open blocking issues defeats the
   control.

3. **Act on the request.** `PATCH /registration_requests/{id}` updates it. The spec also
   exposes `PUT /registration_requests/{id}` with the same semantics — prefer `PATCH`.

4. **Drain the exemption queue.** `GET /exemption_requests` lists requests to be excused
   from a check; each carries `requester_information`, `device_information` and an
   `issues` collection of link-objects naming exactly which issues the exemption covers.
   `GET /exemption_requests/{id}` fetches one, `PATCH /exemption_requests/{id}` decides it.

5. **Adjust enforcement where needed.** `PATCH /devices/{deviceId}/authentication_mode`
   changes how a device is treated at authentication time. To revoke trust entirely,
   `DELETE /devices/{deviceId}/registration` removes the registration without deleting
   the device record (`DELETE /devices/{id}` does that, and is destructive).

## Rules

- **Destructive operations are unguarded.** `DELETE /devices/{id}` and
  `DELETE /devices/{deviceId}/registration` have no confirmation semantics and no
  idempotency key. Confirm the target id with a `GET` immediately before, and never
  derive a delete target from a stale list page.
- **Cursor pagination** — `per_page` up to 100, follow `pagination.next_cursor` until
  `next` is blank. Approval queues routinely exceed one page.
- **Filter with `query`** rather than paging everything: `:` exact, `~` substring,
  `>` / `<` on datetimes, `AND` / `OR` to combine.
- **403** means the key lacks write permission (Kolide Max, granted per key with a
  documented rationale). **401** means a bad token or a plan that excludes the feature.
- Rate limit 270 req/min; honour `Retry-After` on 429.
- Every action taken here lands in the audit log — `GET /audit_logs` — and fires the
  `requests.registration` / `requests.issue_exemption` webhooks.
