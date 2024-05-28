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
- Depending on the type of agreement, parties and other data, the Datahub may make additional or changed agreement data available through the `data-distribution/search` service.
- The authorised user requests the agreement data from the `agreement/search` service and, if necessary, exports the agreements using the `agreement/export` service.

### API messages

In the Datahub, the transmission interface of various agreements is harmonised and thus the same messages and data structures are used. However, it is worth noting that agreements have different rules and therefore a different required and permitted data composition.

| Message                                | Objective                          |
|----------------------------------------|------------------------------------|
| `POST /api/{version}/agreement`        | Create agreement                   |
| `PUT /api/{version}/agreement`         | Update agreement                   |
| `POST /api/{version}/agreement/delete` | Delete agreement                   |
| `POST /api/{version}/agreement-bulk`   | Create multiple agreements at once |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](03-authentication-and-authorisation.md)

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

Other rules:

- The start and end time of the agreement is presented in the user interface with the accuracy of the day or month:
  - If the type of agreement allows validity periods to be determined by month:
    - the agreement starts on the first day of the selected month at 00:00
    - the agreement ends at midnight of the last day of the selected month.
  - If the type of agreement allows the validity period to be determined by days:
    - the agreement starts at 00:00 on the selected day
    - the agreement ends at midnight of the selected day.
- The start and end time of the agreement is presented in the API with the accuracy of date and time:
  - The start time of the agreement must be 00:00:00 Estonian time on the first day of the agreement validity. The Datahub interprets the date and time provided as inclusive. For example, if the agreement should start from the beginning of 01.01.2024, `2024-01-01T:00:00+02:00` or `2023-12-31T22:00:00Z` must be sent in the message.
  - The end time of the agreement must be 00:00:00 Estonian time of the day following the end of the agreement. The Datahub interprets the provided date and time as exclusive. For example, if the agreement should end at midnight on 30.04.2024, then `2024-05-01T00:00:00+03:00` or `2024-04-30T21:00:00Z` must be sent in the message, which according to the Datahub business logic means that the agreement was valid until 30.04.2024 23:59:59.
- The end date of the agreement must be later than the start date.
- It is not permitted to *delete* a valid or expired agreement. It is possible to close a valid agreement by updating the value of the end date of the agreement.
- The type of energy indicated in the agreement must be the same as the type of energy at the metering point indicated in the agreement (if the type of agreement provides for this information).
- For agreements, only the operator ID and the end date of the agreement can be changed. Changing the remaining data is not allowed.

### Web interface

> **Note**
> Transmitting agreements using the web interface is described in the sub-pages.

## Searching and exporting agreements

There are 2 different business cases where agreements are searched:

1. When market participant wants to find agreements, where it is a service provider or customer. After the search, exporting might be performed.
2. When market participant is adding a new grid, supply or aggregation agreement and wants to see other agreements of the metering points.

### API messages

| Message                                      | Objective                                                                       |
| -------------------------------------------- | ------------------------------------------------------------------------------- |
| `POST /api/{version}/agreement/search`       | Find agreements, where the market participant is a service provider or customer |
| `POST /api/{version}/agreement/search/meter` | Find agreements by Metering Point during new agreement registration             |
| `POST /api/{version}/agreement/export`       | Export agreements by attributes                                                 |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

> **Note**
> A collection of sample messages is being created

#### Message rules

> **Warning**
> 
> Using the `/agreement/search/meter` API endpoint is allowed only during new agreement registration process. The use of the service and the legality of use are monitored.

- The metering point agreements search API returns the full data of agreements only if the requester is a service provider of the agreement or if the customer of the metering point has authorized the market participant.

### Web interface

> **Note**
> Searching and exporting agreements using the web interface is described in the sub-pages.
