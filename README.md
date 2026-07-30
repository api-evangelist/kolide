# Kolide

Kolide is a device trust and endpoint security platform, now part of 1Password Extended
Access Management. It enforces Zero Trust access by blocking non-compliant devices from
authenticating into corporate applications through Okta, Google Workspace or Microsoft
Entra, runs continuous security and compliance checks across Linux, macOS, Windows, iOS
and Android endpoints, and maintains a fleet-wide device inventory built on osquery.

Website: https://kolide.com — Developer docs: https://www.kolide.com/docs/developers

## API

The **Kolide K2 API** at `https://api.kolide.com` — 65 REST operations across 52 paths,
published as OpenAPI 3.0 on two dated version lines (`2026-04-07` current, `2023-05-26`
still supported, pinned with `X-Kolide-Api-Version`). Bearer API key auth (`k2sk_v1_`
prefix); write access is Kolide Max only and granted explicitly per key.

## Artifacts

| Dir | What |
|---|---|
| `openapi/` | Both dated K2 specs, fetched verbatim from kolide.com/docs/openapi |
| `overlays/` | Overlay 1.0.0 of our enhancements over the 2026-04-07 spec |
| `mcp/` | The first-party MCP server (github.com/kolide/device-trust-mcp-server), ~55 real tools |
| `asyncapi/` | Webhook catalog (12 events, HMAC-SHA256) + OpenID SSF/CAEP stream contract |
| `well-known/` | Live `/.well-known/ssf-configuration`; everything else 404 |
| `authentication/` | Bearer key model, token shape, per-key write permissions |
| `conventions/` | Cursor pagination, query grammar, rate limits, versioning |
| `errors/` | Error catalog derived from the spec + docs |
| `lifecycle/` | Dated version policy, status page, changelog links |
| `changelog/` | Structured recent API changelog entries |
| `conformance/` | SSF 1.0, CAEP, RFC 8935/8936, SOC 2, GDPR — and what is not claimed |
| `data-model/` | Entity graph derived from the 44 schemas |
| `packages/` | Registry findings — no first-party API client SDK exists |
| `security/` | Domain security probe, HackerOne VDP, trust posture |
| `skills/` | Four packaged Agent Skills for the marquee flows |
| `llms/` | Generated llms.txt (Kolide publishes none) |

## Notable gaps

No first-party API client SDK in any language; no `security.txt`; no RFC 9457 error
envelope or error-code registry; no idempotency keys; no OAuth/OIDC or scopes; no
published deprecation policy or Sunset headers; no `operationId` on any of the 65
operations; no AsyncAPI document despite two real event surfaces.

Backed by: matrix-partners
