# Access right

## Table of contents

- [Access right](#access-right)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Transmitting and requesting access right data](#transmitting-and-requesting-access-right-data)
  - [API messages](#api-messages)
    - [Messages](#messages)
    - [Message rules](#message-rules)

## Introduction

The customer portal is available at [https://estfeed.elering.ee](https://estfeed.elering.ee).

Market participants can grant access rights to open suppliers through the customer portal to view metering point details and metering data from previous periods. This is in particular for the purpose of receiving personalised offers from open suppliers.

The right to access data may also derive from the law.

## Transmitting and requesting access right data

Relevant Datahub services have been set up to transmit and request access right data. The intended use process is as follows:

1. The market participant adds a new access right using the relevant function of the customer portal.
2. The Datahub stores the new access right in its database and designates an open supplier to whom it will be made available.
3. The open supplier uses the `/customer-authorization/search` service and detects that a new access right has been granted to it.
4. Once access has been granted, the open supplier can use messages to request the following data:
   - customer data – described in [Customers](03-customer-eic.md);
   - metering point data – described in [Metering points](04-metering-points.md);
   - metering data – described in [Metering data](07-mooteandmed.md).

## API messages

### Messages

| Message                                             | Objective                                     |
|-----------------------------------------------------|-----------------------------------------------|
| `POST /api/{version}/customer-authorization/search` | Allows the user to search for access rights.  |
| `POST /api/{version}/customer-authorization/change` | Allows the user to scan access right updates. |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

### Message rules

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](02-authentication-and-authorisation.md)

- Each access right has a start and end time. The default validity period is 48h, which can be reduced by the grantor of the access right.
- Each access right includes the specific purpose for which the data is processed and who is the data controller.
- An open supplier does not see the customer’s access rights to other open suppliers.
