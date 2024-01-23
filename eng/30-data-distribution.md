# Data distribution

## Table of contents

- [Data distribution](#data-distribution)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Scanning data updates](#scanning-data-updates)
  - [Distributing data updates](#distributing-data-updates)

## Introduction

For business processes to run successfully and smoothly, the integrated systems of market participants need to be aware of new and changed information.

For this, new information needs to be delivered to the systems of market participants. This document describes the technical solution for distributing data updates through the API interface.

## Scanning data updates

Unlike the old Datahub, the new Datahub does not send messages to integrated parties but requires the integrated system to check whether it has new messages. For this purpose, a dedicated update pulling API `/data-distribution/search ` has been created, which works in a standard way:

- The system of the integrated market participant sends a request defining time period and dataobject type(s).
- The Datahub finds previously created data distribution messages addressed to the Market Participant and where the attributes match with the search criteria.
- The Datahub returns new or changed data objects together with the reason of change.

The system of the integrated market participant scans the data distribution API at a suitable interval, taking into account the usual frequency of data object addition and changing:

- it is recommended that slowly added and changing data (e.g. metering points) are scanned 1-4 times a day;
- it is recommended that rapidly added and changing data (e.g. metering data) are scanned with the same frequency as data are added – for example, every hour or more frequently. This will help the Datahub cope better with peak loads.

## Distributing data updates

Elering’s team is discussing various technical solutions to enable more capable integrated systems to receive data updates faster and without scanning. A specific technical solution is still under development. Market participants will be informed in a timely and thorough manner when it is ready.
