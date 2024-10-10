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

Customer authorization extends the access right of the market participant and can be used to access data, that otherwise would not be allowed.

## Transmitting and requesting the customer authorizations

Relevant Datahub services have been set up to request the customer authorizations. The intended use process is as follows:

- The customer enters the client portal and creates new customer authorization
- The authorized market participant scans for new customer authorizations using the `data-distribution/search` service or searches for specific customer authorization using the `customer-authorization/search` service.
- The authorized market participant can use messages to request the following data:
  - customer data – described in [Customers](04-customer-eic.md);
  - metering point data – described in [Metering points](05-metering-point.md);
  - metering data – described in [Metering data](12-metering-data.md).

### Web interface

> [!NOTE]
> The web interface is being developed.

### API messages

#### Messages

| Message                                             | Objective                                                            |
|-----------------------------------------------------|----------------------------------------------------------------------|
| `POST /api/{version}/customer-authorization/search` | Search for authorizations given by the Customer in the Client Portal |
