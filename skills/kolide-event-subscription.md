---
name: kolide-event-subscription
description: >-
  Subscribe to Kolide device-trust events — verify HMAC-signed webhooks, or consume the
  OpenID Shared Signals Framework (SSF/CAEP) device-compliance stream by push or poll.
api: Kolide K2 API
base_url: https://api.kolide.com
api_version: '2026-04-07'
generated: '2026-07-19'
method: generated
source: >-
  https://www.kolide.com/docs/developers/webhooks,
  https://www.kolide.com/docs/developers/ssf-streams,
  https://api.kolide.com/.well-known/ssf-configuration
operations:
  - POST /ssf_streams
  - GET /ssf_streams
  - PATCH /ssf_streams
  - DELETE /ssf_streams
  - GET /ssf_streams/status
  - POST /ssf_streams/verify
  - GET /ssf_streams/{stream_id}/events
  - POST /ssf_streams/{stream_id}/events
  - POST /ssf_streams/{id}/rotate_poll_token
---

# Kolide event subscription

Kolide has two event surfaces and **no AsyncAPI document**. The webhook catalog and the
SSF stream contract captured in `asyncapi/kolide-events.yml` are the machine-readable
substitute.

Note: the SSF endpoints below are documented on
https://www.kolide.com/docs/developers/ssf-streams but are **not present in the published
2026-04-07 OpenAPI file** — that spec covers the 52 REST resource paths only.

## Option A — Webhooks

Register an HTTPS endpoint in the UI at **Settings > Developers > Webhooks > Add
Endpoint** (requires a Full Access admin). There is no API to create webhook endpoints.

**Verify every delivery before trusting it:**

- The `Authorization` header carries a **SHA-256 HMAC hex digest of the raw JSON body**,
  signed with that endpoint's unique signing secret: `HMAC-SHA256(request_body, signing_secret)`.
- Compute over the **raw bytes**, not a re-serialised object, and compare in constant time.
- `X-Kolide-Webhook-Identifier` is a static per-endpoint value, useful for WAF rules.
- **Do not allow-list IPs.** Kolide sends from any address in AWS `us-east-1` and reserves
  none; IP-based verification is explicitly documented as unsafe.

Every payload has `event`, `id`, `timestamp` and `data`. Subscribable events:

`audit_log.recorded`, `admin_users.created`, `auth_logs.success`, `auth_logs.failure`,
`devices.created`, `devices.registered`, `devices.destroyed`,
`device_trust.status_changed`, `issues.new`, `issues.resolved`,
`requests.issue_exemption`, `requests.registration`.

Delivery logs are retained **6 months**.

## Option B — SSF / CAEP streams

Kolide is an OpenID **Shared Signals Framework 1.0** transmitter using the **CAEP**
profile. Start from discovery:

```
GET https://api.kolide.com/.well-known/ssf-configuration
```

which returns `issuer`, `jwks_uri` (`https://api.kolide.com/ssf/jwks.json`),
`configuration_endpoint`, `status_endpoint`, `verification_endpoint` and the supported
delivery methods. A verbatim copy is at `well-known/kolide-ssf-configuration.json`.

1. **Create a stream.** `POST /ssf_streams` with a delivery method:
   - push — `urn:ietf:rfc:8935`, requires a public **HTTPS** receiver URL
   - poll — `urn:ietf:rfc:8936`, no URL needed at creation
2. **Events.** Streams are auto-subscribed to
   `https://schemas.openid.net/secevent/caep/event-type/device-compliance-change`, and
   Kolide adds `https://schemas.openid.net/secevent/ssf/event-type/verification` to every
   stream request.
3. **Verify.** `POST /ssf_streams/verify` triggers a verification event so you can prove
   the path end-to-end.
4. **Check health.** `GET /ssf_streams/status`.
5. **Poll and acknowledge.** `GET /ssf_streams/{stream_id}/events` retrieves,
   `POST /ssf_streams/{stream_id}/events` acknowledges. Poll requests authenticate with
   `X-Kolide-Poll-Bearer-Token`, **not** the main `Authorization` key.
6. **Rotate poll tokens.** `POST /ssf_streams/{id}/rotate_poll_token` (added 2026-07-09)
   supports `overlap`, `immediate` and `disable` modes. Use `overlap` for zero-downtime
   rotation.

## Rules

- Validate SET signatures against `jwks_uri` — do not trust an unverified token.
- Push delivery URLs **must be HTTPS**, and private-network destinations are blocked
  (enforced since 2026-05-05). A previously working internal endpoint will now fail.
- Management calls use `Authorization: Bearer $KOLIDE_API_TOKEN` and count against the
  270 req/min limit; polling uses the per-stream token.
- Creating streams is a **write** — 403 without Kolide Max write permission on the key.
- Acknowledge polled events, or you will re-receive them.
