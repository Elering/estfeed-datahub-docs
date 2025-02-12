# Joint invoice

## Table of contents
<!-- TOC -->
* [Joint invoice](#joint-invoice)
  * [Table of contents](#table-of-contents)
  * [Introduction](#introduction)
  * [Transmitting and requesting a joint invoice](#transmitting-and-requesting-a-joint-invoice)
  * [Web interface](#web-interface)
  * [API messages](#api-messages)
  * [API message rules](#api-message-rules)
    * [Create or update joint invoice](#create-or-update-joint-invoice)
      * [Attribute specific rules](#attribute-specific-rules)
      * [Additional rules](#additional-rules)
      * [Example messages](#example-messages)
    * [Find and download joint invoice](#find-and-download-joint-invoice)
      * [Attribute specific rules](#attribute-specific-rules-1)
      * [Additional rules](#additional-rules-1)
<!-- TOC -->

## Introduction

The prerequisite for sending a joint invoice is a joint invoice agreement in the Datahub. For more information, see [Joint invoice agreement](06.7-joint-invoice-agreement.md)

The details of the joint invoice to be sent are taken from the e-invoice standard ([Estonian e-invoice guide](https://media.voog.com/0000/0042/1620/files/Eesti_e-arve_kirjelduse_juhend_E_arve_saatmine%20ja%20presenteeerimine%20pangas_ver_1_0.pdf)).

## Transmitting and requesting a joint invoice

Joint invoices can be transmitted via the API. In the future the possibility to add it via the web interface will be added - a form for small grid operators.

Relevant Datahub services have been set up to transmit and request joint invoices. The intended use process can be found in [Business processes](02-business-processes.md#joint-invoice-management)

## Web interface

> [!NOTE]
> The web interface for adding joint invoices is being developed.

> [!NOTE]
> The guide for searching and downloading joint invoices in the web interface is under development.

## API messages

| Message                                      | Objective                     | Description and rules                                               |
|----------------------------------------------|-------------------------------|---------------------------------------------------------------------|
| `POST /api/{version}/joint-invoice`          | Create/update a joint invoice | [Create or update joint invoice](#create-or-update-joint-invoice)   |
| `POST /api/{version}/joint-invoice/search`   | Find a joint invoice          | [Find and download joint invoice](#find-and-download-joint-invoice) |
| `POST /api/{version}/joint-invoice/download` | Download a joint invoice      | [Find and download joint invoice](#find-and-download-joint-invoice) |

## API message rules

### Create or update joint invoice

Joint invoice contains of these sections:

- `marketParticipantContext` section as for every REST message
- `jointInvoiceHeadersList` - list of `jointInvoiceHeaders`. Contains the metadata of the joint invoice
- `invoiceList` - list of `invoice` files in base64 format 

The header contains the metadata and invoice contains the base64 of the joint invoice.

Joint invoices cannot be updated. In case of need for correction, the grid operator or closed distribution network operator will send new joint invoice message containing credit joint invoice XML and if needed a new joint invoice

#### Attribute specific rules

- `jointInvoiceHeaders` header data:

| Attribute       | Description                               | Mandatory? | Other rules                                                       |
|-----------------|-------------------------------------------|------------|-------------------------------------------------------------------|
| senderEic       | EIC code of the sender                    | yes        |                                                                   |
| receiverEic     | EIC code of the receiver                  | yes        |                                                                   |
| commodityType   | Commodity type                            | yes        | One of: ELECTRICITY, NATURAL_GAS                                  |
| customerEic     | EIC code of the customer                  | yes        |                                                                   |
| meterEics       | EIC code(s) of the metering point(s)      | yes        | EIC codes of the metering point on the invoice                    |
| dataPeriodStart | Start date and time of the invoice period | yes        |                                                                   |
| dataPeriodEnd   | End date and time of the invoice period   | yes        |                                                                   |
| fileName        | Name of the file on position "invoice"    | yes        | Has to be unique per message and match the file name of `invoice` |

- `invoice` - i.e. the data of the file are:
  - file name - must correspond to the value at position `jointInvoiceHeadersList.object.fileName` so that the system can match the file and its header together. Eg "joint_invoice.xml"
  - file content - e-invoice XML encoded in base64 format

#### Additional rules

- There must be a valid joint invoice agreement between the sender and the recipient, the validity of which covers the validity of the joint invoice.
- There must be exactly the same amount of headers and files in the message

#### Example messages

Since the `joint-invoice` message is in the `multipart/form-data` format, the sample messages below are not in exact but pseudo structure to convey the rules and logic of message delivery.

<details>

<summary>Example "One metering point, one invoice"</summary>

```json
"marketParticipantContext": {
    "marketParticipantIdentification": "38X-EIN-GO-----0",
    "marketParticipantRole": "GRID_OPERATOR",
    "commodityType": "ELECTRICITY"
},
"jointInvoiceHeadersList": [
    {
        "senderEic": "38X-EIN-GO-----0",
        "receiverEic": "38X-EIN-OS-----J",
        "customerEic": "38X-AVP-ZW6700C6",
        "commodityType": "ELECTRICITY",
        "meterEics": [
            "38ZGO-1000006K-N",
        ],
        "dataPeriodStart": "2024-10-23T00:00:00+03:00",
        "dataPeriodEnd": "2024-10-24T00:00:00+03:00",
        "fileName": "joint_invoice_1.xml"
    }
],
"invoiceList": [
    {
        filename="joint_invoice_1.xml"

        PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPEVfSW52b2ljZSB4bWxuczp4c2k9Imh0dHA6Ly93d3cudzMub3JnLzIwMDEvWE1MU2NoZW1hLWluc3RhbmNlIiB4c2k6bm9OY
        W1lc3BhY2VTY2hlbWFMb2NhdGlvbj0iZS0KaW52b2ljZV92ZXIxLjExLnhzZCI+CjwvRV9JbnZvaWNlPg==
    }
]
```

</details>

<details>

<summary>Example "Multiple metering points on one invoice"</summary>

```json
"marketParticipantContext": {
    "marketParticipantIdentification": "38X-EIN-GO-----0",
    "marketParticipantRole": "GRID_OPERATOR",
    "commodityType": "ELECTRICITY"
},
"jointInvoiceHeadersList": [
    {
        "senderEic": "38X-EIN-GO-----0",
        "receiverEic": "38X-EIN-OS-----J",
        "customerEic": "38X-AVP-ZW6700C6",
        "commodityType": "ELECTRICITY",
        "meterEics": [
            "38ZGO-1000006K-N",
            "38ZGO-1000006P-8"
        ],
        "dataPeriodStart": "2024-10-23T00:00:00+03:00",
        "dataPeriodEnd": "2024-10-24T00:00:00+03:00",
        "fileName": "joint_invoice_1.xml"
    }
],
"invoiceList": [
    {
        filename="joint_invoice_1.xml"

        PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPEVfSW52b2ljZSB4bWxuczp4c2k9Imh0dHA6Ly93d3cudzMub3JnLzIwMDEvWE1MU2NoZW1hLWluc3RhbmNlIiB4c2k6bm9OY
        W1lc3BhY2VTY2hlbWFMb2NhdGlvbj0iZS0KaW52b2ljZV92ZXIxLjExLnhzZCI+CjwvRV9JbnZvaWNlPg==
    }
]
```

</details>

<details>

<summary>Example "Multiple invoices"</summary>

```json
"marketParticipantContext": {
    "marketParticipantIdentification": "38X-EIN-GO-----0",
    "marketParticipantRole": "GRID_OPERATOR",
    "commodityType": "ELECTRICITY"
},
"jointInvoiceHeadersList": [
    {
        "senderEic": "38X-EIN-GO-----0",
        "receiverEic": "38X-EIN-OS-----J",
        "customerEic": "38X-AVP-ZW6700C6",
        "commodityType": "ELECTRICITY",
        "meterEics": [
            "38ZGO-1000006K-N"
        ],
        "dataPeriodStart": "2024-10-23T00:00:00+03:00",
        "dataPeriodEnd": "2024-10-24T00:00:00+03:00",
        "fileName": "joint_invoice_1.xml"
    },
    {
        "senderEic": "38X-EIN-GO-----0",
        "receiverEic": "38X-EIN-OS-----J",
        "customerEic": "38X-AVP-V8JG00C9",
        "commodityType": "ELECTRICITY",
        "meterEics": [
            "38ZGO-10000030-L",
            "38ZGO-10000031-I",
            "38ZGO-10000032-F"
        ],
        "dataPeriodStart": "2024-10-01T00:00:00+03:00",
        "dataPeriodEnd": "2024-11-01T00:00:00+03:00",
        "fileName": "joint_invoice_2.xml"
    }
],
"invoiceList": [
    {
        filename="joint_invoice_1.xml"

        PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPEVfSW52b2ljZSB4bWxuczp4c2k9Imh0dHA6Ly93d3cudzMub3JnLzIwMDEvWE1MU2NoZW1hLWluc3RhbmNlIiB4c2k6bm9OY
        W1lc3BhY2VTY2hlbWFMb2NhdGlvbj0iZS0KaW52b2ljZV92ZXIxLjExLnhzZCI+CjwvRV9JbnZvaWNlPg==
    },
    {
        filename="joint_invoice_2.xml"

        PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPEVfSW52b2ljZSB4bWxuczp4c2k9Imh0dHA6Ly93d3cudzMub3JnLzIwMDEvWE1MU2NoZW1hLWluc3RhbmNlIiB4c2k6bm9OY
        W1lc3BhY2VTY2hlbWFMb2NhdGlvbj0iZS0KaW52b2ljZV92ZXIxLjExLnhzZCI+CjwvRV9JbnZvaWNlPg==
    },
]
```

</details>

### Find and download joint invoice

Separate services have been created to search and download a joint invoice. The search API returns invoice IDs that can be used in the download service.

Joint invoices can also be searched and downloaded via the user interface.

#### Attribute specific rules

It is possible to search for joint invoices based on various characteristics:

| Attribute       | Description                                                                       | Mandatory? | Other rules                                      |
|-----------------|-----------------------------------------------------------------------------------|------------|--------------------------------------------------|
| invoiceId       | ID of the file received in response during joint invoice addition                 | no         | Allows to search for a specific joint invoice    |
| commodityType   | Commodity type                                                                    | yes        | One of them: ELECTRICITY, NATURAL_GAS            |
| createdTimeFrom | Joint invoice creation time from                                                  | yes        |                                                  |
| createdTimeTo   | Joint invoice creation time to                                                    | yes        | Must be greater than `createdTimeFrom`           |
| senderEic       | EIC code of the sender                                                            | no         |                                                  |
| receiverEic     | EIC code of the receiver                                                          | no         |                                                  |
| customerEic     | EIC code of the customer of the metering point                                    | no         |                                                  |
| meterEics       | EIC code(s) of metering point(s)                                                  | no         |                                                  |
| dataPeriodStart | Beginning of the billing period of the joint invoice                              | no         |                                                  |
| dataPeriodEnd   | End of the billing period of the joint invoice                                    | no         | If given, must be greater than `dataPeriodStart` |
| unread          | Has the joint invoice been previously downloaded once by the **addressee** or not | no         |                                                  |

Example message:

```bash
curl -X POST -H "Content-Type: multipart/form-data" \
  -F "invoiceList=@file1.xml" \
  -F "invoiceList=@file2.xml" \
  -F "jointInvoiceHeadersList=[{\"senderEic\":\"38X-AVP-8T8D00EC\",\"receiverEic\":\"38X-AVP-1G0G00E7\",\"customerEic\":\"38X-PP-03712673A\",\"commodityType\":\"ELECTRICITY\",\"meterEics\":[\"38Z-EE-CS-0041-X\",\"38Z-EE-CS-004Z-5\"],\"dataPeriodStart\":\"2023-10-03T22:00:00Z\",\"dataPeriodEnd\":\"2023-11-06T23:00:00Z\",\"fileName\":\"file1\"},{\"senderEic\":\"38X-AVP-8T8D00EC\",\"receiverEic\":\"38X-AVP-1G0G00E7\",\"customerEic\":\"38X-PP-03712673A\",\"commodityType\":\"ELECTRICITY\",\"meterEics\":[\"38Z-EE-CS-0041-X\",\"38Z-EE-CS-004Z-5\"],\"dataPeriodStart\":\"2023-10-03T22:00:00Z\",\"dataPeriodEnd\":\"2023-11-06T23:00:00Z\",\"fileName\":\"file2\"}]" \
  -F "marketParticipantContext={\"marketParticipantIdentification\":\"38X-AVP-UQLB00EB\",\"marketParticipantRole\":\"GRID_OPERATOR\",\"commodityType\":\"ELECTRICITY\"}" \
  {{restHost}}/api/v1/joint-invoice
```

The response contains the ID of the joint invoice file (`invoiceId`), which can be used as input to `POST /api/{version}/joint-invoice/download`

#### Additional rules

- If the searcher for joint invoices is a grid operator or a closed distribution network operator, only those network invoices will be returned where the sender of the request is the sender (allows you to search for joint invoices sent by yourself)
- If the searcher for joint invoices is an open supplier, only those joint invoices are returned where the sender of the request is the receiver.
- If the joint invoice is downloaded by the receiver, the invoice is marked as read (`unread = false`).
