# Metering point

## Table of contents

- [Metering point](#metering-point)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Transmitting metering point data](#transmitting-metering-point-data)
    - [Web interface](#web-interface)
    - [Mass import](#mass-import)
    - [API messages](#api-messages)
      - [Messages](#messages)
      - [Message rules](#message-rules)
  - [Requesting metering point data](#requesting-metering-point-data)
    - [API messages](#api-messages-1)
      - [Messages](#messages-1)
      - [Message rules](#message-rules-1)

## Introduction

A metering point is a device that measures the amount of energy consumed and produced at a given location.

Metering points are managed by the following market participants:

- grid operator;
- line operator;
- closed distribution network operator;
- aggregator;
- producer;
- charging point operator;
- storage operator;
- gas station operator.

For the purpose of this document, they are collectively referred to as **metering point operators**.

Metering point operators are responsible for adding and updating metering point data for the metering points in their area in the Datahub.

> **Warning**
> 
> Please note! Metering point operators are obliged to update the metering point data as soon as possible.

## Transmitting metering point data

Metering point operators can transmit the technical data of metering points:

- one by one using web interface
- using mass import via web interface
- one by one using `meter` service
- using `import` service for mass import

The data of metering point is the same in all interfaces. The data of a metering point is:

- Common data for all metering point types:

| Attribute in the API | Column name in mass import template | Explanation        | Mandatory? | Other rules                                                     |
|----------------------|-------------------------------------|--------------------|------------|-----------------------------------------------------------------|
| meterEic             | Metering Point EIC                  | 16 digits EIC code | yes        | Must be valid EIC code and inside the range of issued EIC range |
| meteringType         | Metering Type                       |                    | yes        | One of: REMOTE_READING, VIRTUAL, NON_REMOTE_READING             |
| meteringPointType    | Metering Point Type                 |                    | yes        | One of: REGULAR, INTERNAL, BORDER, AGGREGATION                  |

- Specific data for electricity and gas metering points:

| Attribute in the API   | Column name in mass import template | Explanation                               | Mandatory? | Other rules                                                                                               |
|------------------------|-------------------------------------|-------------------------------------------|------------|-----------------------------------------------------------------------------------------------------------|
| consumptionScale       | Consumption Scale                   |                                           | yes        | One of: SMALL, LARGE                                                                                      |
| connectionState        | Conection State                     |                                           | yes        | One of: CONNECTED, DISCONNECTED                                                                           |
| resolution             | Resolution                          |                                           | yes        | One of: PT15M (15 minutes), PT1H (1 hour)                                                                 |
| customerType           | Customer Type                       |                                           | yes        | One of: CONSUMER, GRID_OPERATOR, PRODUCER, MICRO (micro producer), LINE_OPERATOR, ENERGY_STORAGE_UNIT, CHARGING_POINT_OPERATOR |
| production             | Production                          | is any production in metering point?      | yes        | One of: TRUE (yes), FALSE (no)                                                                            |
| productionSource       | Production Source                   |                                           | no         | One of: SOLAR, WIND, HYDRO, BIOGAS, BIOMASS, NATURAL_GAS, OIL_SHALE, OTHER_RENEWABLE, OTHER_NON_RENEWABLE |
| transmissionNetworkEic | Transmission Network EIC            | 16 digit EIC code of transmission network | yes        | EIC code of transmission network must be registered in the Datahub                                        |
| apartmentAssociation   | Apartment Association               | is associated with apartment              | yes        | One of: TRUE (yes), FALSE (no)                                                                            |

- Specific data for electricity metering points:

| Attribute in the API  | Column name in mass import template | Explanation                                | Mandatory? | Other rules                                                                                   |
|-----------------------|-------------------------------------|--------------------------------------------|------------|-----------------------------------------------------------------------------------------------|
| isolatedMeteringPoint | Isolated Metering Point             | is isolated metering point?                | yes        | One of: TRUE (yes), FALSE (no)                                                                |
| electricalHeating     | Electrical Heating                  | electrical heating used in metering point? | yes        | One of: TRUE (yes), FALSE (no)                                                                |
| chargingPoint         | Charging Point                      | is charging point?                         | yes        | One of: TRUE (yes), FALSE (no)                                                                |
| storageCapacity       | Storage Capacity                    | storage capacity in kW                     | no         | Must be integer or floating (max. 2 positions after comma) number. Enter value 0 if no value. |
| storageEnergy         | Storage Energy                      | storage capacity  energy in kWh            | no         | Must be integer or floating (max. 2 positions after comma) number. Enter value 0 if no value. |
| productionCapacity    | Production Capacity                 |                                            | no         | Must be integer or floating (max. 2 positions after comma) number. Enter value 0 if no value. |
| transmissionCapacity  | Transmission Capacity               |                                            | no         | Must be integer or floating (max. 2 positions after comma) number. Enter value 0 if no value. |

- Specific data for aggregation metering points:

| Attribute in the API | Column name in mass import template | Explanation                                | Mandatory? | Other rules                   |
|----------------------|-------------------------------------|--------------------------------------------|------------|-------------------------------|
| parentMeterEic       | Parent Metering Point EIC           | 16 digit EIC code of parent metering point | yes        | Must be registered in Datahub |

- Common address data for all metering point types:

| Attribute in the API | Column name in mass import template | Explanation                                  | Mandatory?                               | Other rules           |
|----------------------|-------------------------------------|----------------------------------------------|------------------------------------------|-----------------------|
| adrId                | Adr ID                              | Address ID (ADR_ID) of Land Board ADS system | yes if county and municipality are empty | Must be an integer    |
| comment              | Comment                             |                                              | no                                       |                       |
| county               | County                              |                                              | yes                                      |                       |
| municipality         | Municipality                        |                                              | yes                                      |                       |
| locality             | Locality                            |                                              | no                                       |                       |
| streetAddress        | Street Address                      | street, house, apartment etc                 | yes                                      |                       |
| postcode             | Postcode                            |                                              | yes                                      |                       |
| latitude             | Latitude                            | latitude of coordinates                      | no                                       | In case LEST97, the value must be 7 positions before and 1-3 positions after comma. In case WHS84, the value must be 2 positions before and 4-8 positions after comma. |
| longitude            | Longitude                           | latitude of coordinates                      | no                                       | In case LEST97, the value must be 6 positions before and 1-3 positions after comma. In case WHS84, the value must be 2 positions before and 4-8 positions after comma. |
| coordinateSystem     | Coordinate Sytem                    |                                              | yes if coordinates are provided          | One of: WGS84, LEST97 |

> **Note**
> The structure and validation rules of address attributes are under development

### Web interface

> **Note**
> Documentation is under development

### Mass import

Both web interface and API services provide option to perform metering point mass import using MS Excel file. To use that option, one has to use the web interface or `template` service and download commodity and metering point type specific template, add data and upload the filled template using the web interface or `import` service.

The data of the metering point is described in paragraph [Transmitting metering point data](#transmitting-metering-point-data), but there is one difference - as the template is already commodity and metering point type specific, then the additional metering point type (REGULAR või INTERNAL) has to be specified only for the electricity or gas metering points

### API messages

#### Messages

| Message                              | Objective                                 |
|--------------------------------------|-------------------------------------------|
| `POST /api/{version}/meter`          | Create meter with metadata                |
| `PUT /api/{version}/meter`           | Update meter metadata                     |
| `POST /api/{version}/template/meter` | Get metering point mass import templates  |
| `POST /api/{version}/meter/import`   | Mass import metering points with template |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

#### Message rules

- The EIC of the metering point must be within the range of the grid operator’s EICs.
- The type of the metering point defines the allowed metadata:
  - regular, border, internal types – gas or electricity metadata are allowed;
  - aggregation – aggregation metadata are allowed.
- The resolution of the metering point is additional information and does not affect the transmission of metering data in the future, but only characterises whether the metering point is able to read consumption with an accuracy of 15 minutes, one hour or a day.
- Rules for XY coordinates:
  - XY coordinates are not mandatory
  - Values must be numerical, that can contain positions after comma
  - Values must fit inside the bounding box of Estonia
- For electricity metering point, the `marketParticipantRole` value must be one of:
  - GRID_OPERATOR
  - LINE_OPERATOR
  - CLOSED_DISTRIBUTION_NETWORK
  - PRODUCER_OPERATOR
  - CHARGING_POINT_OPERATOR
- For gas metering point, the `marketParticipantRole` value must be one of:
  - GRID_OPERATOR
  - PRODUCER_OPERATOR
- For electricity metering point, the `marketParticipantRole` value must be AGGREGATOR
- For data quality reasons, please use the official [EHAK classification](https://klassifikaatorid.stat.ee/Item/stat.ee/c4c47742-12d7-4fea-bc8c-5aeca9112e2a/88) (county, municipality and settlement unit designations) for addresses submitted as text.

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](03-authentication-and-authorisation.md)

## Requesting metering point data

In general, all authorised users can request metering point data using the `search` services, but open suppliers and balance responsible parties can also request updates of new and changed metering point data using the `data-distribution/search` service.

### API messages

#### Messages

| Message                                     | Objective                              |
|---------------------------------------------|----------------------------------------|
| `POST /api/{version}/meter/search`          | Find a Metering Point by attributes    |
| `POST /api/{version}/meter/search/customer` | Find a Metering Point by Customer EIC  |
| `POST /api/{version}/meter/search/border`   | Get border Metering Points by customer |
| `POST /api/{version}/meter/export`          | Export Metering Points by attributes   |

> **Warning**
> 
> Service `POST /api/{version}/meter/search/customer` is allowed to use only when adding new agreement. Legitimate usage of this service is monitored 

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

> **Note**
> A collection of sample messages is being created

#### Message rules

> **Note**
> The rights for transmitting and requesting data are described in [Authentication and authorisation](03-authentication-and-authorisation.md)

- If the data requester has the necessary right to see the customer’s data, the search service only returns the EIC.
- The Datahub issues metering point data without an address if a verification is carried out in accordance with subsection 8 (5) of the Network Code on the Operation of the Electricity Market.
- If the user has access rights, the Datahub outputs the entire data set of the metering point.
