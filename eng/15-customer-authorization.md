# Customer authorization

## Table of contents

- [Customer authorization](#customer-authorization)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Sending and requesting the customer authorizations](#sending-and-requesting-the-customer-authorizations)
    - [Web interface](#web-interface)
    - [API messages](#api-messages)
      - [Messages](#messages)
      - [Message rules](#message-rules)

## Introduction

Customer authorization is an access right given by the customer to the open supplier or other market participant via the client portal. Access right given this way has specific validity period and scope.

Customer authorization extends the access right of the market participant and can be used to query such metering point(s) and metering data, that otherwise would not be allowed.

## Sending and requesting the customer authorizations

Relevant Datahub services have been set up to transmit the customer authorizations. The intended use process is as follows:

- The customer enters the client portal and creates new customer authorization
- The authorized market participant scans for new customer authorizations using the `data-distribution/search` service or searches for specific customer authorization using the `search` service.
- The authorized market participant queries the metering point and its metering data using the  `meter` or `meter-data` services by the authorized metering point's EIC code (customer authorization is not used in the data-distribution process).

### Web interface

> **Note**
> The web interface is being developed.

### API messages

#### Messages

| Message                                      | Objective                                                            |
|----------------------------------------------|----------------------------------------------------------------------|
| `POST /api/{version}/customer-authorization` | Search for authorizations given by the Customer in the Client Portal |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

#### Message rules

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](02-authentication-and-authorisation.md)