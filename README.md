# Powershop (powershop)

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

Powershop is an Australian retail energy brand selling electricity in New South Wales, Victoria, south-east Queensland and South Australia, and gas in New South Wales and Victoria. It is operated by Powershop Australia Pty Ltd (ABN 41 154 914 075), a wholly owned Shell Energy Australia business since Shell completed its acquisition from Meridian Energy in February 2022. Powershop publishes no first-party developer portal and no self-serve API — its entire API surface is the Consumer Data Right, which it has actually implemented and not merely claimed.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/powershop/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/powershop/refs/heads/main/apis.yml)

## Tags

- Energy
- Australia
- Utilities
- Electricity
- Gas
- Consumer Data Right
- Energy Retail
- Smart Metering
- Solar
- Tariffs
- Open Data

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## Mandate Posture

- **Regime:** Consumer Data Right (CDR), energy sector — the same statutory machinery (Treasury designation, ACCC, OAIC, Data Standards Body) that produced Australia's banking APIs.
- **Status:** `live-implemented`. Powershop appears in the public ACCC CDR Register energy brand summary (`dataHolderBrandId` `6aaeaf9b-5132-ee11-a83d-000d3a8830d6`, `publicBaseUri` `https://public.cdr.powershop.com.au`, `lastUpdated` 2026-07-27), and that base URI returns live, standards-conformant responses.
- **Standard:** CDR Consumer Data Standards v1.36.0 — CDR Energy API and CDR Common API (OpenAPI 3.0.3).

## APIs

### Powershop CDR Generic Tariff (Energy Plans) API

Public, unauthenticated Consumer Data Right plan data. Under the energy designation the Australian Energy Regulator — not the retailer — holds generic tariff data, so Powershop's plans are served from the AER's Energy Made Easy CDR host. Confirmed 2026-07-27: `GET /cds-au/v1/energy/plans` returned HTTP 200 with 482 plans (416 electricity / 66 gas; 313 MARKET / 169 STANDING; 297 residential / 185 business).

- **Human URL:** [https://cdr.energymadeeasy.gov.au/](https://cdr.energymadeeasy.gov.au/)
- **Base URL:** `https://cdr.energymadeeasy.gov.au/powershop/cds-au/v1`

#### Properties

- [OpenAPI](openapi/powershop-cdr-energy-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/#energy-apis)
- [Documentation](https://www.cdr.gov.au/rollout/cdr-energy-sector)

### Powershop CDR Discovery API

The Consumer Data Standards Discovery endpoints on Powershop's own registered CDR public base URI — the surface that proves the implementation is deployed. Confirmed 2026-07-27, unauthenticated: `/cds-au/v1/discovery/status` HTTP 200 (`status: OK`, "All services operational") and `/cds-au/v1/discovery/outages` HTTP 200 (empty outages array).

- **Human URL:** [https://consumerdatastandardsaustralia.github.io/standards/#common-apis](https://consumerdatastandardsaustralia.github.io/standards/#common-apis)
- **Base URL:** `https://public.cdr.powershop.com.au/cds-au/v1`

#### Properties

- [OpenAPI](openapi/powershop-cdr-common-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/#common-apis)
- [Status](https://public.cdr.powershop.com.au/cds-au/v1/discovery/status)

### Powershop CDR Energy Consumer Data API

The consented, accreditation-gated half of the obligation: customer, account, invoice and billing data plus AEMO-sourced metering, NMI standing and DER register data. Reachable only by an ACCC accredited data recipient holding a valid consumer consent. No anonymous base URI is published.

- **Human URL:** [https://www.powershop.com.au/privacy-policy/cdr-policy](https://www.powershop.com.au/privacy-policy/cdr-policy)

#### Properties

- [OpenAPI](openapi/powershop-cdr-energy-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://www.powershop.com.au/privacy-policy/cdr-policy)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/#energy-apis)
- [Authentication](https://consumerdatastandardsaustralia.github.io/standards/#security-profile)
- [Consent Dashboard](https://dashboard.cdr.powershop.com.au/)

## Common Properties

- [Website](https://www.powershop.com.au/)
- [Privacy Policy](https://www.powershop.com.au/privacy-policy)
- [CDR Policy](https://www.powershop.com.au/privacy-policy/cdr-policy)
- [Shell x Powershop](https://www.powershop.com.au/powershop-and-shell)
- [CDR Register (energy brands)](https://api.cdr.gov.au/cdr-register/v1/energy/data-holders/brands/summary)
- [CDR energy sector rollout](https://www.cdr.gov.au/rollout/cdr-energy-sector)
- [Consumer Data Standards](https://consumerdatastandardsaustralia.github.io/standards/)

## What Is Not Here

Powershop Australia publishes no developer portal, no API keys, and no self-serve documentation. `developer.`, `developers.`, `api.`, `docs.` and `data.powershop.com.au` do not resolve. Powershop stated publicly in 2017 that it had no public API, and that remains true. The `fluxfederation/powershop-api` GitHub repository is the legacy New Zealand Powershop / Flux Federation API, not an Australian Powershop product, and is not listed here.
