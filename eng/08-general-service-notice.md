﻿# General service notice

## Table of contents

- [General service notice](#general-service-notice)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)

## Introduction

Datahub identifies all periods, where the customer is or will be using the general service. Datahub also identifies sub-periods inside those periods, that are covered with named supplier agreement. 
Datahub will create general service (`GENERAL_SERVICE`) agreements for all those identified (sub)periods and sets the grid operator or named supplier as the service provider. 
This solution is purely technical, to store the start and end date of the general service in more explicit manner. Those agreements are not legally valid agreements.

Datahub makes the general service agreements available to the grid operator and to the named supplier via the `data-distribution/search` service. Read more about the data distribution on page [Data Distribution](30-data-distribution.md)

> [!NOTE]
> The Datahub doesn't track the changes of the GENERAL_SERVICE agreements. In case of any changes the old agreements are deleted and new ones created

Upon the activation of the general service, further data exchange will depend on whether the grid operator has a named supplier agreement or not:

- If not, no additional data exchange is foreseen.
- If so, the Datahub will allow the grid operator ja named supplier to exchange customer's meta- and billing data updates using the `PUT customer` service.

> [!NOTE]
> In this process, the Datahub is acting only as data exchanger. Using the service is purely optional.
