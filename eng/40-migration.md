﻿# Migrating from the old system to the new

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

| Old XML service              | New REST service                                                                                |
|------------------------------|-------------------------------------------------------------------------------------------------|
| RequestCustomerEIC           | `POST` `/api/{version}/customer`                                                                |
|                              | `POST` `/api/{version}/customer/search`                                                         |
| NotifyMeteringPointData      | `POST` and `PUT` `/api/{version}/meter`                                                         |
|                              | `POST` and `PUT` `/api /{version}/agreement` where `agreementType = GRID`                       |
| NotifyGridAgreementChange    | `POST` `/api /{version}/data-distribution/search` where `resourceType = AGREEMENT`              |
| RequestMeteringPointsData    | `POST` `/api/{version}/meter/search/customer`                                                   |
| NotifySupplyAgreement        | `POST` and `PUT` `/api /{version}/agreement` where `agreementType = SUPPLY`                     |
| EnergyReport                 | `POST` `/api/{version}/meter-data`                                                              |
| EnergyReportResult           | `POST` `/api /{version}/meter-data/status`                                                      |
| NetworkBill                  | `POST` `/api/{version}/network-bill`                                                            |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = NETWORK_BILL`           |
| RequestMeteringDataHistory   | `POST` `/api/{version}/meter-data/search`                                                       |
| NotifyCustomerAuthorization  | `POST` `/api/customer-authorization/search`                                                     |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = CUSTOMER_AUTHORIZATION` |
| CustomerMetadata             | *The service is under development*                                                              |
| NotifyJointInvoiceAgreement  | `POST` and `PUT` `/api /{version}/agreement` where `agreementType = JOINT_INVOICE`              |
| NotifyPortfolioAgreement     | `POST` and `PUT` `/api /{version}/agreement` where `agreementType = PORTFOLIO_SUPPLIER`         |
| NotifyNamedSupplierAgreement | `POST` and `PUT` `/api /{version}/agreement` where `agreementType = NAMED_SUPPLIER`             |
| RequestAgreementCoordination | *The service is under development*                                                              |
| ReplyAgreementCoordination   | *The service is under development*                                                              |
| ConfirmAgreementCoordination | *The service is under development*                                                              |
| ForwardInvoice               | `POST` `/api/{version}/joint-invoice`                                                           |
|                              | `POST` `/api/{version}/joint-invoice/download`                                                  |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = JOINT_INVOICE`          |
| RequestConnectionState       | `POST` `/api/{version}/connection-state/initiate`                                               |
|                              | `POST` `/api/{version}/connection-state/message`                                                |
|                              | `POST` `/api/{version}/connection-state/message-history`                                        |
|                              | `POST` `/api/{version}/connection-state/search`                                                 |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = CONNECTION_STATE`       |
| ReplyRequestConnectionState  | `POST` `/api/{version}/connection-state/message`                                                |
|                              | `POST` `/api/{version}/connection-state/message-history`                                        |
|                              | `POST` `/api/{version}/connection-state/search`                                                 |
|                              | `POST` `/api /{version}/data-distribution/search` where `resourceType = CONNECTION_STATE`       |
| SendMessage                  | *The service is under development*                                                              |
| BalanceState                 | *The service is under development*                                                              |
| AggregatedMeteringDataReport | *The service is under development*                                                              |
| Report                       | *The service is under development*                                                              |

Information about development and deployment deadlines of all API-s can be found [here](50-roadmap.md)

## Added functionality

Compared to the previous Datahub, the new Datahub has the following new functionalities already developed or under development:

- A new agreement type has been added: [Aggregation agreement](05.6-aggregation-agreement.md).
- Adding and updating a customer is separated from agreement.
- There is a new concept of a master metering point.
- The processing of metering data can be asynchronous.
- Location data now include ADS’s ADR_ID and comment.
- A 15 min resolution has been added to reading resolutions.
- There are new customer types: ENERGY_STORAGE_UNIT, CHARGING_POINT_OPERATOR.
- The existence and type of production: SOLAR, WIND, HYDRO, BIOGAS, BIOMASS, NATURAL_GAS, OIL_SHALE, OTHER_RENEWABLE, OTHER_NON_RENEWABLE.
- Numerical values: storage capacity (storageCapacity), storage energy (storageEnergy), production capacity (productionCapacity) and transmission capacity (transmissionCapacity).
- Transmission grid substation
- Apartment association ID
- Charging point ID
- The resolution of metering data is fixed by energy type in the application configuration and can no longer be controlled in metering data messages.
- When transmitting metering data, it is no longer necessary to calculate or transmit the ‘pos’ value. Instead, a combination of period start time plus resolution is used.
- Definitions of border metering point (BORDER) and border metering point agreement (BORDER_GRID) have been added.
- Joint Invoice billing metadata can be added as Customer metadata.
- Datahub now generates GENERAL_SERVICE agreements automatically and distributes this knowledge to grid operator and named supplier
- Added support for technical users in the API authentication and authorization.