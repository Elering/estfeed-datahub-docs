# General service notice

## Table of contents

<!-- TOC -->
* [General service notice](#general-service-notice)
  * [Table of contents](#table-of-contents)
  * [Introduction](#introduction)
  * [General Service Notification Messages](#general-service-notification-messages)
<!-- TOC -->

## Introduction

Datahub identifies all periods, where the customer is or will be using the general service. Datahub also identifies sub-periods inside those periods, that are covered with named supplier agreement. 
Datahub will create general service (`GENERAL_SERVICE`) agreements for all those identified (sub)periods and sets the grid operator or named supplier as the service provider:

![general-service.svg](../diagrams/general-service/general-service.svg)

This solution is purely technical, to store the start and end date of the general service in more explicit manner. Those agreements are not legally valid agreements.

Datahub makes the general service agreements available to the grid operator and to the named supplier via the `data-distribution/search` service right after their activation. **General service agreements, that activate in the future, are not distributed** nor can they be found via regular agreement searches. Read more about the data distribution GENERAL_SERVICE agreements on page [Data Distribution](30-data-distribution.md)

> [!NOTE]
> The Datahub doesn't track the changes of the GENERAL_SERVICE agreements. In case of any changes the old agreements are deleted and new ones created

Upon the activation of the general service, further data exchange will depend on whether the grid operator has a named supplier agreement or not:

- If not, no additional data exchange is foreseen.
- If so, the Datahub will allow the grid operator ja named supplier to exchange customer's meta- and billing data updates using the `PUT customer` service.

> [!NOTE]
> In this process, the Datahub is acting only as data exchanger. Using the service is purely optional.

## General Service Notification Messages

Since there is no change detection for general service agreements, the data distribution channel does not include messages for general service agreements where the `reason` attribute would have the value `UPDATE`. Only the values `CREATE` and `DELETE` exist.

**Example "New GRID Agreement":**

- The grid operator (GO) creates a new GRID agreement.
- If the start date of the GRID agreement is in the future, no GENERAL_SERVICE agreement distribution follows.
- If the start date of the GRID agreement is today or in the past, then the GO receives a GENERAL_SERVICE agreement notification, where:
  - The `reason` value is `CREATE`
  - The `validFrom` and `validTo` values are identical to the `validFrom` and `validTo` values of the GRID agreement (since there are no SUPPLY agreements).

Diagram:

![general-service-ex-1-eng.svg](../diagrams/general-service/general-service-ex-1-eng.svg)

**Example "New SUPPLY Agreement with a start in the past and end in the future or undefined":**

This example illustrates the business rule for the SUPPLY agreement: "The start date of the agreement may be up to 48h in the past if the open supplier registers the open supply agreement afterwards and the start date of the agreement coincides with the start date of the grid agreement."

- The customer currently has valid GRID and GENERAL_SERVICE agreements for the metering point.
- The OS creates a new SUPPLY agreement, with a `validFrom` in the past that matches the `validFrom` of the GRID agreement, and with a `validTo` in the future or undefined.
- The Datahub identifies that the previously created GENERAL_SERVICE agreement is no longer valid and deletes it.
- The GO receives a GENERAL_SERVICE agreement distribution message, where:
  - The `reason` value is `DELETE`
  - The `validFrom` and `validTo` values are identical to the previous notification (allowing the GO to locate the GENERAL_SERVICE agreement).

Diagram:

![general-service-ex-2-eng.svg](../diagrams/general-service/general-service-ex-2-eng.svg)

**Example "New SUPPLY Agreement with both start and end in the future":**

- The customer currently has valid GRID and GENERAL_SERVICE agreements for the metering point.
- The OS creates a new SUPPLY agreement with a `validFrom` in the future.
- The Datahub identifies that the existing GENERAL_SERVICE agreement is no longer valid and deletes it.
- The Datahub creates a new GENERAL_SERVICE agreement, where: the `validFrom` matches the `validFrom` value of the deleted GENERAL_SERVICE agreement, and `validTo` matches the `validFrom` of the SUPPLY agreement.
- The GO receives two notifications for the GENERAL_SERVICE agreement:
  - Notification 1:
    - The `reason` value is `DELETE`
    - The `validFrom` and `validTo` values are identical to the previous notification (allowing the GO to locate the GENERAL_SERVICE agreement).
  - Notification 2:
    - The `reason` value is `CREATE`
    - The `validFrom` matches the `validFrom` in the `DELETE` message
    - The `validTo` matches the `validFrom` of the SUPPLY agreement.
- Additionally, a standard notification about the addition of the SUPPLY agreement is sent.

Diagram:

![general-service-ex-3-eng.svg](../diagrams/general-service/general-service-ex-3-eng.svg)

**Example "New SUPPLY Agreement with a start in the past and an end in the past":**

This example illustrates the business rule for the SUPPLY agreement: "The start date of the agreement may be up to 48h in the past if the open supplier registers the open supply agreement afterwards and the start date of the agreement coincides with the start date of the grid agreement." This also depicts a highly unlikely situation, such as a one-day SUPPLY agreement in the past.

- The customer currently has valid GRID and GENERAL_SERVICE agreements for the metering point.
- The OS creates a new SUPPLY agreement with a `validFrom` in the past that matches the `validFrom` of the GRID agreement, and a `validTo` in the past (an extreme example of a one- or two-day agreement).
- The Datahub identifies that the current GENERAL_SERVICE agreement is no longer valid and deletes it.
- The Datahub creates a new GENERAL_SERVICE agreement, where `validFrom` matches the `validTo` of the SUPPLY agreement.
- The GO receives two notifications for the GENERAL_SERVICE agreement:
  - Notification 1:
    - The `reason` value is `DELETE`
    - The `validFrom` and `validTo` values are identical to the previous notification (allowing the GO to locate the GENERAL_SERVICE agreement).
  - Notification 2:
    - The `reason` value is `CREATE`
    - The `validFrom` matches the `validTo` of the SUPPLY agreement.
    - The `validTo` is missing.
- Additionally, a standard notification about the addition of the SUPPLY agreement is sent.

Diagram:

![general-service-ex-4-eng.svg](../diagrams/general-service/general-service-ex-4-eng.svg)

**Example "Addition of a NAMED_SUPPLIER Agreement":**

- The customer currently has valid GRID and GENERAL_SERVICE agreements for the metering point.
- The GO creates a new NAMED_SUPPLIER agreement with a `validFrom` in the future.
- The Datahub identifies that the existing GENERAL_SERVICE agreement is no longer valid because the service provider has changed and deletes it.
- The Datahub creates a new GENERAL_SERVICE agreement, where: the `validFrom` matches the `validFrom` value of the deleted GENERAL_SERVICE agreement, and the `validTo` matches the `validFrom` of the NAMED_SUPPLIER agreement.
- The GO receives two notifications for the GENERAL_SERVICE agreement:
  - Notification 1:
    - The `reason` value is `DELETE`
    - The `validFrom` and `validTo` values are identical to the previous notification (allowing the GO to locate the GENERAL_SERVICE agreement).
  - Notification 2:
    - The `reason` value is `CREATE`
    - The `validFrom` matches the `validFrom` in the `DELETE` message.
    - The `validTo` matches the `validFrom` of the NAMED_SUPPLIER agreement.

> [!NOTE]
> Although the Datahub also creates a future GENERAL_SERVICE agreement, no notification is generated as it has not yet become active.

Diagram:

![general-service-ex-5-eng.svg](../diagrams/general-service/general-service-ex-5-eng.svg)
