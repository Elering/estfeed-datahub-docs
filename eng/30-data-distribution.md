# Data distribution

## Table of contents

<!-- TOC -->
* [Data distribution](#data-distribution)
  * [Table of contents](#table-of-contents)
  * [Introduction](#introduction)
  * [Scanning data updates](#scanning-data-updates)
    * [Reason](#reason)
  * [Distributing data updates](#distributing-data-updates)
    * [General rules](#general-rules)
    * [Metering point rules](#metering-point-rules)
    * [Agreement rules](#agreement-rules)
    * [Metering data rules](#metering-data-rules)
    * [Network bill rules](#network-bill-rules)
    * [Customer metadata rules](#customer-metadata-rules)
    * [Customer authorization rules](#customer-authorization-rules)
  * [Structure of the message](#structure-of-the-message)
  * [Resource types](#resource-types)
    * [Agreement](#agreement)
      * [Attributes](#attributes)
      * [Examples](#examples)
    * [Metering Point](#metering-point)
      * [Attributes](#attributes-1)
      * [Examples](#examples-1)
    * [Metering data](#metering-data)
      * [Attributes](#attributes-2)
      * [Examples](#examples-2)
    * [Network bill](#network-bill)
      * [Attributes](#attributes-3)
      * [Examples](#examples-3)
    * [Customer](#customer)
      * [Attributes](#attributes-4)
      * [Examples](#examples-4)
    * [Customer authorizations](#customer-authorizations)
      * [Attributes](#attributes-5)
      * [Examples](#examples-5)
<!-- TOC -->

## Introduction

For business processes to run successfully and smoothly, the integrated systems of market participants need to be aware of new and changed information.

For this, new information needs to be delivered to the systems of market participants. This document describes the technical solution for distributing data updates through the API interface.

## Scanning data updates

Unlike the old Datahub, the new Datahub does not send messages to integrated parties but requires the integrated system to check whether it has new messages. For this purpose, a dedicated update
pulling API `/data-distribution/search ` has been created, which works in a standard way:

- The system of the integrated market participant sends a request defining time period (or message ID start and end) and data object type.
- The Datahub finds previously created data distribution messages addressed to the Market Participant and where the attributes match with the search criteria.
- The Datahub returns new or changed data objects together with the reason of change.

The system of the integrated market participant scans the data distribution API at a suitable interval, taking into account the usual frequency of data object addition and changing:

- it is recommended that slowly added and changing data (e.g. metering points) are scanned 1-4 times a day;
- it is recommended that rapidly added and changing data (e.g. metering data) are scanned with the same frequency as data are added – for example, every hour or more frequently. This will help the
  Datahub cope better with peak loads.

Attributes of the request

| Attribute       | Type | Required?                                  | Comments                                                                                  |
|-----------------|------|--------------------------------------------|-------------------------------------------------------------------------------------------|
| createdTimeFrom | int  | yes, if idFrom/idTo  are not defined       | Start of the creation time of the data distribution message                               |
| createdTimeTo   | int  | yes, if idFrom/idTo  are not defined       | End of the creation time of the data distribution message                                 |
| idFrom          | int  | yes, if createdTimeFrom/To are not defined | Start of the message ID                                                                   |
| idTo            | int  | yes, if createdTimeFrom/To are not defined | End of the message ID                                                                     |
| resourceType    | int  | yes                                        | One of: METERING_POINT, METERING_DATA, NETWORK_BILL, CUSTOMER_DATA, AGREEMENT, PERMISSION |
| pagination      | int  | yes                                        | Standard pagination section                                                               |

Resource types are:

- METERING_POINT - metering point
- METERING_DATA - metering data
- NETWORK_BILL - network bill
- CUSTOMER_DATA - customer's metadata (billing data for named supplier)
- AGREEMENT - agreement and general service, which is modelled as agreement
- PERMISSION - customer authorizations (given in the Client Portal)

Maximum allowed period in the query depends on the resource type:

- metering data: 1 hour
- other types: 24 hours (this distinction is important during the autumn winter/summer time change, as the local (not UTC) day is 25 hours long)

Maximum allowed range of the ID-s (`idTo` minus `idFrom`) is 10000.

> [!TIP]
> To request messages for a longer period of time, it is possible to send several different requests for different periods. For example, the first message for the period 02.01.2024-03.01.2024 and the second for the period 01.01.2024-02.01.2024.

### Reason

The response message always has a `reason` attribute, which for AGREEMENT and METERING_POINT resource types helps to understand why this change occurred (since they can be changed).
For the rest of the resource types, the value may be missing or always be `CREATE` because they have no lifecycle.

The reasons for the change are as follows:

- Fixed values - these values are always the same. They are so called "hard coded" and behave like an enum. Possible values are:
  - `CREATE` - data object got created
  - `UPDATE` - data object got updated
  - `DELETE` - data object got deleted
- Dynamic values - these values are dynamic, because the root cause of the change was indirect. The data object got created, updated or deleted because of some operation with another data object. For example, when SUPPLY agreement gets modified because of the modification of the GRID agreement. Known possible values are:
  - `UPDATE_BC_SUPPLY_CREATE` - data object got updated, because SUPPLY agreement was created
  - `UPDATE_BC_GRID_UPDATE` - data object got updated, because GRID agreement was updated
  - `DELETE_BC_GRID_UPDATE` - data object got deleted, because GRID agreement was updated
  - `DELETE_BC_GRID_DELETE` - data object got deleted, because GRID agreement was deleted
  - `CREATE_BC_PORTFOLIO_SUPPLIER_CREATE` - data object got created, because PORTFOLIO_SUPPLIER agreement was created
  - `UPDATE_BC_PORTFOLIO_SUPPLIER_UPDATE` - data object got updated, because PORTFOLIO_SUPPLIER agreement was updated
  - `DELETE_BC_PORTFOLIO_SUPPLIER_UPDATE` - data object got deleted, because PORTFOLIO_SUPPLIER agreement was updated
  - `DELETE_BC_PORTFOLIO_SUPPLIER_DELETE` - data object got deleted, because PORTFOLIO_SUPPLIER agreement was deleted
  - `CREATE_BC_BORDER_GRID_CREATE` - data object got created, because BORDER_GRID agreement was created
  - `UPDATE_BC_BORDER_GRID_UPDATE` - data object got updated, because BORDER_GRID agreement was updated
  - `DELETE_BC_BORDER_GRID_UPDATE` - data object got deleted, because BORDER_GRID agreement was updated
  - `DELETE_BC_BORDER_GRID_DELETE` - data object got deleted, because BORDER_GRID agreement was deleted

> [!NOTE]
> The format of the dynamic values follow a pattern: "what happened to the data object in the message" + BC (because) + "what was done with the data object causing the change"

> [!WARNING]
> 
> Data older than 7 days cannot be read retrospectively.

## Distributing data updates

Different business rules have been implemented in the Datahub regarding when and to whom data updates are distributed. This document does not describe all the rules, but to give an idea of how data primarily flows, here is a general list of the most important rules.

### General rules

- The Datahub identifies the parties to be notified based on the data in the agreements.
- The notified parties are divided into two categories:
  - Direct parties – their right to notifications derives from a direct end-user agreement.
  - Portfolio providers – their right to notifications derives from portfolio agreements.
- Changes are not reflected back to the data senders/modifiers through data distribution.
- All portfolio providers at different levels are notified uniformly.
- In general, portfolio providers are the recipients of various data distribution notifications. Only in a few cases, only the direct party is notified. **In the following sections, portfolio providers are not listed separately.**

### Metering point rules

- No changes are distributed for a metering point without valid or future-valid agreements.

| Condition                                    | Distribution                                                            |
|----------------------------------------------|-------------------------------------------------------------------------|
| Border metering point data is changed        | Customer                                                                |
| Metering point data is changed               | Open supplier, named supplier, aggregator of aggregation metering point |

### Agreement rules

- The service provider's portfolio provider is always a subject of data distribution.
- The system decides based on business rules whether the full or partial agreement data is distributed.
- When adding/modifying/deleting an aggregation agreement, it is checked whether there is a temporal overlap with the parent metering point's GENERAL_SERVICE, SUPPLY, or BORDER_SUPPLY agreements.
  - If not, no data distribution follows after adding/modifying/deleting the aggregation agreement.
  - If there is, distribution follows.
- GENERAL_SERVICE agreements are distributed only after their activation

| Condition                                                                                                  | Distribution                                                                                                             |
|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| The system creates or deletes a GENERAL_SERVICE agreement where the named supplier is the service provider | named supplier, grid operator                                                                                            |
| The system creates or deletes a GENERAL_SERVICE agreement where the grid operator is the service provider  | Grid operator                                                                                                            |
| Modification/deletion of GRID or BORDER_GRID agreement                                                     | Active or future open supplier, aggregator of aggregation metering point                                                 |
| Modification of GRID agreement affecting SUPPLY agreement(s)                                               | Open supplier(s), Metering point operator                                                                                |
| Addition/modification/deletion of SUPPLY agreement                                                         | Metering point operator                                                                                                  |
| Addition/modification/deletion of SUPPLY agreement the way, that it affects other SUPPLY agreement(s)      | Metering point operator , other opeen supplier                                                                           |
| Addition/modification/deletion of AGGREGATION agreement                                                    | According to overlapping agreements in the parent metering point: open supplier, named supplier, metering point operator |

### Metering data rules

- Upon receiving metering data, the Datahub checks whether all the submitted data (one message may contain data for several metering points over multiple periods) can be forwarded one-to-one to the corresponding recipients or not. If not, the Datahub splits the data so that only the intended data reaches the recipients.
- Data distribution directly depends on the SUPPLY, BORDER_SUPPLY, GENERAL_SERVICE, AGGREGATION agreements of the metering point and the overlap of the agreement validity periods with the periods in the submitted data. If the period in the metering data message overlaps with any such agreement, metering data is distributed to the service provider of that agreement.

### Network bill rules

- Upon receiving the network bill, the Datahub checks whether all the submitted data can be forwarded one-to-one to the corresponding recipients or not. If not, the Datahub splits the data so that only the intended data reaches the recipients.
- The recipient of data distribution can be either the open supplier or named supplier, or both, depending on the SUPPLY or GENERAL_SERVICE agreement.

### Customer metadata rules

- Updates to the customer's BILLING metadata are distributed to the named supplier who currently has or had a valid GENERAL_SERVICE agreement with the customer within the last 12 months (provided that the named supplier did not change the data themselves).
- Updates to the customer's name are distributed to active service providers.

### Customer authorization rules

- A new customer authorization is always distributed to the subject of the customer authorization.

> [!NOTE]
> Elering’s team is discussing various technical solutions to enable more capable integrated systems to receive data updates faster and without scanning. A specific technical solution is still under
development. Market participants will be informed in a timely and thorough manner when it is ready.

## Structure of the message

Every data distribution response message consists of common and resource type specific attributes:

| Attribute            | Type     | Always present? | Comments                                                                                                    |
|----------------------|----------|-----------------|-------------------------------------------------------------------------------------------------------------|
| id                   | int      | yes             | Unique message ID, that is increasing in the time.                                                          |
| createdTime          | datetime | yes             | Creation time of the data distribution (not the message, that caused data distribution) message             |
| resourceType         | string   | yes             | Resource type                                                                                               |
| reason               | string   | jah             | Values described in section [Reason](#reason).                                                              |
| hasContent           | bool     | jah             | If "true", then position "content" has content. If "false", then content is missing (for technical reasons) |
| content              | string   | yes             | Content of the message, depending on the resource type (see next paragraphs)                                |
| contentMissingReason | string   | no              | Human readable explanation about the reason, why the attribute "content" is empty                           |
| pagination           | object   | jah             | Standard pagination elements                                                                                |

Possible `contentMissingReason` values:

* "File not found at the specified path"
* "Unexpected error while getting file from MinIO"
* "The path value is null"

Example of the response message:

```json
{
  "dataDistributions": [
    {
      "id": 4656,
      "createdTime": "2024-05-23T10:08:44.320005900Z",
      "resourceType": "AGREEMENT",
      "reason": "CREATE",
      "hasContent": true,
      "content": "[{\"meterEic\":\"38ZGO-1000001U-D\",\"agreementType\":\"GENERAL_SERVICE\",\"preliminaryTerminationFee\":false,\"commodityType\":\"ELECTRICITY\",\"validFrom\":\"2024-05-22T21:00Z\",\"validTo\":\"2024-05-31T21:00Z\"}]"
    },
    {
      "id": 4660,
      "createdTime": "2024-05-23T10:10:13.682197100Z",
      "resourceType": "AGREEMENT",
      "reason": "CREATE",
      "hasContent": true,
      "content": "[{\"agreementId\":\"einar-2024-05-23T13:08:42.936268+03:00-EST\",\"meterEic\":\"38ZGO-1000001U-D\",\"agreementType\":\"SUPPLY\",\"preliminaryTerminationFee\":true,\"commodityType\":\"ELECTRICITY\",\"validFrom\":\"2024-05-22T21:00Z\",\"validTo\":\"2024-06-30T21:00Z\",\"serviceProviderEic\":\"38X-EIN-OS-----J\",\"customerEic\":\"38X-AVP-ZW6700C6\"}]"
    },
    {
      "id": 4661,
      "createdTime": "2024-05-23T10:10:13.682552100Z",
      "resourceType": "METERING_POINT",
      "reason": "",
      "content": "",
      "hasContent": false,
      "contentMissingReason": "File not found at the specified path"
    }
  ],
  "pagination": {
    "page": 0,
    "totalPages": 1
  }
}

```

## Resource types

### Agreement

#### Attributes

The system uses the same data structure and attributes as described in the response message of  `POST /api/{version}/agreement` service, but the following differences may occur:

- `agreementId`, `meterEic` and `validTo` can be not present if they are not set in the original agreement message.
- `serviceProviderEic` and `customerEic` are missing, if the information should not be available (because of business rules) for the market participant

#### Examples

```json
{
  "meterEic": "38ZGO-10000074-U",
  "agreementType": "GENERAL_SERVICE",
  "preliminaryTerminationFee": false,
  "commodityType": "ELECTRICITY",
  "validFrom": "2024-11-12T22:00Z",
  "validTo": "2024-11-30T22:00Z",
  "serviceProviderEic": "38X-EIN-GO-----0",
  "customerEic": "38X-AVP-ZW6700C6"
}
```

```json
{
  "agreementType": "JOINT_INVOICE",
  "preliminaryTerminationFee": false,
  "commodityType": "ELECTRICITY",
  "validFrom": "2024-05-31T21:00Z",
  "serviceProviderEic": "38X-EIN-NS-----R",
  "customerEic": "38X-EIN-ALL----B"
}
```

### Metering Point

#### Attributes

The system uses the same structure and attributes as the `PUT /api/{version}/meter` service.

#### Examples

```json
{
    "meteringPoint": {
        "meterEic": "38ZGO-10000018-5",
        "meteringType": "NON_REMOTE_READING"
    },
    "meterLocation": {
        "adrId": 3182855,
        "comment": "Müristab jaanuaris, siis ei kuule seda jaanipäeva aegu.",
        "county": "Rapla maakond",
        "municipality": "Kehtna vald",
        "locality": "Järvakandi alev",
        "streetAddress": ", Uus tn, , 20-3",
        "postcode": "79101",
        "coordinates": {
            "coordinateSystem": "LEST97",
            "latitude": 6515113.24,
            "longitude": 546858.53
        }
    },
    "electricityCharacteristics": {
        "consumptionScale": "SMALL",
        "connectionState": "DISCONNECTED",
        "resolution": "PT15M",
        "customerType": "MICRO",
        "production": true,
        "productionSource": "SOLAR",
        "transmissionNetworkEic": "38A-EE-98-4634-U",
        "apartmentAssociation": true,
        "isolatedMeteringPoint": false,
        "electricalHeating": true,
        "chargingPoint": false,
        "storageCapacity": 603.4,
        "storageEnergy": 636.83,
        "productionCapacity": 580.39,
        "transmissionCapacity": 440.17
    }
}
```

### Metering data

#### Attributes

The structure of metering data distribution message is exactly the same as in `POST /meter-data` message.

#### Examples

```json
[
    {
        "meterEic": "38ZGO-1000000C-Y",
        "periods": [
            {
                "r": "PT15M",
                "aI": [
                    {
                        "pS": "2024-03-21T00:00:00+02:00",
                        "inQty": {
                            "rTime": "2024-03-21T09:45:58.146109Z",
                            "rType": "E",
                            "kwh": 12.803
                        },
                        "outQty": {
                            "rTime": "2024-03-21T09:45:58.146118Z",
                            "rType": "E",
                            "kwh": 1.417
                        }
                    },
                    {
                        "pS": "2024-03-21T00:15:00+02:00",
                        "inQty": {
                            "rTime": "2024-03-21T09:45:58.146123Z",
                            "rType": "E",
                            "kwh": 49.497
                        },
                        "outQty": {
                            "rTime": "2024-03-21T09:45:58.146126Z",
                            "rType": "E",
                            "kwh": 27.454
                        }
                    }
                ]
            }
        ]
    }
]
```

### Network bill

#### Attributes

The structure of network bill data distribution message is exactly the same as in `POST /network-bill` message.

#### Examples

```json
[
    {
        "commodityType": "ELECTRICITY",
        "meterEic": "38ZGO-10000013-K",
        "networkBillPeriod": {
            "calculationTimestamp": "2024-05-02T17:23:07.648663+03:00",
            "containsCalculatedValues": true,
            "measurements": [
                {
                    "day": 10,
                    "direction": "IN",
                    "measurementUnit": "KWH",
                    "night": 10,
                    "total": 20
                },
                {
                    "day": 20,
                    "direction": "OUT",
                    "measurementUnit": "KWH",
                    "night": 20,
                    "total": 40
                }
            ],
            "periodEnd": "2024-03-25T00:00+02:00",
            "periodStart": "2024-03-24T00:00+02:00"
        }
    }
]
```

### Customer

#### Attributes

Customer's metadata data-distribution message contains of following sections:

- `customerType` - same as in `api/{version}/customer/search` response message
- `customerMetadata` - same as in `api/{version}/customer/search` response message
- `customerEic` - customer's EIC code

#### Examples

```json
{
  "customerType": "PHYSICAL_PERSON",
  "customerMetadata": [
    {
      "metadataType": "BILLING_METHOD",
      "metadataValue": "BANK,POST,EMAIL",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "FIRST_NAME",
      "metadataValue": "Mari",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "LAST_NAME",
      "metadataValue": "Maasikas",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "PHONE",
      "metadataValue": "55667788",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "BILLING_ADDRESS",
      "metadataValue": "A.H.Tammsaare tee 55, Mustamäe linnaosa, Tallinn",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "BILLING_BANK_NAME",
      "metadataValue": "SEB Pank Eesti",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "EMAIL",
      "metadataValue": "mari.maasikas@gmail.com",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "MOBILE_PHONE",
      "metadataValue": "+37255667788",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "BILLING_BANK_ACCOUNT",
      "metadataValue": "EE1234567890",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    }
  ],
  "customerEic": "38X-AVP-ZW6700C6"
}
```

```json
{
  "customerType": "PHYSICAL_PERSON",
  "customerMetadata": [
    {
      "metadataType": "FIRST_NAME",
      "metadataValue": "Einars",
      "validFrom": "2024-05-27T12:58:18.648130Z"
    },
    {
      "metadataType": "LAST_NAME",
      "metadataValue": "Arros",
      "validFrom": "2024-05-27T12:58:18.648130Z"
    }
  ],
  "customerEic": "38X-AVP-ZW6700C6"
}
```

### Customer authorizations

#### Attributes

| Attribute           | Type     | Always present? | Description                                                                                                                          |
|---------------------|----------|-----------------|--------------------------------------------------------------------------------------------------------------------------------------|
| mandateCustomerEic  | string   | YES             | 16-characters long EIC code of the market participant                                                                                |
| mandateCustomerType | string   | YES             | One of: PRIVATE, LEGAL                                                                                                               |
| meteringPointEic    | string   | YES             | 16-characters long EIC code of the metering point                                                                                    |
| ownerCustomerEic    | string   | YES             | 16-characters long EIC code of the customer                                                                                          |
| ownerCustomerType   | string   | YES             | One of: PRIVATE, LEGAL                                                                                                               |
| participantRoleType | string   | YES             | For open supplier always OPEN_SUPPLIER; for aggregator always AGGREGATOR; for energy service provider always ENERGY_SERVICE_PROVIDER |
| permissionType      | string   | YES             | Always ACCESS                                                                                                                        |
| purpose             | string   | YES             | For open supplier always ENERGY_SUPPLY_OFFER, for aggregator always AGGREGATION_OFFER, for energy service provider various values    |
| status              | string   | YES             | Always APPROVED                                                                                                                      |
| subjectPeriodFrom   | datetime | YES             | The beginning of the time period to which the customer authorization gives access                                                    |
| subjectPeriodTo     | datetime | YES             | The end of the time period to which the customer authorization gives access                                                          |
| validFrom           | datetime | YES             | Validity start of the customer authorization                                                                                         |
| validTo             | datetime | NO              | Validity end of the customer authorization                                                                                           |

#### Examples

```json
{
    "mandateCustomerEic": "38XVK-08600000-Q",
    "mandateCustomerType": "LEGAL",
    "meteringPointEic": "38Z-EE-DL-00N39F",
    "ownerCustomerEic": "38X-AVP-ILS600CI",
    "ownerCustomerType": "PRIVATE",
    "participantRoleType": "OPEN_SUPPLIER",
    "permissionType": "ACCESS",
    "purpose": "ENERGY_SUPPLY_OFFER",
    "status": "APPROVED",
    "subjectPeriodFrom": "2023-05-20T00:00Z",
    "subjectPeriodTo": "2024-05-20T00:00Z",
    "validFrom": "2024-05-20T21:37:54.499Z",
    "validTo": "2024-05-22T21:37:54.499Z"
}
```
