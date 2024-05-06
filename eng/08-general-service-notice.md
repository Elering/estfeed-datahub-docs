# General service notice

## Table of contents

- [General service notice](#general-service-notice)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)

## Introduction

Datahub identifies all periods, where the customer is or will be using the general service. Datahub also identifies sub-periods inside those periods, that are covered with named supplier agreement. 
Datahub will create general service (`GENERAL_SERVICE`) agreements for all those identified (sub)periods and sets the grid operator or named supplier as the service provider. 
This solution is purely technical, to store the start and end date of the general service in more explicit manner. Those agreements are not legally valid agreements.

Datahub makes the general service agreements available to the grid operator and to the named supplier via the `data-distribution/search` service immediately after general service activation.
The response contains data of GENERAL_SERVICE agreement.

Upon the activation of the general service, further data exchange will depend on whether or not the grid operator has a named supplier agreement or not:

- If not, no additional data exchange is foreseen.
- If so, the Datahub will allow the grid operator to send customer's contact and billing metadata using the `customer` service.

> **Note**
> In this process, the Datahub is acting only as data exchanger. Using the service is purely optional.
