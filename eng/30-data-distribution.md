# Data distribution

## Table of contents

<!-- TOC -->
* [Data distribution](#data-distribution)
  * [Table of contents](#table-of-contents)
  * [Introduction](#introduction)
  * [Scanning data updates](#scanning-data-updates)
  * [Distributing data updates](#distributing-data-updates)
  * [Examples](#examples)
    * [Agreement](#agreement)
    * [Metering Point](#metering-point)
    * [Metering data](#metering-data)
    * [Network bill](#network-bill)
    * [Customer](#customer)
    * [Reports](#reports)
<!-- TOC -->

## Introduction

For business processes to run successfully and smoothly, the integrated systems of market participants need to be aware of new and changed information.

For this, new information needs to be delivered to the systems of market participants. This document describes the technical solution for distributing data updates through the API interface.

## Scanning data updates

Unlike the old Datahub, the new Datahub does not send messages to integrated parties but requires the integrated system to check whether it has new messages. For this purpose, a dedicated update
pulling API `/data-distribution/search ` has been created, which works in a standard way:

- The system of the integrated market participant sends a request defining time period and dataobject type.
- The Datahub finds previously created data distribution messages addressed to the Market Participant and where the attributes match with the search criteria.
- The Datahub returns new or changed data objects together with the reason of change.

The system of the integrated market participant scans the data distribution API at a suitable interval, taking into account the usual frequency of data object addition and changing:

- it is recommended that slowly added and changing data (e.g. metering points) are scanned 1-4 times a day;
- it is recommended that rapidly added and changing data (e.g. metering data) are scanned with the same frequency as data are added – for example, every hour or more frequently. This will help the
  Datahub cope better with peak loads.

Resource types are:

- METERING_POINT - metering point
- METERING_DATA - metering data
- NETWORK_BILL - network bill
- CUSTOMER - customer's metadata (billing data for named supplier)
- AGREEMENT - agreement and general service, which is modelled as agreement
- REPORT - reports

Maximum allowed period in the query depends on the resource type:

- metering data: 1 hour
- other types: 1 day

## Distributing data updates

Elering’s team is discussing various technical solutions to enable more capable integrated systems to receive data updates faster and without scanning. A specific technical solution is still under
development. Market participants will be informed in a timely and thorough manner when it is ready.

## Examples

### Agreement

```json
[
    {
        "agreementId": "einar-2024-04-03T16:25:08.569885+03:00-EST",
        "meterEic": "38ZGO-1000001B-X",
        "agreementType": "SUPPLY",
        "preliminaryTerminationFee": false,
        "commodityType": "ELECTRICITY",
        "validFrom": "2024-04-03T21:00:00Z",
        "validTo": "2024-04-17T21:00:00Z"
    }
]
```

### Metering Point

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

> **Note**
> A collection of sample messages is being created

### Customer

> **Note**
> A collection of sample messages is being created

### Reports

> **Note**
> A collection of sample messages is being created

