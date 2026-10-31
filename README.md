# Powershop

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

Powershop is an Australian retail energy brand selling electricity in New South Wales, Victoria, south-east Queensland and South Australia, and gas in New South Wales and Victoria. It is operated by Powershop Australia Pty Ltd (ABN 41 154 914 075), a wholly owned Shell Energy Australia business since Shell completed its acquisition from Meridian Energy in February 2022. Powershop sits at the retail end of the energy value chain — it buys wholesale, bills the customer, and owns the customer relationship — and is known for its "Powerpacks" prepay purchasing model, GreenPower add-on, and EV Day/EV Night plans. Its API posture is entirely regulatory, not commercial: Powershop publishes NO first-party developer portal, no API keys, and no self-serve documentation, and has publicly said since 2017 that it has no public API. What it does have is a verified Consumer Data Right (CDR) energy implementation. Powershop is a designated CDR energy data holder listed live on the ACCC CDR Register with a public base URI of https://public.cdr.powershop.com.au, which returns standards-conformant Consumer Data Standards responses for /cds-au/v1/discovery/status and /cds-au/v1/discovery/outages without authentication. Its Generic Tariff (plan) data is served openly and anonymously from the Australian Energy Regulator's Energy Made Easy CDR host, where 482 Powershop electricity and gas plans are retrievable with no credentials at all. The customer-level data the mandate actually exists to unlock — accounts, billing, invoices, payment schedules, concessions, plus AEMO-sourced metering, NMI standing and DER register data — is real, documented, and reachable only by an accredited data recipient acting on an authenticated consumer consent. Open tariff data, closed consumer data: a mandate that was implemented, not merely claimed.

**Areas:** Energy · Australia · Utilities · Electricity · Gas · Consumer Data Right · Energy Retail · Smart Metering · Solar · Tariffs · Open Data

## Powershop on APIs.io

Everything profiled for Powershop is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/powershop/](https://apis.io/providers/powershop/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [Powershop Data Holder Customers API](https://apis.io/apis/powershop/powershop-data-holder-customers-api/) — Data Holder Customer endpoints
- [Powershop Data Holder Operations API](https://apis.io/apis/powershop/powershop-data-holder-operations-api/) — Data Holder Operations endpoints
- [Powershop Distributed Energy Resources API](https://apis.io/apis/powershop/powershop-distributed-energy-resources-api/) — Distributed Energy Resource endpoints
- [Powershop Electricity Service Points API](https://apis.io/apis/powershop/powershop-electricity-service-points-api/) — Electricity Service Point endpoints
- [Powershop Electricity Usage API](https://apis.io/apis/powershop/powershop-electricity-usage-api/) — Electricity Usage endpoints
- [Powershop Energy Account Balances API](https://apis.io/apis/powershop/powershop-energy-account-balances-api/) — Energy Account Balance endpoints
- [Powershop Energy Account Billing API](https://apis.io/apis/powershop/powershop-energy-account-billing-api/) — Energy Account Billing endpoints
- [Powershop Energy Accounts API](https://apis.io/apis/powershop/powershop-energy-accounts-api/) — Energy Account endpoints
- [Powershop Energy Plans API](https://apis.io/apis/powershop/powershop-energy-plans-api/) — Energy Plan endpoints

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [powershop](https://apis.io/servers/powershop/powershop/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Powershop Agentic Access](https://apis.io/agentic-access/powershop/powershop-agentic-access/)

#### Collections (2)

Postman and Open Collection request collections.

- [CDR Common API](https://apis.io/collections/powershop/open-powershop-cdr-common-api/)
- [CDR Energy API](https://apis.io/collections/powershop/open-powershop-cdr-energy-api/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Powershop Cdr Common Api Overlay](https://apis.io/overlays/powershop/powershop-cdr-common-api-overlay/)
- [Powershop Cdr Energy Api Overlay](https://apis.io/overlays/powershop/powershop-cdr-energy-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Powershop Authentication](https://apis.io/security/powershop/powershop-authentication/)
- [Powershop Domain Security](https://apis.io/security/powershop/powershop-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Powershop Scopes](https://apis.io/scopes/powershop/powershop-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.powershop.com.au/)
- [Documentation](https://www.powershop.com.au/privacy-policy/cdr-policy)
- [API reference](https://consumerdatastandardsaustralia.github.io/standards/#energy-apis)
- [Pricing](https://www.powershop.com.au/energy-rates-and-prices)
- [Sign up](https://www.powershop.com.au/sign-up)
- [Support](https://www.powershop.com.au/help-centre)
- [Blog](https://www.powershop.com.au/energy-insights)
- [Terms of service](https://www.powershop.com.au/terms-and-conditions)
- [Privacy policy](https://www.powershop.com.au/privacy-policy)
- [Status](https://public.cdr.powershop.com.au/cds-au/v1/discovery/status)

## API Evangelist rating

**Kin Score 43.0** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 66.1 |
| Contract quality | 44.7 |
| Contract governance | 18.2 |
| Operational transparency | 31.6 |
| Developer ergonomics | 37.5 |
| Access clarity | 44.7 |

**Agent readiness 25.5** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 34.4** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/powershop/](https://apis.io/providers/powershop/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Powershop: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/powershop/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
