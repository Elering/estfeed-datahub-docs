# Customer enquiries

> **Warning**
> 
> Talks with market participants on the implementation of this service package are still ongoing. The description below is only a preliminary vision.

## Table of contents

- [Customer enquiries](#customer-enquiries)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Transmitting and replying to a customer enquiry](#transmitting-and-replying-to-a-customer-enquiry)
    - [Web interface](#web-interface)
    - [API messages](#api-messages)
      - [Messages](#messages)
      - [Message rules](#message-rules)

## Introduction

The purpose of the customer enquiry transmission process is to transmit customer enquiries related to the grid service from suppliers to grid operators. Customer enquiries can only be transmitted as messages between a supplier and a grid operator. The functionality of customer enquiries involves information exchange between grid operators and suppliers in a standardised form.

> **Warning**
> 
> All functionality described in this document is excluded from the original scope.

## Transmitting and replying to a customer enquiry

It is possible to send and view enquiries via both the API and web interface.

Relevant Datahub services have been set up to transmit enquiries. The intended use process is as follows:

- An open supplier sends the information regarding customer enquiries using the `direct-messages` service.
- The Datahub stores the enquiry and makes it available to the grid operator via the `TODO` service.
- The grid operator scans the `TODO` service and receives new or changed enquiries.
- The grid operator sends a response to the enquiry using the `response` service.
- The Datahub stores the response and makes it available to the open supplier via the `TODO` service.
- The open supplier scans the `TODO` service and receives new or changed responses.

The grid operator or open supplier can use the `search` service to search for enquiries and responses stored in the Datahub.

### Web interface

> **Note**
> The web interface is being developed

### API messages

#### Messages

| Message                                        | Objective                                                                                       |
|------------------------------------------------|-------------------------------------------------------------------------------------------------|
| `POST /api/{version}/direct-messages`          | Allows the user to register a new customer inquiry                                              |
| `PUT /api/{version}/direct-messages`           | Allows the user to change the data of an existing customer enquiry or cancel a customer enquiry |
| `POST /api/{version}/direct-messages/search`   | Allows the user to search for customer enquiries and responses                                  |
| `POST /api/{version}/direct-messages/response` | Allows the user to register a new response to a customer enquiry                                |
| `PUT /api/{version}/direct-messages/response`  | Allows the user to change the data of an existing response to a customer enquiry                |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

#### Message rules

- The Datahub does not check the recipient of enquiries. It is the responsibility of the open supplier to provide correct data.

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](02-authentication-and-authorisation.md)
