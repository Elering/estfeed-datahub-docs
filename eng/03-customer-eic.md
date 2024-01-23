# Customer EIC

## Table of contents

- [Customer EIC](#customer-eic)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Transmitting and requesting customer data](#transmitting-and-requesting-customer-data)
  - [API messages](#api-messages)
    - [Messages](#messages)
    - [Message rules](#message-rules)

## Introduction

Of the market participants mentioned in the Electricity Market Act, the Datahub only enables the addition and modification of *customer* data. The data of remaining market participants are managed by the system operator of the Datahub.

Each customer is assigned an **EIC** by the Datahub, which is the main customer identifier in the system.

The Datahub can register both Estonian and foreign natural and legal persons. In addition, support for non-natural persons who do not have a Commercial Register (or equivalent) code in Estonia or another country has been added. For example, embassies.

## Transmitting and requesting customer data

Relevant Datahub services have been set up to transmit and request customer data. The intended use process is as follows:

- A grid operator sends a new or changed customer message using the `customer` service.
- The Datahub stores the customer’s details and assigns an EIC to the customer.
- The authorised user requests the customer’s data from the `customer/search` service.
- The authorised user requests updates of new and changed customer data by using the `/data-distribution/search` service.

## API messages

### Messages

| Message                                              | Objective                                                   |
|------------------------------------------------------|-------------------------------------------------------------|
| `POST /api/{version}/customer`                       | Create Customer with metadata                               |
| `PUT /api/{version}/customer`                        | Update customer with metadata                               |
| `POST /api/{version}/customer/search`                | Find a customer by identity                                 |
| `POST /api/{version}/customer/search/representative` | Find Estonian Business Registry representations of Customer |
| `POST /api/{version}/customer/search/agreement`      | Search Customer agreements                                  |
| `POST /api/{version}/customer/search/meter`          | Search Customer metering points                             |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

> **Note**
> A collection of sample messages is being created

### Message rules

- Only grid operators are allowed to add or modify customer data.
- When registering a new customer, the Datahub will check whether the person already exists in the system:
  - If they exist, the Datahub returns the EIC of the existing customer to the message sender and, if there was new information in the message, updates the data (e.g. name).
  - If the person does not yet exist, the Datahub creates a new person, assigns them an EIC and returns the EIC.
- When adding or changing a natural person, the following information is mandatory:
  - first name and last name;
  - country;
  - personal identification code if the country value is Estonia;
  - document number if the country value is not Estonian and there is no personal identification code.
- When adding or changing a legal person, the following information is mandatory:
  - name;
  - country;
  - Commercial Register code if the country value is Estonia and the person is not an embassy;
  - other identifier if the person is a foreign company or embassy.
- Estonian personal identification codes are subject to a format check.
- For foreign IDs, no format check applies.
- The 2-character codes of the [ISO standard](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) are used for country values.
- When registering a new customer, the `customerType + identityType + identityValue + extensionType(COUNTRY)` combination must be unique. If it is not, the customer is an existing customer and the system will treat the add request as a customer update request and will update the customer’s details if possible.
- If the data requester does not have the corresponding right, the customer search service only returns the customer’s EIC.
- Only market participant can be searched by name.

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](02-authentication-and-authorisation.md)
