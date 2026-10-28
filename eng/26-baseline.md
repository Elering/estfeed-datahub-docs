# Baseline

> [!WARNING]
> **DRAFT.** This document describes the first phase of the baseline functionality. The API contracts —
> in particular the search parameters and the response layout — may still change before go-live.

## Table of contents

- [Introduction](#introduction)
- [Key concepts](#key-concepts)
- [Submission deadline and time rules](#submission-deadline-and-time-rules)
- [Transmitting baseline data](#transmitting-baseline-data)
  - [API message](#api-message)
  - [Web interface and Excel import](#web-interface-and-excel-import)
- [Checking the processing status](#checking-the-processing-status)
- [Requesting baseline data](#requesting-baseline-data)
- [Requesting resource data](#requesting-resource-data)
- [Corrections after the deadline and missing baselines](#corrections-after-the-deadline-and-missing-baselines)

## Introduction

Baseline is the **Balancing Service Provider's** (hereinafter referred to as the Aggregator) forecast of a metering point's consumption or
production for a 15-minute settlement period in the situation where no balancing energy activation takes
place. It describes the expected normal energy behavior of the metering point and creates the reference
level against which the accuracy of the forecast and the actual delivery of declared aFRR and mFRR
balancing energy are later assessed.

The Aggregator chooses its own forecasting method and is responsible for the accuracy of the submitted baseline.

In the first phase, Estfeed Datahub accepts baseline submissions, stores them, and makes them available
for querying together with metered quantities. Accuracy assessment and validation of declared deliveries
follow in later phases.

The public consultation materials for the Baseline Methodology are available on the Elering website (in Estonian): https://www.elering.ee/konsultatsioon/baasjoone-metoodika-avalik-konsultatsioon

> [!NOTE]
> Baseline functionality applies to **electricity** only.

## Key concepts

| Term | Explanation |
| --- | --- |
| Resource | A prequalified balancing resource, identified by a **resource EIC**. A resource groups one or more grid metering points. Resources are registered and maintained by Elering. |
| Grid metering point | The (grid) metering point for which the baseline is submitted. A grid metering point is the parent of one or more aggregation metering points. |
| Aggregation metering point | The metering point registered by the aggregator under a grid metering point. The resource EIC is declared on the aggregation metering point's characteristics. |
| Settlement period | A 15-minute period, identified by its **UTC start time**. Market period, activation period and settlement period all refer to the same 15-minute window. |
| Baseline right | An Aggregator may submit and query baselines for a grid metering point exactly when it holds a valid aggregation agreement on an aggregation metering point whose parent is that grid metering point. |

**Baseline is submitted per grid metering point**, as two separate values per settlement period:

| Direction | Meaning |
| --- | --- |
| Consumption baseline (`outQty`) | Forecast consumption of the grid metering point, kWh |
| Production baseline (`inQty`) | Forecast production of the grid metering point, kWh |


> [!IMPORTANT]
> "IN/OUT" is used for two unrelated things in the balancing documentation, and they can point in
> opposite directions for the same event:
>
> - **Energy directions** (grid perspective) — in the baseline submission, `inQty` is energy fed *into*
>   the grid (production forecast) and `outQty` energy taken *out of* the grid (consumption forecast).
> - **Regulation directions** (system perspective) — for declared aFRR/mFRR deliveries, IN =
>   up-regulation (consume less or produce more) and OUT = down-regulation (consume more or produce
>   less).
>
> Example: when consumption is *reduced*, the delivery is **IN** (up-regulation), but its effect appears
> in the **consumption** (`outQty`) energy column. This document always states which meaning applies.

## Submission deadline and time rules

It is recommended to submit an initial baseline well in advance and subsequently provide baseline refinements or updates. This helps ensure that no gaps remain in the baseline data.

> [!WARNING]
> The settlement period baseline must be received by Estfeed Datahub no **later than 30 minutes before the start of the settlement period (UTC)**. Therefore, it is recommended to submit the baseline with a sufficient time margin.

```
deadline(P) = period start (UTC) − 30 minutes
```

A submission received at or before the deadline is considered valid for that settlement period. Because settlement periods
start on quarter-hour boundaries, this means: if the time of transmission is 10:07, the earliest period
that can still be covered starts at **10:45** (its deadline 10:15 is still ahead; the 10:30 period's
deadline 10:00 has already passed).

- Baseline may be submitted up to **32 days** ahead of the period (configurable ceiling).
- Until the deadline, the Aggregator may freely correct or replace the baseline. The valid baseline is the last successfully accepted value received before the deadline. Previous baseline values are not retained as separate effective data versions; however, all submitted messages and their processing results are preserved in the message history.
- After the deadline, the Aggregator can no longer change the baseline (see
  [Corrections after the deadline](#corrections-after-the-deadline-and-missing-baselines)).
- The submission obligation does not depend on whether balancing energy is ordered or activated in the
  period — the baseline must be submitted for **all** settlement periods of the associated grid metering
  points.

Time and calendar rules:

- Settlement periods are identified by their **UTC start time**. Estonian local time determines the
  settlement day and month and is used for display.
- A normal local day has 96 settlement periods, the spring DST-transition day 92 and the autumn one 100.
  Repeated local times on the autumn transition day are distinguished by their UTC timestamps.
- Agreement validity is assessed per Estonian calendar day: all settlement periods of a valid calendar day
  are covered.

Other rules:
- See also [General principles data exchange](01.2-general-principles-data-exchange.md). [Header Version 2](01.2-general-principles-data-exchange.md#header-version-2) is used in machine-to-machine messages.

## Transmitting baseline data

General baseline data transmission process

1. The Aggregator submits baseline data to Estfeed Datahub either via the API message or an Excel file.

2. Estfeed Datahub records the message arrival time, which is used for submission deadline validation. Subsequent technical delays do not affect the timeliness assessment.

3. Business validations are performed:
   - The Aggregator must be authorized to submit a baseline for the grid metering point.
   - Submission deadlines and data validity are checked.
   - If any validation fails, HTTP 422 (`REJECTED`) is returned immediately and no data is stored.

4. If all validations pass, HTTP 202 (`ACCEPTED`) is returned and the message enters status `PROCESSING`.

5. The data is stored asynchronously.

6. An all-or-nothing principle applies:
   - If at least one period is invalid, the entire message is rejected.
   - Partial storage is not performed.

7. Before the deadline, data may be resubmitted:
   - A newly accepted value replaces the previous one.
   - The last successfully accepted version is used.

8. After the deadline, the baseline can no longer be changed.

9. All submitted messages, including rejected ones, are retained in the message history and can be viewed through the Status API.

10. Status values:
    - `PROCESSING` - The message has been received and is currently being processed
    - `SUCCESSFUL` - The data has been successfully saved
    - `REJECTED` - The message was rejected because of a validation error or a business rule violation
    - `ERROR` - Processing was completed with errors

### API message

`POST /api/v1/baseline`

The request body is a **list** of objects, one per grid metering point:

**CreateBaselineRequest**

| Attribute | Type | Mandatory | Explanation and rules |
| --- | --- | --- | --- |
| `meteringPointEic` | string (EIC) | yes | EIC code of the **grid** metering point. Must exist in the system; its commodity type must match the `x-commodity-type` header. One message must not contain the same metering point EIC twice. |
| `periods` | list | yes | List of settlement periods. At least one period is mandatory; the maximum number of periods per message depends on the configuration. |

**Period object**

| Attribute | Type | Mandatory | Explanation and rules |
| --- | --- | --- | --- |
| `pS` | string (date-time) | yes | Settlement period start, ISO-8601 with offset. Must fall on a quarter-hour boundary (hh:00, hh:15, hh:30, hh:45). Must satisfy the submission deadline and the 32-day ceiling. |
| `inQty` | number | see below | **Production** baseline, kWh. Non-negative; zero is allowed; precision 0.001 kWh (three decimals). |
| `outQty` | number | see below | **Consumption** baseline, kWh. Non-negative; zero is allowed; precision 0.001 kWh (three decimals). |

> [!WARNING]
> The baseline methodology expects **both** directions for each period: consumption (OUT) and production (IN). A value of 0 represents a submitted baseline with a forecast quantity of zero. A missing field or absence of a direction for a period indicates that the corresponding baseline was not submitted.

**Message rules**

- The submitter must hold the baseline right for **every** grid metering point and **every** period in the
  message: a valid aggregation agreement covering each submitted period (evaluated at the period's time,
  which is always in the future).
- The submission time used for the deadline check is the time the message is received by Estfeed Datahub.
- If even a **single** period violates any rule, the whole message is rejected and nothing is stored. The error response lists all failing periods and rules so the message can be corrected and resubmitted before the deadline. Use the [status API](#checking-the-processing-status)to check the processing result of the submitted message.
- Submitting the same period again before its deadline is not an error: the new value replaces the old one.
- When submitting baseline data, a limit applies to the number of periods that can be included in a single message. A maximum of 35,040 periods can be submitted at once.

**Responses**

| HTTP | Meaning |
| --- | --- |
| `202` | Every period passed validation; the message is queued for storage. Use the [Status API](#checking-the-processing-status) with your `x-document-identification` to confirm the technical outcome. |
| `422` | Business rejection — nothing was stored. The error list names every failing period and rule. |
| `400` / `403` | Malformed request / wrong commodity type, market role or missing rights. |

The success response has no body: the business verdict is the HTTP status code, and the storage outcome is
available through the Status API.

### Web interface and Excel import

The web interface offers the same functionality with an Excel file:

| Operation | Endpoint | Explanation |
| --- | --- | --- |
| Template | `GET /api/v1/baseline/template` | Empty `.xlsx` template: grid metering point EIC, period start, consumption baseline (kWh), production baseline (kWh) |
| Import | `POST /api/v1/baseline/import` | Multipart `.xlsx` upload. The file is validated as a whole (all row errors are collected and returned at once); a valid file is processed exactly like an API message |
| Export | `GET /api/v1/baseline/export` | The [search](#requesting-baseline-data) result as an `.xlsx` file; same parameters as the search API |

When submitting baseline data using an Excel file, the maximum file size is 35,000 rows. For example, when submitting 31 days of baseline data in advance, a single file can contain baseline data for up to 11 metering points.

Import responses: `202` = accepted and queued; `422` with an error list = file-level or business-level
failures, nothing stored; `400`/`403` = broken file / wrong commodity or role. One import produces one
message (one `x-document-identification`), visible in the Status API exactly like an API submission.

## Checking the processing status

`GET /api/v1/baseline/status`

Returns the processing status and submission history of baseline messages — one entry per message,
including messages that were rejected synchronously.

**Parameters**

| Attribute | Mandatory | Explanation and rules |
| --- | --- | --- |
| `lastModifiedTimeFrom` | yes | ISO-8601; start of the window on the status's last change |
| `lastModifiedTimeTo` | yes | Must be greater than `lastModifiedTimeFrom`; the maximum window length depends on the configuration |
| `originalDocumentIdentification` | no | The `x-document-identification` sent with the submission. Can be used to filter by a specific submitted message/document identifier (for example: 3fa85f64-5717-4562-b3fc-2c963f66afa6) |
| `meteringPointEics` | no | Narrow the result to specific grid metering points |
| `status` | no | One of: `REJECTED`, `PROCESSING`, `SUCCESSFUL`, `ERROR` |
| `page` / `size` | no | Paging; defaults 0 / 20, `size` at most 500 |

**Response** — paged; each entry:

| Attribute | Explanation |
| --- | --- |
| `originalDocumentIdentification` | Correlation to the submitted message |
| `receivedTime` | The arrival time used for the deadline verdict |
| `status` | `REJECTED` (terminal at creation) \| `PROCESSING` → `SUCCESSFUL` \| `ERROR` |
| `statusMessage` | Human-readable summary |
| `errors` | Structured error list: validation errors on `REJECTED`, storage errors on `ERROR`, otherwise empty |
| `meteringPoints` | Per-grid-metering-point summary: `eic`, `periodCount`, `earliestPeriodStart`, `latestPeriodStart` |
| `lastModifiedTime` | For incremental polling |

A status entry is created for messages that receive HTTP 202 (`PROCESSING` → `SUCCESSFUL`) and for business validation rejections returned with HTTP 422 (`REJECTED`). Validation errors are available in the errors field. No status entry is created for technically invalid requests that result in HTTP 400 or 403. An Aggregator can see only its own messages.

## Requesting baseline data

`GET /api/v1/baseline`

Returns baseline values together with the metered quantities of the grid metering point and the activated
(metered) quantities of the aggregation metering points, at a chosen aggregation level.

> [!WARNING]
> The parameters and the response layout of the search API are still being finalised. The contract below
> is the current draft.

**Parameters**

| Attribute | Mandatory | Explanation and rules |
| --- | --- | --- |
| `meteringPointEics` | one selector required (At least one of meteringPointEics or resourceEics must be provided) | Grid or aggregation metering point EICs; at least one entry; the maximum depends on the market role and `purpose` |
| `resourceEics` | one selector required | Alternative selector: resource EICs |
| `purpose` | conditional | Purpose of the query; governs the allowed history depth and window length |
| `periodStart` | yes | Inclusive |
| `periodEnd` | no | Exclusive; defaults to the current time; the maximum window length depends on `purpose` |
| `aggregateBy` | no | `RESOURCE` \| `GRID_METERING_POINT` \| `AGGREGATION_METERING_POINT` — The granularity of the response rows. By default, the level corresponds to the selector used (meteringPointEics or resourceEics) |
| `frequencyReserve` | no | `aFRR` \| `mFRR` — limits which aggregation metering points contribute activated quantities to the response. If omitted, both reserve types are included |
| `resolution` | no | `PT15M` (15-minute resolution) |
| `page` / `size` | no | Paging |

**Response** — one entry per aggregation unit and settlement period:

| Attribute | Explanation |
| --- | --- |
| `unit` | Resource EIC or metering point EIC selected by the query parameters |
| `periodStart`, `resolution` | Settlement period identity (UTC start) |
| `inResource` / `outResource` | The sum of the activated quantities of the row's resource |
| `inBaseline` / `outBaseline` | Baseline: production / consumption forecast (energy directions) |
| `inQuantity` / `outQuantity` | Metered quantities of the grid metering point |
| `inActivated` / `outActivated` | Metered quantities of the aggregation metering points (narrowed by `frequencyReserve` when given) |
| `inCorrected` / `outCorrected` | Final validated balancing energy quantities — empty until the validation phase goes live |
| `warnings` | Data-availability notes, e.g. when metered quantities were temporarily unavailable |

Rules:

- An Aggregator receives only grid metering points whose periods its baseline right covers — **including
  historical periods**: an Aggregator can query baselines of grid metering points it was associated with in the
  past.
- A period with no submitted baseline is returned with **empty** baseline columns. Missing data is never
  presented as zero.
- Aggregation levels: searching by one identifier returns the related levels as well — a resource query
  sums its grid metering points; a grid metering point query shows its own values plus the resource
  totals; an aggregation metering point query shows its own activated quantities plus the parent and
  resource context.

## Requesting resource data

`GET /api/v1/resources`

The resource register: which resources exist and which aggregation metering points belong to them.
Resources are **registered and maintained by Elering**; the Aggregator declares the resource EIC on the
aggregation metering point's characteristics when registering the metering point.

**Parameters**

| Attribute | Mandatory | Explanation |
| --- | --- | --- |
| `resourceEics` | no | Filter by resource EIC |
| `meteringPointEics` | no | Aggregation metering points — "which resource does this metering point belong to" |
| `validAt` | no | Point in time for the membership list; defaults to the current time |
| `includeMeteringPoints` | no | Default `true` |
| `page` / `size` | no | Paging |

**Response item**: `resourceEic`, `baselineType`, `ownerEic`, `createdTime`, and (when included)
`meteringPoints[]` with `eic`, `parentMeteringPointEic`, `validFrom`, `validTo`.

An Aggregator sees only its own resources.

## Corrections after the deadline and missing baselines

After the deadline the Aggregator cannot change a submitted baseline. Two Elering-mediated procedures exist:

1. **Correction.** In a justified exceptional case, and based on objective data, Elering can correct an
   already-submitted baseline. Corrected data points are marked with the data quality
   flag *"Andmed muudetud"* and the correction history is retained.
2. **Missing baseline.** A baseline that is not submitted by the deadline is considered a non-submission.

> [!CAUTION]
> A missed deadline is final for the Aggregator. Plan submissions so that every settlement period for each associated metering point is covered at least 30 minutes in advance.
