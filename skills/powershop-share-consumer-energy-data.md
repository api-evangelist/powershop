---
name: Share Powershop consumer energy data as an accredited data recipient
description: >-
  The consented half of Powershop's CDR obligation — accounts, balances,
  invoices, billing, payment schedules, concessions, service points, metering
  usage and DER (solar) register data. Requires ACCC accreditation, CDR
  Register-issued mutual-TLS certificates and an explicit consumer consent.
api: openapi/powershop-cdr-energy-api-openapi.json
operations:
  - getCustomer
  - getCustomerDetail
  - listEnergyAccounts
  - getEnergyAccountDetail
  - getEnergyAccountBalance
  - listEnergyAccountBalancesBulk
  - listEnergyAccountBalancesSpecificAccounts
  - getEnergyAccountInvoices
  - listEnergyAccountInvoicesBulk
  - listEnergyInvoicesForSpecificAccounts
  - getBillingForEnergyAccount
  - listEnergyAccountBillingBulk
  - listEnergyAccountBillingForSpecificAccounts
  - getEnergyAccountPaymentSchedule
  - getEnergyAccountConcessions
  - listElectricityServicePoints
  - getElectricityServicePointDetail
  - getElectricityServicePointUsage
  - listElectricityUsageBulk
  - listElectricityUsageForServicePoints
  - getElectricityDERForServicePoint
  - listElectricityDERBulk
  - listElectricityDERForSpecificServicePoints
generated: '2026-07-27'
method: generated
---

# Share Powershop consumer energy data

Read this before writing any code: **you cannot call these operations without
ACCC accreditation.** There is no API key, no sandbox, no partner tier and no
commercial path around it. Powershop issues no credential of any kind. This
skill describes the operations and the gate honestly so an agent stops rather
than fabricating an integration that cannot exist.

## The gate

To reach any operation below you must:

1. Be an ACCC **accredited data recipient**, or operate as the authorised
   representative or CDR representative of one.
2. Be listed on the **CDR Register** with a registered software product.
3. Hold CDR Register-issued **mutual-TLS** transport certificates and signing
   certificates.
4. Hold a live, scoped, time-bounded **consumer consent** for each account.

The authenticated base URI is **not published anonymously** — it is resolved
through the CDR Register. Do not guess a host.

## The consumer flow

Per Powershop's own CDR policy: the consumer starts in your app and selects
Powershop; they are redirected to Powershop; Powershop verifies identity with a
**one-time password sent to the email address on the account**; the consumer
then selects which accounts, which data clusters and how long to share for.
Consents are managed by the consumer at
`https://dashboard.cdr.powershop.com.au/`.

Security profile: OAuth 2.0 / OpenID Connect under the CDS security profile —
FAPI hardening, PAR, JARM and mutual-TLS sender-constrained tokens. Powershop
does **not** expose OpenID Provider metadata anonymously; there is no
`/.well-known/openid-configuration` to read.

## Scopes → operations

| Scope | Operations |
|---|---|
| `common:customer.basic:read` | `getCustomer` |
| `common:customer.detail:read` | `getCustomerDetail` |
| `energy:accounts.basic:read` | `listEnergyAccounts` |
| `energy:accounts.detail:read` | `getEnergyAccountDetail` |
| `energy:accounts.paymentschedule:read` | `getEnergyAccountPaymentSchedule` |
| `energy:accounts.concessions:read` | `getEnergyAccountConcessions` |
| `energy:billing:read` | `getEnergyAccountBalance`, `listEnergyAccountBalancesBulk`, `listEnergyAccountBalancesSpecificAccounts`, `getEnergyAccountInvoices`, `listEnergyAccountInvoicesBulk`, `listEnergyInvoicesForSpecificAccounts`, `getBillingForEnergyAccount`, `listEnergyAccountBillingBulk`, `listEnergyAccountBillingForSpecificAccounts` |
| `energy:electricity.servicepoints.basic:read` | `listElectricityServicePoints` |
| `energy:electricity.servicepoints.detail:read` | `getElectricityServicePointDetail` |
| `energy:electricity.usage:read` | `getElectricityServicePointUsage`, `listElectricityUsageBulk`, `listElectricityUsageForServicePoints` |
| `energy:electricity.der:read` | `getElectricityDERForServicePoint`, `listElectricityDERBulk`, `listElectricityDERForSpecificServicePoints` |

Ask only for the clusters you will use. Every extra scope is an extra thing the
consumer must agree to on the Powershop consent screen.

## Happy path

1. `getStatus` on the public base URI — do not start if the holder is down.
2. `listEnergyAccounts` (`x-v: 2`) — returns `accountId`, `accountNumber`,
   `displayName`, `openStatus`, `creationDate`, and per plan the
   `servicePointIds`.
3. `getEnergyAccountDetail` (`x-v: 4`) for the plan detail behind an account.
4. `getEnergyAccountBalance` / `getEnergyAccountInvoices` (`x-v: 1`) or
   `getBillingForEnergyAccount` (`x-v: 3`) for money movement.
5. `getElectricityServicePointUsage` (`x-v: 1`) with `oldest-date`,
   `newest-date` and `interval-reads` (`NONE` | `MIN_30` | `FULL`) for metering
   data.
6. `getElectricityDERForServicePoint` (`x-v: 1`) for the solar/inverter/battery
   register.

For many accounts at once, prefer the bulk operations. The `…Bulk` GETs sweep
everything under the consent; the POST variants
(`listEnergyAccountBalancesSpecificAccounts`,
`listEnergyInvoicesForSpecificAccounts`,
`listEnergyAccountBillingForSpecificAccounts`,
`listElectricityUsageForServicePoints`,
`listElectricityDERForSpecificServicePoints`) take a list of IDs in the request
body. These POSTs are **queries, not writes** — they create and mutate nothing,
so there is no idempotency key and retrying is safe.

## Rules

- `x-v` is mandatory on every call; each endpoint has its own current version
  (see `lifecycle/powershop-lifecycle.yml`).
- Send `x-fapi-interaction-id` (an RFC 4122 UUID) and log the one played back;
  also send `x-fapi-auth-date` and `x-fapi-customer-ip-address` when the
  customer is present.
- Paginate with `page` / `page-size`; read `meta.totalRecords` and
  `meta.totalPages`, follow `links.next`.
- Handle `404 Invalid Energy Account` / `Unavailable Energy Account` and the
  service-point equivalents as *consent scope* problems, not bugs — the ID is
  simply not covered by this consent.
- A `422 Invalid Page` means the page is out of range; a `406 Unsupported
  Version` means back off the `x-v`.
- Metering, NMI standing and DER data originate from **AEMO** as secondary data
  holder. Freshness and gaps are AEMO's, not Powershop's.
- Respect the CDS non-functional requirements and traffic thresholds; the AER
  host advertises `Retry-After`, so honour it on a 429.
- Everything you retrieve is CDR data under the OAIC privacy safeguards. Delete
  or de-identify it when the consent ends.

## Related

- `authentication/powershop-authentication.yml` — the full auth profile
- `scopes/powershop-scopes.yml` — every scope with the data it unlocks
- `data-model/powershop-data-model.yml` — the consented entity graph
- `errors/powershop-problem-types.yml` — the error catalogue
