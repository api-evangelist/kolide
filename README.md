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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Kolide is a device trust and endpoint security platform, now part of 1Password Extended Access Management. It enforces Zero Trust access by blocking non-compliant devices from authenticating into corporate applications through Okta, Google Workspace or Microsoft Entra, runs continuous security and compliance checks across Linux, macOS, Windows, iOS and Android endpoints, and maintains fleet-wide device inventory built on thousands of osquery-sourced data points. Its distinguishing philosophy is user-first remediation: rather than silently denying access, Kolide educates the end user about the specific problem on their device and guides them through fixing it themselves, cutting helpdesk load. The public developer surface is the K2 API at api.kolide.com — 65 REST operations across devices, people, groups, security checks, compliance issues, live osquery campaigns, approval queues, reporting tables and audit logs — published as OpenAPI 3.0 on dated version lines, with HMAC-signed webhooks, an OpenID Shared Signals Framework (CAEP) event stream, and a first-party MCP server.

**Areas:** Company · B2B · Security · Device Trust · Endpoint Security · Zero Trust · Compliance · Identity · osquery · Device Management

## Kolide on APIs.io

Everything profiled for Kolide is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/kolide/](https://apis.io/providers/kolide/)** — or go straight to one of the APIs or properties below.

### APIs (17)

- [Kolide Admin Users API](https://apis.io/apis/kolide/kolide-admin-users-api/) — The Admin Users API from Kolide — 2 operation(s) for admin users.
- [Kolide Audit Logs API](https://apis.io/apis/kolide/kolide-audit-logs-api/) — The Audit Logs API from Kolide — 2 operation(s) for audit logs.
- [Kolide Auth Logs API](https://apis.io/apis/kolide/kolide-auth-logs-api/) — The Auth Logs API from Kolide — 2 operation(s) for auth logs.
- [Kolide Checks API](https://apis.io/apis/kolide/kolide-checks-api/) — The Checks API from Kolide — 5 operation(s) for checks.
- [Kolide Custom Check Drafts API](https://apis.io/apis/kolide/kolide-custom-check-drafts-api/) — The Custom Check Drafts API from Kolide — 2 operation(s) for custom check drafts.
- [Kolide Deprovisioned People API](https://apis.io/apis/kolide/kolide-deprovisioned-people-api/) — The Deprovisioned People API from Kolide — 1 operation(s) for deprovisioned people.
- [Kolide Device Groups API](https://apis.io/apis/kolide/kolide-device-groups-api/) — The Device Groups API from Kolide — 5 operation(s) for device groups.
- [Kolide Devices API](https://apis.io/apis/kolide/kolide-devices-api/) — The Devices API from Kolide — 7 operation(s) for devices.
- [Kolide Exemption Requests API](https://apis.io/apis/kolide/kolide-exemption-requests-api/) — The Exemption Requests API from Kolide — 2 operation(s) for exemption requests.
- [Kolide Issues API](https://apis.io/apis/kolide/kolide-issues-api/) — The Issues API from Kolide — 2 operation(s) for issues.
- [Kolide Live Query Campaigns API](https://apis.io/apis/kolide/kolide-live-query-campaigns-api/) — The Live Query Campaigns API from Kolide — 3 operation(s) for live query campaigns.
- [Kolide Packages API](https://apis.io/apis/kolide/kolide-packages-api/) — The Packages API from Kolide — 2 operation(s) for packages.
- [Kolide People API](https://apis.io/apis/kolide/kolide-people-api/) — The People API from Kolide — 5 operation(s) for people.
- [Kolide Person Groups API](https://apis.io/apis/kolide/kolide-person-groups-api/) — The Person Groups API from Kolide — 3 operation(s) for person groups.
- [Kolide Registration Requests API](https://apis.io/apis/kolide/kolide-registration-requests-api/) — The Registration Requests API from Kolide — 2 operation(s) for registration requests.
- [Kolide Reporting API](https://apis.io/apis/kolide/kolide-reporting-api/) — The Reporting API from Kolide — 6 operation(s) for reporting.
- [Kolide Whoami API](https://apis.io/apis/kolide/kolide-whoami-api/) — The Whoami API from Kolide — 1 operation(s) for whoami.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Kolide Events](https://apis.io/asyncapis/kolide/kolide-events/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [1Password Device Trust (Kolide K2) MCP Server](https://apis.io/servers/kolide/kolide/)

#### Collections (17)

Postman and Open Collection request collections.

- [K2 Admin Users API](https://apis.io/collections/kolide/open-kolide-admin-users-api/)
- [K2 Admin Users Audit Logs API](https://apis.io/collections/kolide/open-kolide-audit-logs-api/)
- [K2 Admin Users Auth Logs API](https://apis.io/collections/kolide/open-kolide-auth-logs-api/)
- [K2 Admin Users Checks API](https://apis.io/collections/kolide/open-kolide-checks-api/)
- [K2 Admin Users Custom Check Drafts API](https://apis.io/collections/kolide/open-kolide-custom-check-drafts-api/)
- [K2 Admin Users Deprovisioned People API](https://apis.io/collections/kolide/open-kolide-deprovisioned-people-api/)
- [K2 Admin Users Device Groups API](https://apis.io/collections/kolide/open-kolide-device-groups-api/)
- [K2 Admin Users Devices API](https://apis.io/collections/kolide/open-kolide-devices-api/)
- [K2 Admin Users Exemption Requests API](https://apis.io/collections/kolide/open-kolide-exemption-requests-api/)
- [K2 Admin Users Issues API](https://apis.io/collections/kolide/open-kolide-issues-api/)
- [K2 Admin Users Live Query Campaigns API](https://apis.io/collections/kolide/open-kolide-live-query-campaigns-api/)
- [K2 Admin Users Packages API](https://apis.io/collections/kolide/open-kolide-packages-api/)
- [K2 Admin Users People API](https://apis.io/collections/kolide/open-kolide-people-api/)
- [K2 Admin Users Person Groups API](https://apis.io/collections/kolide/open-kolide-person-groups-api/)
- [K2 Admin Users Registration Requests API](https://apis.io/collections/kolide/open-kolide-registration-requests-api/)
- [K2 Admin Users Reporting API](https://apis.io/collections/kolide/open-kolide-reporting-api/)
- [K2 Admin Users Whoami API](https://apis.io/collections/kolide/open-kolide-whoami-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Kolide K2 Overlay](https://apis.io/overlays/kolide/kolide-k2-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Kolide Authentication](https://apis.io/security/kolide/kolide-authentication/)
- [Kolide Domain Security](https://apis.io/security/kolide/kolide-domain-security/)
- [Kolide Trust Center](https://apis.io/security/kolide/kolide-trust-center/)
- [Kolide Vulnerability Disclosure](https://apis.io/security/kolide/kolide-vulnerability-disclosure/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://kolide.com)
- [Documentation](https://www.kolide.com/docs)
- [Getting started](https://www.kolide.com/docs/developers/usecases)
- [API reference](https://kolideapi.readme.io/reference)
- [Pricing](https://www.kolide.com/pricing)
- [Sign up](https://app.kolide.com/signin)
- [Support](https://www.kolide.com/docs/about-kolide/support)
- [Blog](https://www.kolide.com/blog)
- [Terms of service](https://www.kolide.com/legal/terms)
- [Privacy policy](https://www.kolide.com/legal/privacy)
- [GitHub](https://github.com/kolide)
- [Status](https://status.1password.com)

## API Evangelist rating

**Kin Score 56.5** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 57.7 |
| Contract governance | 18.2 |
| Operational transparency | 52.6 |
| Developer ergonomics | 56.5 |
| Access clarity | 60.5 |

**Agent readiness 28.4** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | — |

**Regulatory alignment 35.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/kolide/](https://apis.io/providers/kolide/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Kolide: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/kolide/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
