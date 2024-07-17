# Balance area

## Table of contents

- [Balance area](#balance-area)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Balance area message](#balance-area-message)
  - [API messages](#api-messages)
  - [Message rules](#message-rules)
  - [Attribute specific rules](#attribute-specific-rules)

## Introduction

In other words, a balance area is a portfolio of metering points. Each metering point must belong to a balance area. Belonging to the balance area is determined by who is the energy supplier for the metering point at a given time.

The rule for creating a balance area is as follows: the balance area of a balance responsible party is determined by the metering points of the balance settlement of the market participants in that balance area – this is a metering point where the balance responsible party of a market participant and the balance responsible party of the grid operator differ.

A balance responsible party has the rights and obligations of an open supplier in the Datahub. The supply chain of a balance responsible party consists of market participants who have an open supply agreement with the balance responsible party and other open suppliers and/or grid operators entered via portfolio agreements by the balance responsible party.

A balance responsible party sees the following data in the Datahub regarding its balance area:

1. Metering point EIC.
2. Customer EIC.
3. Metering point’s grid operator EIC.
4. Grid operator’s balance responsible party EIC.
5. If the metering point is in the supply chain of a balance responsible party: the EIC of the open supplier at the metering point and the EIC of the balance responsible party.
6. If the metering point is not in the supply chain of a balance responsible party then the open supplier at the metering point and the balance responsible party are not visible.
7. Period (start and end time of the open supply agreement).

A balance responsible party receives metering data from the Datahub as follows:

1. Metering data from those metering points that are in the open supply chain of the balance responsible party pursuant to agreements.
2. If the border metering points of the grid operator are the border metering points of the balance area of the balance responsible party, the information will also include metering data from those border metering points.

## Balance area message

Used to forward changes in the area of the balance responsible party to the balance responsible party and the system operator. The process for generating and transmitting a balance area change message is as follows:

- A new grid or open supply or portfolio agreement becomes active in the Datahub OR an existing grid or open supply or portfolio agreement expires (at midnight).
- The balance responsible party requests changes to the balance area at a convenient time using the `balance-settlement-point/change` service and specifying the date of changes.
- The Datahub calculates and returns the changes immediately. The message contains new metering points in the balance area *(ADDED)* or metering points removed from the balance area *(REMOVED)*.

## API messages

| Message                                               | Objective                                                                            |
|-------------------------------------------------------|--------------------------------------------------------------------------------------|
| `POST /api/{version}/balance-settlement-point/change` | Allows the user to search for the balance area changes                               |
| `POST /api/{version}/balance-settlement-point/search` | Allows the user to search for the balance settlement points for the requested period |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

## Message rules

- The service only responds to balance responsible parties (who have a portfolio agreement with the TSO). No data is issued to other portfolio providers in the balance tree.
- Only one day changes can be requested with a `change` message. To request changes of a longer period, the message must be sent several times with the date of the desired period.

> [!NOTE]
> The rights for transmitting and requesting data are described in [Authentication and authorisation](03-authentication-and-authorisation.md)

## Attribute specific rules

### Service `change`

| Attribute in the API | Explanation                                                  | Mandatory? | Other rules                                                                                                                                                 |
|----------------------|--------------------------------------------------------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| updatePeriodStart    | The date of the balance change                               | no         | Allows to search the changed on specific date. Sent time value is ignored by Datahub. If not provided, then Datahub will set the value to current timestamp |
| meteringPointActions | Type of change                                               | no         | On of: ADDED, REMOVED                                                                                                                                       |
| includeParticipants  | Whether the response should contain participants information | no         | If "true", then position `serviceProviders` is filled in the response                                                                                       |

### Service `search`

| Attribute in the API | Explanation                 | Mandatory? | Other rules                                                                                         |
|----------------------|-----------------------------|------------|-----------------------------------------------------------------------------------------------------|
| periodStart          | Start of the desired period | yes        | periodStart and periodEnd define the period for which the balance state metering points are desired |
| periodEnd            | End of the desired period   | yes        |                                                                                                     |
| meteringPointTypes   | Metering point types        | no         | REGULAR - regular metering point; BORDER - border metering point                                    |