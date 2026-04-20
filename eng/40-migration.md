# Migrating from the old system to the new

## Table of contents

- [Migrating from the old system to the new](#migrating-from-the-old-system-to-the-new)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Comparison of data exchange interface services](#comparison-of-data-exchange-interface-services)
  - [Added functionality](#added-functionality)

## Introduction

This document has been created as a temporary tool for developers to help them manage the updates and version changes of the Datahub. After the migration to the new version of the Datahub, this document will become obsolete and will be removed from the repository.

## Comparison of data exchange interface services

The new Datahub uses a more modern REST data exchange interface. As a consequence, all the services of the data exchange interface will change. The table below compares old and new services.

| Old XML service              | New REST service                                                                        | Link to the API                                                                                      |
|------------------------------|-----------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| RequestCustomerEIC           | `POST` and `PUT` `/api/{version}/customer`                                              | [Customer EIC](04-customer-eic.md)                                                                   |
|                              | `POST` `/api/{version}/customer/search`                                                 | [Customer EIC](04-customer-eic.md)                                                                   |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = CUSTOMER_DATA`  | [Data distribution](30-data-distribution.md)                                                         |
| NotifyMeteringPointData      | `POST` and `PUT` `/api/{version}/meter`                                                 | [Metering point](05-metering-point.md)                                                               |
|                              | `POST` and `PUT` `/api/{version}/meter/import`                                          |                                                                                                      |
|                              | `POST` and `PUT` `/api /{version}/agreement` where `agreementType = GRID`               | [Agreements](06-agreements.md)                                                                       |
|                              | `POST` `/api /{version}/agreement/delete`                                               |                                                                                                      |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = METERING_POINT` | [Data distribution](30-data-distribution.md)                                                         |
| NotifyGridAgreementChange    | `POST` `/api /{version}/data-distribution/search` where `resourceType = AGREEMENT`      | [Data distribution](30-data-distribution.md)                                                         |
| RequestMeteringPointsData    | `POST` `/api/{version}/meter/search/customer`                                           | [Metering point](05-metering-point.md)                                                               |
|                              | `POST` `/api/{version}/agreement/search/meter`                                          | [Agreements](06-agreements.md)                                                                       |
| NotifySupplyAgreement        | `POST` and `PUT` `/api /{version}/agreement` where `agreementType = SUPPLY`             | [Agreements](06-agreements.md)                                                                       |
|                              | `POST` `/api /{version}/agreement/delete`                                               |                                                                                                      |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = AGREEMENT`      | [Data distribution](30-data-distribution.md)                                                         |
| EnergyReport                 | `POST` `/api/{version}/metering-data/natural-gas`                                       | [Metering data](12-metering-data.md)                                                                 |
|                              | `POST` `/api/{version}/metering-data/natural-gas/import`                                |                                                                                                      |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = METERING_DATA`  | [Data distribution](30-data-distribution.md)                                                         |
| EnergyReportResult           | `POST` `/api /{version}/meter-data/status`                                              | [Metering data](12-metering-data.md)                                                                 |
| NetworkBill                  | `POST` and `PUT` `/api/{version}/network-bill`                                          | [Network bill](13-network-bill.md)                                                                   |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = NETWORK_BILL`   | [Data distribution](30-data-distribution.md)                                                         |
| RequestMeteringDataHistory   | `POST` `/api/{version}/meter-data/search`                                               | [Metering data](12-metering-data.md)                                                                 |
| NotifyCustomerAuthorization  | `POST` `/api/customer-authorization/search`                                             | [Customer authorization](15-customer-authorization.md)                                               |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = PERMISSION`     | [Data distribution](30-data-distribution.md)                                                         |
| NotifyJointInvoiceAgreement  | `POST` and `PUT` `/api /{version}/agreement` where `agreementType = JOINT_INVOICE`      | [Agreements](06-agreements.md)                                                                       |
|                              | `POST` `/api /{version}/agreement/delete`                                               |                                                                                                      |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = AGREEMENT`      | [Data distribution](30-data-distribution.md)                                                         |
| NotifyPortfolioAgreement     | `POST` and `PUT` `/api /{version}/agreement` where `agreementType = PORTFOLIO_SUPPLIER` | [Agreements](06-agreements.md)                                                                       |
|                              | `POST` `/api /{version}/agreement/delete`                                               |                                                                                                      |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = AGREEMENT`      | [Data distribution](30-data-distribution.md)                                                         |
| NotifyNamedSupplierAgreement | `POST` and `PUT` `/api /{version}/agreement` where `agreementType = NAMED_SUPPLIER`     | [Agreements](06-agreements.md)                                                                       |
|                              | `POST` `/api /{version}/agreement/delete`                                               |                                                                                                      |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = AGREEMENT`      | [Data distribution](30-data-distribution.md)                                                         |
| RequestAgreementCoordination | *The service is under development*                                                      | -                                                                                                    |
| ReplyAgreementCoordination   | *The service is under development*                                                      | -                                                                                                    |
| ConfirmAgreementCoordination | *The service is under development*                                                      | -                                                                                                    |
| ForwardInvoice               | `POST` and `PUT` `/api/{version}/joint-invoice`                                         | [Joint invoice](14-joint-invoice.md)                                                                 |
|                              | `POST` `/api/{version}/joint-invoice/search`                                            |                                                                                                      |
|                              | `POST` `/api/{version}/joint-invoice/download`                                          |                                                                                                      |
| RequestConnectionState       | `POST` `/api/{version}/connection-state/initiate`                                       | [Connecting to and disconnecting from the grid](21-connection-to-and-disconnecting-from-the-grid.md) |
|                              | `POST` `/api/{version}/connection-state/search`                                         |                                                                                                      |
| ReplyRequestConnectionState  | `POST` `/api/{version}/connection-state/message`                                        |                                                                                                      |
|                              | `POST` `/api/{version}/connection-state/message-history`                                |                                                                                                      |
|                              | `POST` `/api/{version}/connection-state/search`                                         |                                                                                                      |
| SendMessage                  | *The service is under development*                                                      | -                                                                                                    |
| BalanceState                 | `POST /api/{version}/balance-settlement-point/change`                                   | [Balance area](10-balance-area.md)                                                                   |
| AggregatedMeteringDataReport | See section "Report"                                                                    | [Reports](20-reports.md)                                                                             |
| Report                       | `POST /api/{version}/report/search`                                                     | [Reports](20-reports.md)                                                                             |
|                              | `POST /api/{version}/report/export/xlsx`                                                | -                                                                                                    |
|                              | `POST /api/{version}/report/export/json`                                                | -                                                                                                    |

Information about development and deployment deadlines of all API-s can be found [here](50-roadmap.md)

## Added functionality

Compared to the previous Datahub, the new Datahub has the following differences:

- Adding and modifying a customer is independent of the contract. If the customer name has been changed in GAVP within the last two years, the name in Estfeed Datahub will remain valid. Unfortunately, it is not possible for us to determine which name is correct.  
- The technical data of the metering point has changed; read more about them [here](05-metering-points.md).  
- When submitting metering data, it is no longer necessary to calculate or submit the "pos" value. Instead, a combination of period start and resolution is used.  
- Separate definitions have been added for a border metering point (BORDER) and a border metering point contract (BORDER_GRID).  
- The ability has been added to submit billing-related data as customer metadata.  
- The data warehouse automatically generates GENERAL_SERVICE contracts and distributes this information to the grid operator and the designated supplier.  
- Support has been created for technical user accounts required to use the API.  
- The process for receiving and processing metering data has changed to asynchronous. The processing result can be queried from the service `/meter-data/status`.  
- Reports can be downloaded in JSON format, but not in XML format.  
- A single market participant can have multiple EIC code ranges.  
- Instead of _Billing sequence_, _reading time_ is now used. The GO can define the _reading time_ value when submitting metering data, and OS/NS can search for metering data based on this value.  
- Metering data can be downloaded from the web interface only one metering point at a time.