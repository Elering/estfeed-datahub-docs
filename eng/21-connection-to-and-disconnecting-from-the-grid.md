# Connecting to and disconnecting from the grid

## Table of contents

- [Connecting to and disconnecting from the grid](#connecting-to-and-disconnecting-from-the-grid)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Connection and disconnection request and confirmation](#connection-and-disconnection-request-and-confirmation)
    - [API messages](#api-messages)
      - [Messages](#messages)
      - [Message rules](#message-rules)

## Introduction

If a grid service provider and an open supplier have entered into a joint invoice agreement, a market participant will always be sent a joint invoice (the market participant cannot choose otherwise) and the open supplier will have the right to request that the grid connection be turned off if the market participant has not paid its joint invoice.

> **Warning**
> 
> All functionality described in this document is excluded from the original scope.

## Connection and disconnection request and confirmation

Relevant Datahub services have been set up to transmit the request and confirmation for connecting and disconnecting. The intended use process is as follows:

1. An open supplier sends a request to turn the connection on or off.
2. The Datahub verifies that there is (or has been in the last six months) a valid joint invoice agreement between the designated recipient and the sender and whether the designated customer has (or has had within the past 12 months) a valid open supply agreement with the sender at this metering point and whether the combination of the designated customer and the metering point has (or has had within the past 12 months) a valid grid agreement with the recipient:
   - if not, the Datahub responds with an error message;
   - if yes, the Datahub stores the data in the database and makes the data available to the grid operator via the `change` service.
3. If necessary, the open supplier can update the application data using the `PUT` service (this service can also be used to cancel a subscription).
4. The grid operator can scan connection and disconnection requests using the `change` service.
5. The grid operator adds the status of the request using the `connection-state/response` service. Possible options are:
   - indicating a plan to connect or disconnect a metering point;
   - refusal to connect or disconnect a metering point;
   - connecting or disconnecting a metering point.
6. The open supplier scans the grid operator’s responses using the `change` service.
7. The grid operator updates the status of the request using the `connection-state/response` service. Possible options are:
   - a change in the plan to connect or disconnect a metering point;
   - refusal to connect or disconnect a metering point;
   - connecting or disconnecting a metering point.
8. The open supplier scans the grid operator’s responses using the `change` service.

### API messages

#### Messages

| Message                                         | Objective                                                                         |
|-------------------------------------------------|-----------------------------------------------------------------------------------|
| `POST /api/{version}/connection-state`          | Allows the user to create a new connection or disconnection request               |
| `PUT /api/{version}/connection-state`           | Allows the user to change or cancel the connection or disconnection request       |
| `POST /api/{version}/connection-state/search`   | Allows the user to search for a response to a connection or disconnection request |
| `POST /api/{version}/connection-state/response` | Allows the user to create a new response to a connection or disconnection request |
| `PUT /api/{version}/connection-state/response`  | Allows the user to change the response to a connection or disconnection request   |
| `POST /api/{version}/connection-state/change`   | Allows the user to scan connection or disconnection requests or their responses   |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

#### Message rules

- A single connection or disconnection request can only have one response. The response must be changed in the case of reconsideration.
- Users can modify the connection or disconnection request before the grid operator has sent a reply with the final state (CONNECTED, DISCONNECTED).

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](02-authentication-and-authorisation.md)
