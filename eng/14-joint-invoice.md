# Joint invoice

## Table of contents

- [Joint invoice](#joint-invoice)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Transmitting a network bill](#transmitting-a-network-bill)
    - [Web interface](#web-interface)
    - [API messages](#api-messages)
      - [Messages](#messages)
      - [Message rules](#message-rules)

## Introduction

The prerequisite for sending a joint invoice is a joint invoice agreement in the Datahub. For more information, see [Agreements](05-agreements.md).

The basic flow scheme of the network bill is as follows: Grid Operator > Datahub > Seller > Customer.

The details of the network bill to be sent are taken from the e-invoice standard ([Estonian e-invoice guide](https://media.voog.com/0000/0042/1620/files/Eesti_e-arve_kirjelduse_juhend_E_arve_saatmine%20ja%20presenteeerimine%20pangas_ver_1_0.pdf)).

## Transmitting a network bill

Network bills can be transmitted via both the API and the web interface (a form for small grid operators) and downloaded (for sellers).

Relevant Datahub services have been set up to transmit and request a network bill. The intended use process is as follows:

- A grid operator sends a new joint network bill message using the `joint-invoice` service.
- The Datahub verifies that:
  - there is a valid joint invoice joint agreement between the designated recipient and the sender and
  - the designated customer has a valid open supply agreement with the bill recipient at this metering point and
  - the designated customer has a valid grid agreement with the bill recipient at this metering point.
- If conditions are not met, then Datahub responds with an error message.
- If conditions are met, then Datahub stores the data in the database.
- Open suppliers can scan network bill changes using the `search` service.
- Open suppliers can download network bills using the `download` service.

### Web interface

> **Note**
> The web interface is being developed.

### API messages

#### Messages

| Message                                      | Objective                |
|----------------------------------------------|--------------------------|
| `POST /api/{version}/joint-invoice`          | Create a joint invoice   |
| `POST /api/{version}/joint-invoice/search`   | Find a joint invoice     |


For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

#### Message rules

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](02-authentication-and-authorisation.md)
