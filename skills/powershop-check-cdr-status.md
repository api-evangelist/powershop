---
name: Check Powershop CDR availability before sharing data
description: >-
  Read Powershop's mandated CDS Discovery status and scheduled-outage endpoints
  to decide whether a consumer data-sharing call is worth attempting. Anonymous,
  no credentials, no accreditation.
api: openapi/powershop-cdr-common-api-openapi.json
operations: [getStatus, getOutages]
generated: '2026-07-27'
method: generated
---

# Check Powershop CDR availability

Powershop runs no human status page — `status.powershop.com.au` does not resolve
in DNS. What it does run, because the Consumer Data Standards make it mandatory,
is a machine-readable status surface on its own registered CDR host. For an
accredited data recipient this is the pre-flight check before burning a consent
on a call that was never going to succeed.

## Base URL

```
https://public.cdr.powershop.com.au/cds-au/v1
```

This is the `publicBaseUri` Powershop registers with the ACCC CDR Register
(`dataHolderBrandId` `6aaeaf9b-5132-ee11-a83d-000d3a8830d6`). It carries the
Discovery endpoints and nothing else — `/energy/plans` and `/common/customer`
both return `404` here by design.

## Authentication

None. Send `x-v: 1`. Omitting it returns `400`
`urn:au-cds:error:cds-all:Header/Missing` with detail
`"x-v header is mandatory for CDR endpoint requests"`.

## Step 1 — status (`getStatus`)

```
GET /discovery/status
x-v: 1
```

Live response on 2026-07-27:

```json
{"data":{"status":"OK","updateTime":"2026-07-27T20:25:56.145894714Z","explanation":"All services operational"},"links":{"self":"https://public.cdr.powershop.com.au/cds-au/v1/discovery/status"},"meta":{}}
```

`data.status` is one of `OK`, `PARTIAL_FAILURE`, `UNAVAILABLE`,
`SCHEDULED_OUTAGE`. Treat anything other than `OK` as a reason to defer, and
surface `data.explanation` to the consumer rather than a generic failure.

## Step 2 — scheduled outages (`getOutages`)

```
GET /discovery/outages
x-v: 1
```

Live response on 2026-07-27: `{"data":{"outages":[]},...}` — none scheduled.

Each outage carries `outageTime`, `duration`, `isPartial` and `explanation`.
Use it to schedule bulk consented pulls around planned maintenance instead of
retrying into a window that is already announced.

## Rules

- Poll status before a batch of consented calls, not before every call.
- Cache for minutes, not seconds; `updateTime` tells you how fresh the holder's
  own view is.
- A `SCHEDULED_OUTAGE` is not an error — do not burn retry budget on it, read
  `/discovery/outages` and wait for the published window to pass.
- This endpoint says nothing about Powershop's retail website or app. It is the
  status of the CDR data-sharing implementation only.
- The tariff data on `cdr.energymadeeasy.gov.au` is served by the Australian
  Energy Regulator and has its own availability, unrelated to this status.

## Related

- `lifecycle/powershop-lifecycle.yml` — status, outages and versioning policy
- `authentication/powershop-authentication.yml` — what accreditation actually requires
- `conformance/powershop-conformance.yml` — what was verified and how
