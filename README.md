# Kolide

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
