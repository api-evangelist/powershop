---
name: Look up Powershop energy plans (CDR Generic Tariff)
description: >-
  Retrieve and filter Powershop's 482 published Australian retail electricity and
  gas plans, then pull full tariff detail for one plan. Entirely anonymous — no
  API key, no registration, no accreditation.
api: openapi/powershop-cdr-energy-api-openapi.json
operations: [listEnergyPlans, getEnergyPlanDetail]
generated: '2026-07-27'
method: generated
---

# Look up Powershop energy plans

Powershop publishes no developer portal and issues no API keys. Its retail plan
data is nonetheless completely open, because the Consumer Data Right requires it
— and under the energy designation the **Australian Energy Regulator**, not the
retailer, is the data holder for generic tariff data. So the plans live on the
regulator's Energy Made Easy CDR host, namespaced by brand.

## Base URL

```
https://cdr.energymadeeasy.gov.au/powershop/cds-au/v1
```

## Authentication

None. Do not send an Authorization header — there is no key to send. The one
mandatory header is the CDS version header.

| Header | Required | Value |
|---|---|---|
| `x-v` | yes | `1` for `listEnergyPlans`, `3` for `getEnergyPlanDetail` |
| `x-min-v` | no | lowest acceptable endpoint version |

Omitting `x-v` returns `400` with
`urn:au-cds:error:cds-all:Header/Missing`. Sending a version above the maximum
returns `406` with `urn:au-cds:error:cds-all:Header/UnsupportedVersion` — the
live host reports `max=1` for the plan list.

## Step 1 — list plans (`listEnergyPlans`)

```
GET /energy/plans?fuelType=ELECTRICITY&effective=CURRENT&page=1&page-size=100
x-v: 1
```

Useful filters, all optional:

- `type` — `STANDING` | `MARKET` | `REGULATED` | `ALL` (default `ALL`)
- `fuelType` — `ELECTRICITY` | `GAS` | `DUAL` | `ALL` (default `ALL`)
- `effective` — `CURRENT` | `FUTURE` | `ALL` (default `CURRENT`)
- `updated-since` — delta polling; only plans changed after this date-time
- `brand`
- `page`, `page-size` (default 25)

The response is the CDS envelope: `data.plans[]`, `links`, `meta`. Page with
`meta.totalRecords` / `meta.totalPages` and follow `links.next` until absent.
On 2026-07-27 the full set was **482 plans**.

Each plan carries `planId`, `displayName`, `type`, `fuelType`, `customerType`,
`brandName`, `effectiveFrom` / `effectiveTo`, `lastUpdated`, `applicationUri`,
and a `geography` block with `distributors` and `includedPostcodes`. Use
`geography.distributors` to work out where a plan is actually available —
Ausgrid, Endeavour and Essential Energy for NSW; Citipower, Powercor, United
Energy, AusNet and Jemena/Multinet for Victoria; Energex for south-east
Queensland; SA Power Networks and Australian Gas Networks for South Australia.

## Step 2 — get plan detail (`getEnergyPlanDetail`)

```
GET /energy/plans/{planId}
x-v: 3
```

URL-encode the `planId` — Powershop plan IDs contain an `@`, e.g.
`PSH1060421MRE2@EME` becomes `PSH1060421MRE2%40EME`.

Detail adds `electricityContract` and/or `gasContract`, each with
`tariffPeriod[]` (single rate, time-of-use, demand charges, banded daily supply
charges), `solarFeedInTariff`, `discounts`, `incentives`, `greenPowerCharges`,
`controlledLoad`, `eligibility`, `fees`, `termType`, `benefitPeriod`,
`coolingOffDays` and `billFrequency`, plus `meteringCharges`.

An unknown `planId` returns `404`
`urn:au-cds:error:cds-all:Resource/NotFound`.

## Rules

- Amounts are `AmountString` — string-encoded decimals. Parse as decimal, never
  as float.
- Dates are ISO 8601 `DateString` / `DateTimeString`.
- Do not compare a MARKET plan's headline rate to a STANDING offer without also
  reading `discounts` and `eligibility`; conditional discounts are common.
- Poll with `updated-since` rather than re-fetching the full 482-plan set.
- Correlate requests with `x-fapi-interaction-id`; the host echoes one back.
- This surface is retail tariff data only. It is not wholesale, grid or system
  data — Powershop is a retailer and owns no network or generation assets.

## Related

- `conventions/powershop-conventions.yml` — versioning, pagination, envelope
- `errors/powershop-problem-types.yml` — the full error catalogue
- `data-model/powershop-data-model.yml` — the plan entity graph
