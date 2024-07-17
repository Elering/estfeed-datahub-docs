# Joint invoice

## Table of contents
<!-- TOC -->
* [Joint invoice](#joint-invoice)
  * [Table of contents](#table-of-contents)
  * [Introduction](#introduction)
  * [Transmitting requesting a network bill](#transmitting-requesting-a-network-bill)
  * [Web interface](#web-interface)
  * [API messages](#api-messages)
  * [API message rules](#api-message-rules)
    * [Create or update joint invoice](#create-or-update-joint-invoice)
      * [Attribute specific rules](#attribute-specific-rules)
      * [Additional rules](#additional-rules)
    * [Find and download joint invoice](#find-and-download-joint-invoice)
      * [Attribute specific rules](#attribute-specific-rules-1)
      * [Additional rules](#additional-rules-1)
<!-- TOC -->

## Introduction

The prerequisite for sending a joint invoice is a joint invoice agreement in the Datahub. For more information, see [Joint invoice agreement](14-joint-invoice.md)

The details of the joint invoice to be sent are taken from the e-invoice standard ([Estonian e-invoice guide](https://media.voog.com/0000/0042/1620/files/Eesti_e-arve_kirjelduse_juhend_E_arve_saatmine%20ja%20presenteeerimine%20pangas_ver_1_0.pdf)).

## Transmitting requesting a network bill

Joint invoices can be transmitted via both the API and the web interface (a form for small grid operators) and downloaded (for sellers).

Relevant Datahub services have been set up to transmit and request joint invoices. The intended use process can be found in [Business processes](02-business-processes.md#joint-invoice-management)

## Web interface

> [!NOTE]
> The web interface is being developed.

## API messages

| Message                                      | Objective                     | Description and rules                                               |
|----------------------------------------------|-------------------------------|---------------------------------------------------------------------|
| `POST /api/{version}/joint-invoice`          | Create/update a joint invoice | [Create or update joint invoice](#create-or-update-joint-invoice)   |
| `POST /api/{version}/joint-invoice/search`   | Find a joint invoice          | [Find and download joint invoice](#find-and-download-joint-invoice) |
| `POST /api/{version}/joint-invoice/download` | Download a joint invoice      | [Find and download joint invoice](#find-and-download-joint-invoice) |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

## API message rules

> [!NOTE]
> The rights for transmitting and requesting data are described in [Authentication and authorisation](03-authentication-and-authorisation.md)

### Create or update joint invoice

Joint invoice contains of 2 sections:

- `jointInvoiceHeader`
- `invoice`

The header contains the metadata and invoice contains the base64 of the joint invoice.

Joint invoices cannot be updated. In case of need for correction, the grid operator or closed distribution network operator will send new joint invoice message containing credit joint invoice XML and if needed a new joint invoice

#### Attribute specific rules

- Header data:

| Attribute       | Description                               | Mandatory? | Other rules                                                       |
|-----------------|-------------------------------------------|------------|-------------------------------------------------------------------|
| senderEic       | EIC code of the sender                    | yes        |                                                                   |
| receiverEic     | EIC code of the receiver                  | yes        |                                                                   |
| commodityType   | Commodity type                            | yes        | One of: ELECTRICITY, NATURAL_GAS                                  |
| customerEic     | EIC code of the customer                  | yes        |                                                                   |
| meterEics       | EIC code(s) of the metering point(s)      | yes        |                                                                   |
| dataPeriodStart | Start date and time of the invoice period | yes        |                                                                   |
| dataPeriodEnd   | End date and time of the invoice period   | yes        |                                                                   |
| fileName        | Name of the file on position "invoice"    | yes        | Has to be unique per message and match the file name of `invoice` |

#### Additional rules

- There must be a valid joint invoice agreement between the sender and the recipient, the validity of which covers the validity of the joint invoice.
- There must be a valid grid agreement between the sender and the customer, the validity of which covers the validity of the joint invoice.
- There must be a valid open supply agreement between the receiver and the customer, the validity of which covers the validity of the joint invoice.
- There must be exactly the same amount of headers and files in the message

### Find and download joint invoice

Separate services have been created to search and download a joint invoice. The search API returns invoice IDs that can be used in the download service.

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
