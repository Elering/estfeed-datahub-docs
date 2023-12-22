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

| Old XML service              | Is included in the MVP scope | New REST service                         |
|------------------------------|-----------------------|-----------------------------------------|
| RequestCustomerEIC           | MVP                   | `/api/{version}/customer`               |
| NotifyMeteringPointData      | MVP                   | `/api/{version}/meter`                  |
| NotifyGridAgreementChange    | MVP                   | `/api /{version}/agreement`             |
| RequestMeteringPointsData    | MVP                   | `/api/{version}/meter/search/customer`  |
| NotifySupplyAgreement        | MVP                   | `/api /{version}/agreement`             |
| EnergyReport                 | MVP                   | `/api/{version}/meter-data`             |
| EnergyReportResult           | MVP                   | `/api/{version}/meter-data/change`      |
| NetworkBill                  | MVP                   | `/api/{version}/network-bill`           |
| RequestMeteringDataHistory   | MVP                   | `/api/{version}/meter-data/search`      |
| NotifyCustomerAuthorization  | MVP                   | `/api/customer-authorization`           |
| CustomerMetadata             | MVP                   | *The service is under development*             |
| NotifyJointInvoiceAgreement  | MVP                   | `/api/{version}/agreement`              |
| NotifyPortfolioAgreement     | MVP                   | `/api /{version}/agreement`             |
| NotifyNamedSupplierAgreement | MVP                   | `/api /{version}/agreement`             |
| RequestAgreementCoordination | -                     | `/api/{version}/agreement-coordination` |
| ReplyAgreementCoordination   | -                     | `/api/{version}/agreement-coordination` |
| ConfirmAgreementCoordination | -                     | `/api/{version}/agreement-coordination` |
| ForwardInvoice               | MVP                   | `/api/{version}/joint-invoice`          |
| RequestConnectionState       | -                     | `/api/{version}/connection-state`       |
| ReplyRequestConnectionState  | -                     | `/api/{version}/connection-state`       |
| SendMessage                  | -                     | `/api/{version}/direct-message`         |
| BalanceState                 | MVP                   | `/api/{version}/balance-state`          |
| AggregatedMeteringDataReport | MVP                   | *The service is under development*             |
| Report                       | -                     | *The service is under development*             |

## Added functionality

Compared to the previous Datahub, the new Datahub has the following new functionalities already developed or under development:

- A new agreement type has been added: [Aggregation agreement](05.6-aggregation-agreement.md).
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