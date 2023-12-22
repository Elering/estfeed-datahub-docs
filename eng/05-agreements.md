# Agreements

## Table of contents

- [Agreements](#agreements)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Uninterrupted open supply](#uninterrupted-open-supply)
  - [Transmitting agreements](#transmitting-agreements)
    - [Transmitting agreements using the web interface](#transmitting-agreements-using-the-web-interface)
    - [API messages](#api-messages)
      - [Messages](#messages)
      - [Message rules](#message-rules)

## Introduction

The system allows the user to add the following agreements:

| Agreement                                             | Code               |
| ----------------------------------------------------- | ------------------ |
| grid agreement                                        | GRID               |
| border metering point grid agreement                  | BORDER_GRID        |
| open supply agreement                                 | SUPPLY             |
| aggregation agreement                                 | AGGREGATION        |
| portfolio agreement (this includes balance agreement) | PORTFOLIO_SUPPLIER |
| named supplier agreement                              | NAMED_SUPPLIER     |
| joint invoice agreement                               | JOINT_INVOICE      |

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

- The relevant market participant sends a new or changed agreement message using the `agreement` service.
- Depending on the type of agreement, parties and other data, the Datahub may make additional or changed agreement data available through the `change` service.
- The authorised user requests the agreement data from the `agreement/search` service and, if necessary, exports the agreements using the `agreement/export` service.

### Transmitting agreements using the web interface

> **Note**
> The web interface is under construction

### API messages

In the Datahub, the transmission interface of various agreements is harmonised and thus the same messages and data structures are used. However, it is worth noting that agreements have different rules and therefore a different required and permitted data composition.

#### Messages

| Message                                | Objective                                                   |
| -------------------------------------- | ----------------------------------------------------------- |
| `POST /api/{version}/agreement`        | Allows the user to add a new agreement                      |
| `PUT /api/{version}/agreement`         | Allows the user to update agreement data                    |
| `POST /api/{version}/agreement/delete` | Allows the user to cancel a agreement                       |
| `POST /api/{version}/agreement/search` | Allows the user to search for agreements                    |
| `POST /api/{version}/agreement/export` | Allows the user to export agreements fitting the conditions |
| `POST /api/{version}/agreement/change` | Allows the user to scan agreement data updates              |

The registration of a grid agreement with a metering point is described in [Metering points](04-metering-points.md).

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

> **Note**
> A collection of sample messages is being created

#### Message rules

Dependencies and rules between agreements:

- At any one time, there can be only one valid agreement of the same type between the same parties.
- An open supplier can only add open supply agreements if they have a valid portfolio agreement (i.e. when the open supplier is in someone’s portfolio). The validity period is not taken into account.
- A grid operator can only add grid agreements if they have a valid portfolio agreement (i.e. when the grid operator is in someone’s portfolio). The validity period is not taken into account.
- An aggregator can only add aggregation agreements if they have a valid portfolio agreement (i.e. when the aggregator is in someone’s portfolio). The validity period is not taken into account.
- An open supply agreement cannot be entered into without a valid grid agreement at the metering point. The duration of the open supply agreement cannot exceed the duration of the grid agreement at either end point.
- An aggregation agreement cannot be entered into without a valid grid agreement at the grid metering point (also called the master metering point). The duration of the aggregation agreement cannot exceed the duration of the grid agreement at either end point.
- The customer of the open supply and aggregation agreement must be the same person who is also the customer of the grid agreement.

Other rules:

- The start time of the agreement is given to the day, the agreement will start at 00:00 on the day in question.
- The end time of the agreement is given to the day, the agreement will end at midnight on the day in question.
- The end date of the agreement must be later than the start date.
- It is not permitted to *delete* a valid or expired agreement. It is possible to close a valid agreement by updating the value of the end date of the agreement.
- The type of energy indicated in the agreement must be the same as the type of energy at the metering point indicated in the agreement (if the type of agreement provides for this information).
- For agreements, only the operator ID and the end date of the agreement can be changed. Changing the remaining data is not allowed.

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](02-authentication-and-authorisation.md)
