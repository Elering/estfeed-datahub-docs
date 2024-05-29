# Business processes

## Table of contents

- [Business processes](#business-processes)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Metering point management](#metering-point-management)
    - [Register new metering point](#register-new-metering-point)
    - [Update metadata of a metering point](#update-metadata-of-a-metering-point)
  - [Customer management](#customer-management)
    - [Register new customer](#register-new-customer)
    - [Update metadata of a customer](#update-metadata-of-a-customer)
  - [Agreement management](#agreement-management)
    - [Register new grid agreement](#register-new-grid-agreement)
    - [Register new open supply agreement](#register-new-open-supply-agreement)
    - [Generate and distribute general service agreements](#generate-and-distribute-general-service-agreements)
    - [Exchange customer's billing information from grid operator to named supplier](#exchange-customers-billing-information-from-grid-operator-to-named-supplier)
  - [Connecting to and disconnecting from the grid](#connecting-to-and-disconnecting-from-the-grid)
    - [Disconnecting](#disconnecting)
    - [Reconnecting](#reconnecting)
  - [Joint invoice management](#joint-invoice-management)
    - [Add joint invoice](#add-joint-invoice)
    - [Update joint invoice](#update-joint-invoice)
  - [Network bill management](#network-bill-management)
    - [Add network bill](#add-network-bill)
    - [Update network bill](#update-network-bill)

## Introduction

This document describes the main Datahub related business processes and thereby tries to give an overview about the connection between different API-s and business processes.

The diagrams are composed in an object-oriented way, where complex processes reuse simpler processes. For example, the process "Register new grid agreement" reuses the following processes:

- Register new customer
- Update metadata of a customer
- Register new metering point

Indicator for reused process is:

![Reusable process marking](../diagrams/reusable-process-marking.png)

## Metering point management

### Register new metering point

![Register new metering point](../diagrams/metering-point-management/register-new-metering-point.svg)

### Update metadata of a metering point

![Update metadata of metering point](../diagrams/metering-point-management/update-metadata-of-metering-point.svg)

## Customer management

### Register new customer

![Register new customer](../diagrams/customer-management/register-customer.svg)

### Update metadata of a customer

![Update metadata of customer](../diagrams/customer-management/update-metadata-of-customer.svg)

## Agreement management

### Register new grid agreement

![Register new grid agreement](../diagrams/agreement-management/register-new-grid-agreement.svg)

### Register new open supply agreement

![Register new open supply agreement](../diagrams/agreement-management/register-new-open-supply-agreement.svg)

### Generate and distribute general service agreements

Business process:

![Generate and distribute general service agreements](../diagrams/agreement-management/generate-and-distribute-general-service-agreements.svg)

Additional diagram, that helps to clarify how general service agreements are generated:

![Additional info](../diagrams/agreement-management/general-service-agreement-generation-additional-info.svg)

### Exchange customer's billing information from grid operator to named supplier

![Exchange customer's billing information from grid operator to named supplier](../diagrams/agreement-management/exchange-customer-billing-data.svg)

## Connecting to and disconnecting from the grid

### Disconnecting

![Disconnect](../diagrams/connection-state/disconnect.svg)

### Reconnecting

![Reconnect](../diagrams/connection-state/reconnect.svg)

## Joint invoice management

### Add joint invoice

![Add joint invoice](../diagrams/joint-invoice/add-joint-invoice.svg)

### Update joint invoice

*Process is under development*

## Network bill management

### Add network bill

![Add network bill](../diagrams/network-bill/add-network-bill.svg)

### Update network bill

![Update network bill](../diagrams/network-bill/update-network-bill.svg)