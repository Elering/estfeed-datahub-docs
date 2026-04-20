# Agreements

## Table of contents

<!-- TOC -->
* [Agreements](#agreements)
  * [Table of contents](#table-of-contents)
  * [Introduction](#introduction)
  * [Uninterrupted open supply](#uninterrupted-open-supply)
  * [Transmitting agreements](#transmitting-agreements)
    * [API messages](#api-messages)
      * [Message rules](#message-rules)
    * [Web interface](#web-interface)
  * [Searching and exporting agreements](#searching-and-exporting-agreements)
    * [API messages](#api-messages-1)
      * [Message rules](#message-rules-1)
    * [Web interface](#web-interface-1)
<!-- TOC -->

## Introduction

The system allows the user to add the following agreements:

| Agreement                                             | Code               | Market |
|-------------------------------------------------------|--------------------|----|
| grid agreement                                        | GRID               | Electricity, Gas |
| border metering point grid agreement                  | BORDER_GRID        | Electricity, Gas |
| open supply agreement                                 | SUPPLY             | Electricity, Gas |
| aggregation agreement                                 | AGGREGATION        | Electricity |
| portfolio agreement (this includes balance agreement) | PORTFOLIO_SUPPLIER | Electricity, Gas |
| named supplier agreement                              | NAMED_SUPPLIER     | Electricity, Gas |
| joint invoice agreement                               | JOINT_INVOICE      | Electricity, Gas |

Agreements have different rules. In addition, there are rules between agreements, for example, an open supply agreement cannot be added to a period where there is no grid agreement.

## Uninterrupted open supply

Balance responsibility is ensured through an uninterrupted open supply chain in the following hierarchy:

1. The system operator has an open supply agreement for the Estonian electricity system. The system operator settles the open supplies of the Estonian electricity system and balance responsible parties. Elering is an open supplier of its own grid losses.
2. An open supplier that has a balance agreement with the system operator is called a balance responsible party. The balance responsible party uses readings from the border metering points in the balance area where it is responsible to settle the balance.
3. An open supplier has an open supply agreement with one balance responsible party (unless the open supplier is itself a balance responsible party). An open supplier settles the balances of those market participants in its area whose open supplier it is.
4. A distribution network operator has an open supply agreement with one open supplier for its service area (to cover grid losses).
5. A consumer and a producer enter into an open supply agreement with one open supplier, i.e. there can be only one open supply agreement per metering point per time period.

## Transmitting agreements

Agreements can be transmitted to the Datahub using both a web interface and an automatic data exchange message. Relevant Datahub services have been set up to transmit and request agreements. The intended use process is as follows:

- The relevant market participant sends a new or changed agreement message using the agreement service.
- Depending on the type of agreement, parties and other data, the Datahub may make additional or changed agreement data available through the data distribution service.
- The authorised user requests the agreement data from the search service and, if necessary, exports the agreements using the export service.

### API messages

In the Datahub, the transmission interface of various agreements is harmonised and thus the same messages and data structures are used. However, it is worth noting that agreements have different rules and therefore a different required and permitted data composition.

| V1 message                      | V2 message                       | Objective                          |
|---------------------------------|----------------------------------|------------------------------------|
| `POST /api/v1/agreement`        | `POST /api/v2/agreements`        | Create agreement                   |
| `POST /api/v1/agreement-bulk`   | `POST /api/v2/agreements/bulk`   | Create multiple agreements at once |
| `PUT /api/v1/agreement`         | `PUT /api/v2/agreements/{id}`    | Update agreement                   |
| `POST /api/v1/agreement/delete` | `DELETE /api/v2/agreements/{id}` | Delete agreement                   |

> [!IMPORTANT]
> The implementation of agreement V2 API-s are a prerequisite for the market participant to receive coordinated changes to the agreements via the data distribution service (Data Distribution). To do this, market participants must request the IDs of all their agreements via the `GET /api/v2/agreements` service.


#### Message rules

Dependencies and rules between agreements:

- Validity periods of portfolio, joint invoice or named supplier agreement between the same parties cannot overlap
- Validity periods of (border) grid, (border) supply, aggregation or general service agreement between the same parties and the same metering point cannot overlap
- An open supplier can only add open supply agreements if they have a valid portfolio agreement (i.e. when the open supplier is in someone’s portfolio). The validity period is not taken into account.
- A grid operator can only add grid agreements if they have a valid portfolio agreement (i.e. when the grid operator is in someone’s portfolio). The validity period is not taken into account.
- An aggregator can only add aggregation agreements if they have a valid portfolio agreement (i.e. when the aggregator is in someone’s portfolio). The validity period is not taken into account.
- An open supply agreement cannot be entered into without a valid grid agreement at the metering point. The duration of the open supply agreement cannot exceed the duration of the grid agreement at either end point.
- An aggregation agreement cannot be entered into without a valid grid agreement at the parent metering point. The duration of the aggregation agreement cannot exceed the duration of the grid agreement at either end point.

Other rules:

- The start and end time of the agreement is presented in the user interface with the accuracy of the day or month:
  - See the following table: user interface — monthly precision
- The start and end time of the agreement is presented in the API with the accuracy of date and time:
  - See the following table: user interface — daily precision, data exchange interface start/end
- The end date of the agreement must be later or equal than the start date (one-day agreements have the same start and end date, but different time values).
- It is not permitted to *delete* a valid or expired agreement. It is possible to close a valid agreement by updating the value of the end date of the agreement.
- It is not permitted to modify expired agreement.
- The type of energy indicated in the agreement must be the same as the type of energy at the metering point indicated in the agreement (if the type of agreement provides for this information).
- For agreements, only the operator's agreement ID and the end date of the agreement can be changed. Changing the remaining data is not allowed.

Electricity Market and Gas Market Contract Start and End Differences

| **Domain** | **Rule / Description** | **Electricity Market (midnight – midnight)** | **Gas Market (gas day 07:00 – 07:00)** |
|-----------|------------------------|-----------------------------------------------|---------------------------------------|
| **User interface — monthly precision** | Contract starts | 1st day of the month at 00:00 | 1st day of the month at 07:00 |
| | Contract ends | at midnight on the last day of the month | 1st day of the following month at 07:00 |
| **User interface — daily precision** | Contract starts | Selected day at 00:00 (Ex: 01.01.2024 00:00)| Selected day at 07:00 (Ex: 01.01.2024 07:00) |
| | Contract ends | at midnight on the selected day (30.04.2024 midnight)| Following day at 07:00 (01.05.2024 07:00)|
| **Data exchange interface — start** | Start time according to EE time | 01.01.2024 00:00:00 | 01.01.2024 07:00:00 |
| Must be sent in the message | Start example (winter time) | 2024-01-01T00:00:00+02:00 or 2023-12-31T22:00:00Z | 2024-01-01T07:00:00+02:00 or 2024-01-01T05:00:00Z |
| **Data exchange interface — end** | End time according to EE time | 30.04.2024 at midnight | 01.05.2024 07:00:00 |
| Must be sent in the message | End example (summer time) | 2024-05-01T00:00:00+03:00 or 2024-04-30T21:00:00Z | 2024-05-01T07:00:00+03:00 or 2024-05-01T04:00:00Z |
| **Valid until (result)** | According to Data Hub interpretation | 30.04.2024 23:59:59 | 01.05.2024 06:59:59 |

### Web interface

> [!NOTE]
> Transmitting agreements using the web interface is described in the sub-pages.

## Searching and exporting agreements

There are 2 different business cases where agreements are searched:

1. When market participant wants to find agreements, where it is a service provider or customer. After the search, exporting might be performed.
2. When market participant is adding a new grid, supply or aggregation agreement and wants to see other agreements of the metering points.

### API messages

| V1 message                            | V2 message                                     | Objective                                                                       |
|---------------------------------------|------------------------------------------------|---------------------------------------------------------------------------------|
| `POST /api/v1/agreement/search`       | `GET /api/v2/agreements`                       | Find agreements, where the market participant is a service provider or customer |
| -                                     | `GET /api/v2/agreements/{id}`                  | Find specific agreement by ID                                                   |
| `POST /api/v1/agreement/search/meter` | `GET /api/v2/metering-points/{eic}/agreements` | Find agreements by Metering Point during new agreement registration             |
| `POST /api/v1/agreement/export`       | `GET /api/v2/agreements/export`                | Export agreements by attributes                                                 |

> [!IMPORTANT]
> The implementation of agreement V2 API-s are a prerequisite for the market participant to receive coordinated changes to the agreements via the data distribution service (Data Distribution). To do this, market participants must request the IDs of all their agreements via the `GET /api/v2/agreements` service.

#### Message rules

> [!CAUTION] 
> Using the `/agreement/search/meter` or `/metering-points/{eic}/agreements` API endpoint is allowed only during new agreement registration process. The use of the service and the legality of use are monitored.

### Web interface

> [!NOTE]
> Searching and exporting agreements using the web interface is described in the sub-pages.
