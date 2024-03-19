# Customer EIC

## Table of contents

- [Customer EIC](#customer-eic)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Transmitting and requesting customer data](#transmitting-and-requesting-customer-data)
  - [API messages](#api-messages)
  - [API message rules](#api-message-rules)
    - [Create or update customer with metadata](#create-or-update-customer-with-metadata)
      - [Attribute specific rules](#attribute-specific-rules)
      - [Additional rules](#additional-rules)
    - [Find customer](#find-customer)
      - [Attribute specific rules](#attribute-specific-rules-1)
      - [Additional rules](#additional-rules-1)
    - [Find Estonian Business Registry representations of Customer](#find-estonian-business-registry-representations-of-customer)
    - [Search Customer agreements](#search-customer-agreements)
    - [Search Customer metering points](#search-customer-metering-points)

## Introduction

Of the market participants mentioned in the Electricity Market Act, the Datahub only enables the addition and modification of *customer* data. The data of remaining market participants are managed by the system operator of the Datahub.

Each customer is assigned an **EIC** by the Datahub, which is the main customer identifier in the system.

The Datahub can register both Estonian and foreign physical and legal persons. In addition, support for non-physical persons who do not have a Commercial Register (or equivalent) code in Estonia or another country has been added. For example, embassies.

## Transmitting and requesting customer data

Relevant Datahub services have been set up to transmit and request customer data. The intended use process can be found in [Business processes](02-business-processes.md#customer-management)

## API messages

| Message                                              | Objective                                                   | Description and rules                                                               |
| ---------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `POST /api/{version}/customer`                       | Create Customer with metadata                               | [Create or update customer with metadata](#create-or-update-customer-with-metadata) |
| `PUT /api/{version}/customer`                        | Update customer with metadata                               | [Create or update customer with metadata](#create-or-update-customer-with-metadata) |
| `POST /api/{version}/customer/search`                | Find a customer by identity                                 | [Find customer](#find-customer)                                                     |
| `POST /api/{version}/customer/search/representative` | Find Estonian Business Registry representations of Customer |                                                                                     |
| `POST /api/{version}/customer/search/agreement`      | Search Customer agreements                                  |                                                                                     |
| `POST /api/{version}/customer/search/meter`          | Search Customer metering points                             |                                                                                     |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

> **Note**
> A collection of sample messages is being created

## API message rules

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](03-authentication-and-authorisation.md)

### Create or update customer with metadata

#### Attribute specific rules

- The data of a customer is:

| Attribute in the API | Explanation                 | Mandatory? | Other rules                                         |
| -------------------- | --------------------------- | ---------- | --------------------------------------------------- |
| customerType         | Type of the customer        | yes        | One of: PHYSICAL_PERSON, LEGAL_PERSON, ORGANIZATION |
| customerMetadata     | Metadata of the customer    | yes        | Attributes described in sections below              |
| customerIdentifiers  | Identifiers of the customer | yes        | Attributes described in sections below              |

- customerMetadata:

Metadata is modelled as key-value pairs, where the "key" is `metadataType` and the "value" is `metadataValue`. Those key-value pairs can have validity. One customer can have more than one metadata value. In this case, this section needs to be multiplied.

| Attribute in the API | Explanation                    | Mandatory?   | Other rules                                                                                                    |
|----------------------|--------------------------------|--------------|----------------------------------------------------------------------------------------------------------------|
| metadataType         | Type of the metadata           | yes          | One of: FIRST_NAME, LAST_NAME, COMPANY_NAME, PHONE, EMAIL, ORGANIZATION_NAME, MOBILE_PHONE, BILLING_ADDRESS, BILLING_BANK_NAME, BILLING_BANK_ACCOUNT, BILLING_METHOD |
| metadataValue        | Value of the metadata          | yes          | |
| validFrom            | Validity start of the metadata | no           | Cannot be empty if `validTo` is provided. Usual value is `now`, because it's hard for grid operators to identify the exact date of creation. But if it's known, then grid operator can provide more accurate datetime |
| validTo              | Validity start of the metadata | no           | Must be bigger, than `validFrom`. Used to "end" some metadata value. For example, the `PHONE`is not used anymore. |

- customerIdentifiers:

One customer can have more than one identifier. In this case, this section needs to be multiplied.

| Attribute in the API | Explanation             | Mandatory? | Other rules                                               |
|----------------------|-------------------------|------------|-----------------------------------------------------------|
| identityType         | Type of the identifier  | yes        | One of: PERSONAL_ID, DOCUMENT_ID, COMPANY_ID, EMBASSY_ID. |
| identityValue        | Value of the identifier | yes        |                                                           |

- identityExtension:

One identity can have multiple extension. For example if the `identityType` value is `DOCUMENT_ID`, then it can have both country and issuer values.

| Attribute in the API | Explanation                     | Mandatory? | Other rules                                                                                                                             |
|----------------------|---------------------------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| extensionType        | Validity start of the extension | no         | One of: COUNTRY, ISSUER                                                                                                                 |
| extensionValue       | Validity start of the extension | no         | In case of `COUNTRY` the 2-character codes of the [ISO standard](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) are used |

#### Additional rules

- Only grid operators are allowed to add or modify customer data.
- When adding or changing a physical person, the following information is mandatory:
  - first name and last name;
  - country;
  - personal identification code if the country value is Estonia;
  - document number if the country value is not Estonian and there is no personal identification code.
- When adding or changing a legal person, the following information is mandatory:
  - name;
  - country;
  - registry code;
- When adding or changing an organization (like embassy), the following information is mandatory:
  - organization name;
  - country;
  - embassy ID;
- Customer type and identity type have the following allowed combinations:

|             | ORGANIZATION | PHYSICAL_PERSON | LEGAL_PERSON |
| ----------- | ------------ | --------------- | ------------ |
| PERSONAL_ID | -            | ✓               | -            |
| COMPANY_ID  | ✓            | -               | ✓            |
| DOCUMENT_ID | ✓            | ✓               | -            |
| EMBASSY_ID  | ✓            | -               | -            |

- Identity type and identity extension type have the following allowed combinations:

|             | COUNTRY | ISSUER |
| ----------- | ------- | ------ |
| PERSONAL_ID | ✓       | ✓      |
| COMPANY_ID  | ✓       | ✓      |
| DOCUMENT_ID | ✓       | ✓      |
| EMBASSY_ID  | ✓       | -      |

- Customer type and metadata type have the following allowed combinations:

|                      | ORGANIZATION | PHYSICAL_PERSON | LEGAL_PERSON |
| -------------------- | ------------ | --------------- | ------------ |
| ORGANIZATION_NAME    | ✓            | -               | -            |
| FIRST_NAME           | -            | ✓               | -            |
| LAST_NAME            | -            | ✓               | -            |
| COMPANY_NAME         | -            | -               | ✓            |
| PHONE                | ✓            | ✓               | ✓            |
| EMAIL                | ✓            | ✓               | ✓            |
| BILLING_METHOD       | ✓            | ✓               | ✓            |
| BILLING_BANK_NAME    | ✓            | ✓               | ✓            |
| BILLING_BANK_ACCOUNT | ✓            | ✓               | ✓            |
| BILLING_ADDRESS      | ✓            | ✓               | ✓            |
| SELF_SERVICE         | ✓            | ✓               | ✓            |

- Only one metadata of the same type can be valid at a time. When updating the data, the Datahub invalidates the previous value (according to the transmitted `validFrom` and `validTo` values, or automatically if they are not provided).
- Additional rules for metadata `BILLING_METHOD`:
  - Allowed values are: `EMAIL`, `POST` and `BANK`
  - For sending multiple values, use comma separated values, like `EMAIL,POST` (without spaces)
  - Depending on the value, additional data might be required:
    - In case of value `EMAIL`, the customer must already have or the message must contain metadata with type `EMAIL`
    - In case of value `POST`, the customer must already have or the message must contain metadata with type `BILLING_ADDRESS`
    - In case of value `BANK`, the customer must already have or the message must contain metadata with type `BILLING_BANK_ACCOUNT` and `BILLING_BANK_NAME`
- Estonian personal identification codes and Estonian registry code are subject to a format check.
- For foreign IDs, no format check applies.
- When registering a new customer, the `customerType + identityType + identityValue + extensionType(COUNTRY)` combination must be unique. If it is not, the customer is an existing customer and the system will treat the add request as a customer update request and will update the customer’s details if possible.

### Find customer

#### Attribute specific rules

| Attribute in the API  | Explanation                                             | Mandatory? | Other rules                                                                                           |
|-----------------------|---------------------------------------------------------|------------|-------------------------------------------------------------------------------------------------------|
| customerTypes         | Types of the customer                                   | yes        | One of: PHYSICAL_PERSON, LEGAL_PERSON, ORGANIZATION, MARKET_PARTICIPANT. Multiple values are allowed. |
| marketParticipantRole | Role of the searched market participant in the Datahub. | no         | Used to search for specific market participants                                                       |
| searchCriteria        | Search criteria                                         | yes        | Uses the same structure as `customerIdentifiers`                                                      |

#### Additional rules

- If the data requester does not have the corresponding right, the customer search service only returns the customer’s EIC.
- Only service provider can be searched by name.

### Find Estonian Business Registry representations of Customer

> **Note**
> Documentation under development

### Search Customer agreements

> **Note**
> Documentation under development

### Search Customer metering points

> **Note**
> Documentation under development
