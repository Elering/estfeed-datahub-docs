# Data distribution

## Table of contents

<!-- TOC -->
* [Data distribution](#data-distribution)
  * [Table of contents](#table-of-contents)
  * [Distributing data updates](#distributing-data-updates)
    * [General rules](#general-rules)
    * [Metering point rules](#metering-point-rules)
    * [Agreement rules](#agreement-rules)
    * [Metering data rules](#metering-data-rules)
    * [Network bill rules](#network-bill-rules)
    * [Customer metadata rules](#customer-metadata-rules)
    * [Customer authorization rules](#customer-authorization-rules)
    * [Agreement coordination rules](#agreement-coordination-rules)
  * [Scanning data updates](#scanning-data-updates)
    * [Reason](#reason)
      * [Simple values](#simple-values)
      * [Complex values](#complex-values)
  * [API messages](#api-messages)
    * [Versions](#versions)
    * [New services](#new-services)
    * [Old services](#old-services)
      * [Request](#request)
      * [Response](#response)
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

### Agreement coordination rules

> [!IMPORTANT]
> Data distribution of agreement coordination is under development

- All coordination candidates get agreement coordination distribution messages if:
  - New agreement coordination was created
  - Existing agreement coordination was cancelled
  - Agreement coordination got an approval or denial response from any candidate

## Scanning data updates

Unlike the old Datahub, the new Datahub does not send messages to integrated parties but requires the integrated system to check whether it has new messages. For this purpose, a dedicated update
pulling API-s have been created.

The system of the integrated market participant scans the data distribution API at a suitable interval, taking into account the usual frequency of data object addition and changing:

- it is recommended that slowly added and changing data (e.g. metering points) are scanned 1-4 times a day;
- it is recommended that rapidly added and changing data (e.g. metering data) are scanned with the same frequency as data are added – for example, every hour or more frequently. This will help the
  Datahub cope better with peak loads.

Resource types are:

- METERING_POINT - metering point
- METERING_DATA - metering data
- NETWORK_BILL - network bill
- CUSTOMER_DATA - customer's metadata (billing data for named supplier)
- AGREEMENT - agreement and general service, which is modelled as agreement
- PERMISSION - customer authorizations (given in the Client Portal)
- AGREEMENT_COORDINATION - agreement coordination

> [!IMPORTANT]
> Agreement coordination is under development

Maximum allowed period in the query depends on the resource type:

- metering data: 1 hour
- other types: 24 hours (this distinction is important during the autumn winter/summer time change, as the local (not UTC) day is 25 hours long)

Maximum allowed range of the ID-s (`idTo` minus `idFrom`) is 10000.

> [!TIP]
> To request messages for a longer period of time, it is possible to send several different requests for different periods. For example, the first message for the period 02.01.2024-03.01.2024 and the second for the period 01.01.2024-02.01.2024.

> [!WARNING]
> Data older than 7 days cannot be read retrospectively.

### Reason

The response message always has a `reason` attribute, which describes the essence of the change. The reasons for the change are as follows:

#### Simple values

Simple values exist for all data object types that have lifecycle. Some data objects may lack some values. For example, it is not possible to delete a metering point or update a network bill.

Simple values are:

- `CREATE` - data object created
- `UPDATE` - data object updated
- `DELETE` - data object deleted

#### Complex values

Complex values are only used in agreement data-distribution messages, because a change to one agreement can lead to changes to another agreement or even multiple agreements. For example, if the SUPPLY agreement is changed due to a change to the GRID agreement.

Complex values always consist of the following parts:

| What happened to the agreement in the message | Because | Type of agreement that caused the change                        | Action of the agreement that caused the change |
|-----------------------------------------------|---------|-----------------------------------------------------------------|------------------------------------------------|
| CREATE, UPDATE or DELETE                      | BC      | GRID, BORDER_GRID, SUPPLY, PORTFOLIO_SUPPLIER or NAMED_SUPPLIER | CREATE, UPDATE or DELETE                       |

The exact list of values used can be found in the Swagger descriptions, but below is a list of some values:

| Category                  | Code                                | Description                                                                                                                              |
|---------------------------|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| GRID impact               | CREATE_BC_GRID_CREATE               | Agreement created, because GRID agreement was created                                                                                    |
|                           | UPDATE_BC_GRID_CREATE               | Agreement updated, because GRID agreement was created                                                                                    |
|                           | DELETE_BC_GRID_CREATE               | Agreement deleted, because GRID agreement was created                                                                                    |
|                           | CREATE_BC_GRID_UPDATE               | Agreement created, because GRID agreement was updated                                                                                    |
|                           | UPDATE_BC_GRID_UPDATE               | Agreement updated, because GRID agreement was updated                                                                                    |
|                           | DELETE_BC_GRID_UPDATE               | Agreement deleted, because GRID agreement was updated                                                                                    |
|                           | DELETE_BC_GRID_DELETE               | Agreement deleted, because GRID agreement was deleted                                                                                    |
| BORDER_GRID impact        | CREATE_BC_BORDER_GRID_CREATE        | Agreement created, because BORDER_GRID agreement was created                                                                             |
|                           | UPDATE_BC_BORDER_GRID_CREATE        | Agreement updated, because BORDER_GRID agreement was created                                                                             |
|                           | DELETE_BC_BORDER_GRID_CREATE        | Agreement deleted, because BORDER_GRID agreement was created                                                                             |
|                           | CREATE_BC_BORDER_GRID_UPDATE        | Agreement created, because BORDER_GRID agreement was updated                                                                             |
|                           | UPDATE_BC_BORDER_GRID_UPDATE        | Agreement updated, because BORDER_GRID agreement was updated                                                                             |
|                           | DELETE_BC_BORDER_GRID_UPDATE        | Agreement deleted, because BORDER_GRID agreement was updated                                                                             |
|                           | CREATE_BC_BORDER_GRID_DELETE        | Agreement created, because BORDER_GRID agreement was deleted                                                                             |
|                           | UPDATE_BC_BORDER_GRID_DELETE        | Agreement updated, because BORDER_GRID agreement was deleted                                                                             |
|                           | DELETE_BC_BORDER_GRID_DELETE        | Agreement deleted, because BORDER_GRID agreement was deleted                                                                             |
| SUPPLY impact             | CREATE_BC_SUPPLY_CREATE             | Agreement created, because SUPPLY agreement was created                                                                                  |
|                           | UPDATE_BC_SUPPLY_CREATE             | Agreement updated, because SUPPLY agreement was created                                                                                  |
|                           | DELETE_BC_SUPPLY_CREATE             | Agreement deleted, because SUPPLY agreement was created                                                                                  |
|                           | CREATE_BC_SUPPLY_UPDATE             | Agreement created, because SUPPLY agreement was updated                                                                                  |
|                           | UPDATE_BC_SUPPLY_UPDATE             | Agreement updated, because SUPPLY agreement was updated                                                                                  |
|                           | DELETE_BC_SUPPLY_UPDATE             | Agreement deleted, because SUPPLY agreement was updated                                                                                  |
|                           | CREATE_BC_SUPPLY_DELETE             | Agreement created, because SUPPLY agreement was deleted                                                                                  |
|                           | UPDATE_BC_SUPPLY_DELETE             | Agreement updated, because SUPPLY agreement was deleted                                                                                  |
|                           | DELETE_BC_SUPPLY_DELETE             | Agreement deleted, because SUPPLY agreement was deleted                                                                                  |
|                           | CREATE_BC_AGREEMENT_COORDINATION    | Agreement created, because other SUPPLY agreement was created or updated via agreement coordination. Used for GENERAL_SERVICE agreements |
|                           | UPDATE_BC_AGREEMENT_COORDINATION    | Agreement updated, because other SUPPLY agreement was created or updated via agreement coordination                                      |
|                           | DELETE_BC_AGREEMENT_COORDINATION    | Agreement deleted, because other SUPPLY agreement was created or updated via agreement coordination                                      |
| PORTFOLIO_SUPPLIER impact | CREATE_BC_PORTFOLIO_SUPPLIER_CREATE | Agreement created, because PORTFOLIO_SUPPLIER was created                                                                                |
|                           | UPDATE_BC_PORTFOLIO_SUPPLIER_CREATE | Agreement updated, because PORTFOLIO_SUPPLIER was created                                                                                |
|                           | DELETE_BC_PORTFOLIO_SUPPLIER_CREATE | Agreement deleted, because PORTFOLIO_SUPPLIER was created                                                                                |
|                           | CREATE_BC_PORTFOLIO_SUPPLIER_UPDATE | Agreement created, because PORTFOLIO_SUPPLIER was updated                                                                                |
|                           | UPDATE_BC_PORTFOLIO_SUPPLIER_UPDATE | Agreement updated, because PORTFOLIO_SUPPLIER was updated                                                                                |
|                           | DELETE_BC_PORTFOLIO_SUPPLIER_UPDATE | Agreement deleted, because PORTFOLIO_SUPPLIER was updated                                                                                |
|                           | CREATE_BC_PORTFOLIO_SUPPLIER_DELETE | Agreement created, because PORTFOLIO_SUPPLIER was deleted                                                                                |
|                           | UPDATE_BC_PORTFOLIO_SUPPLIER_DELETE | Agreement updated, because PORTFOLIO_SUPPLIER was deleted                                                                                |
|                           | DELETE_BC_PORTFOLIO_SUPPLIER_DELETE | Agreement deleted, because PORTFOLIO_SUPPLIER was deleted                                                                                |
| NAMED_SUPPLIER impact     | CREATE_BC_NAMED_SUPPLIER_CREATE     | Agreement created, because NAMED_SUPPLIER was created                                                                                    |
|                           | UPDATE_BC_NAMED_SUPPLIER_CREATE     | Agreement updated, because NAMED_SUPPLIER was created                                                                                    |
|                           | DELETE_BC_NAMED_SUPPLIER_CREATE     | Agreement deleted, because NAMED_SUPPLIER was created                                                                                    |
|                           | CREATE_BC_NAMED_SUPPLIER_UPDATE     | Agreement created, because NAMED_SUPPLIER was updated                                                                                    |
|                           | UPDATE_BC_NAMED_SUPPLIER_UPDATE     | Agreement updated, because NAMED_SUPPLIER was updated                                                                                    |
|                           | DELETE_BC_NAMED_SUPPLIER_UPDATE     | Agreement deleted, because NAMED_SUPPLIER was updated                                                                                    |
|                           | CREATE_BC_NAMED_SUPPLIER_DELETE     | Agreement created, because NAMED_SUPPLIER was deleted                                                                                    |
|                           | UPDATE_BC_NAMED_SUPPLIER_DELETE     | Agreement updated, because NAMED_SUPPLIER was deleted                                                                                    |
|                           | DELETE_BC_NAMED_SUPPLIER_DELETE     | Agreement deleted, because NAMED_SUPPLIER was deleted                                                                                    |

## API messages

### Versions

Data distribution API-s are versioned. When the structure of the request or the response is changed, then new version of the API becomes available.

It is important to understand, that the main API version of the data object may be different, than the data-distribution API version. For example, if agreement search API request structure is updated, but the response remains the same, then there's no need to update the data-distribution API. But if for example the structure of the Agreement entity is changed, then it causes a version bump for data-distribution API also.

Examine the structures of the main API-s and data-distribution API-s in the Swagger to identify matching ones.

### New services

> [!IMPORTANT]
> Agreement and agreement coordination API-s are under development

The term "New" refers to the fact, that these API-s were created after the "Old" API. These API-s are data object specific and return the new version (V2 and newer) of the data object.

| Message                                                 | Objective                                                  |
|---------------------------------------------------------|------------------------------------------------------------|
| `GET /api/v1/data-distributions/agreement`              | Find data-distribution messages of agreements              |
| `GET /api/v1/data-distributions/agreement-coordination` | Find data-distribution messages of agreement coordinations |

New API-s are resource type specific. Therefore the description of the API-s can be found in the Swagger with explicit request and response structures.

### Old services

The term "Old" refers to the fact, that this API was created with the initial delivery of the Datahub. It's a unified API for all data object types (except agreement coordination). 

This API returns the V1 version of the data objects.

| Message                                      | Objective                                                |
|----------------------------------------------|----------------------------------------------------------|
| `POST /api/v1/data-distribution/search`      | Find data-distribution messages of all data object types |

#### Request

Attributes:

| Attribute       | Type              | Required?                                  | Comments                                                                                  |
|-----------------|-------------------|--------------------------------------------|-------------------------------------------------------------------------------------------|
| createdTimeFrom | string($datetime) | yes, if idFrom/idTo  are not defined       | Start of the creation time of the data distribution message                               |
| createdTimeTo   | string($datetime) | yes, if idFrom/idTo  are not defined       | End of the creation time of the data distribution message                                 |
| idFrom          | int               | yes, if createdTimeFrom/To are not defined | Start of the message ID                                                                   |
| idTo            | int               | yes, if createdTimeFrom/To are not defined | End of the message ID                                                                     |
| resourceType    | int               | yes                                        | One of: METERING_POINT, METERING_DATA, NETWORK_BILL, CUSTOMER_DATA, AGREEMENT, PERMISSION |
| pagination      | int               | yes                                        | Standard pagination section                                                               |

#### Response

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

#### Resource types

##### Agreement

###### Attributes

The system uses the same data structure and attributes as described in the response message of  `POST /api/{version}/agreement` service, but the following differences may occur:

- `agreementId`, `meterEic` and `validTo` can be not present if they are not set in the original agreement message.
- `serviceProviderEic` and `customerEic` are missing, if the information should not be available (because of business rules) for the market participant

###### Examples

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

##### Metering Point

###### Attributes

The system uses the same structure and attributes as the `PUT /api/{version}/meter` service.

###### Examples

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

##### Metering data

###### Attributes

The structure of metering data distribution message is exactly the same as in `POST /meter-data` message.

###### Examples

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

##### Network bill

###### Attributes

The structure of network bill data distribution message is exactly the same as in `POST /network-bill` message.

###### Examples

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

##### Customer

###### Attributes

Customer's metadata data-distribution message contains of following sections:

- `customerType` - same as in `api/{version}/customer/search` response message
- `customerMetadata` - same as in `api/{version}/customer/search` response message
- `customerEic` - customer's EIC code

###### Examples

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

##### Customer authorizations

###### Attributes

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

###### Examples

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
