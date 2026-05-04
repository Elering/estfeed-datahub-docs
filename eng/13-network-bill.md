# Network bill

## Table of contents

- [Network bill](#network-bill)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Transmitting and requesting a network bill](#transmitting-and-requesting-a-network-bill)
  - [API messages](#api-messages)
    - [Messages](#messages)
    - [Message rules](#message-rules)
  - [Net metering data in network bill message](#net-metering-data-in-network-bill-message)

## Introduction

The grid operator can use the network bill generation message to transmit information about the moment and the data on the basis of which the grid operator billed the customer for the grid service. The information in this message allows suppliers to bill their customers for the same amount of energy as the network bill. The Datahub transmits the message sent by the grid operator to the open supplier of the metering point.

As of **01.08.2026** grid operators are required to set net measured metering data for bidirectional metering points to the Estfeed Datahub. The data must be calculated by the grid operator by subtracting consumption from production. Therefore, starting from the beginning of September, the grid operator must submit the network bill together with net measured quantities. For this purpose transition to new API version is needed. Testing in the test environment is possible, if market participants admin does not have access to the test evironment then write to datahub@elering.ee to sign a test environment agreement with Elering. Initially, two API versions will remain in parallel use, but the V1 version does not support net measured quantities.

> [!WARNING] 
> The Datahub is not responsible for the quality of the energy amount data provided in the message.

> [!WARNING]
> Day and night quantities are optional also in V2 API, change will be made in Swagger soon.

## Transmitting and requesting a network bill

Relevant Datahub services have been set up to transmit and request a network bill. The intended use process is as follows:

- The grid operator sends a new or updated network bill message using the `POST /api/v2/network-bills/bulk` service.
- Datahub stores the network bill into the database
- The open supplier searches for new network bills using the `POST /api/v2/data-distributions/network-bill` service. Data can be requested for 7 days.

In order to update a network bill, new `network-bill` message with same period values and updated `calculationTimestamp` value must be sent.

## API messages

### Messages

| Message                                   | Objective                          |
|-------------------------------------------|------------------------------------|
| `POST /api/v2/network-bills/bulk`         | Create or update network bill data |

### Message rules

- Rules for adding network bills:
  - Only grid operator (GO) or closed distribution network operator (CDN) can add network bills
  - The `periodStart` cannot be smaller than the validity start of grid agreement
  - and `periodEnd` cannot be bigger than the validity end of grid agreement
  - The maximum network billing period is one month.
  - The period start and end month value must be the same (if the open supplier does not change at the turn of the month, then the grid operator must transmit two separate network bills).
- If the market participant uses the general service, the transmission of the network bills to the Datahub is optional.
- Rules for searching network bills:
  - grid operator (GO) and closed distribution network operator (CDN) can search for network bills, that they added.
  - open supplier can search for those network bills, where the `periodStart` and `periodEnd` are covered with such open supply agreement, where the open supplier is the service provider.
  - named supplier can search for those network bills, where the `periodStart` and `periodEnd` are covered with such GENERAL_SERVICE agreement, where the named supplier is the service provider.