# Metering data

## Table of contents

<!-- TOC -->
* [Metering data](#metering-data)
  * [Table of contents](#table-of-contents)
  * [Introduction](#introduction)
  * [Transmitting metering data](#transmitting-metering-data)
    * [Transmitting metering data via the web interface](#transmitting-metering-data-via-the-web-interface)
    * [API messages](#api-messages)
      * [Messages](#messages)
      * [Message rules](#message-rules)
  * [Metering data requests](#metering-data-requests)
    * [Requesting metering data via the web interface](#requesting-metering-data-via-the-web-interface)
    * [API messages](#api-messages-1)
      * [Messages](#messages-1)
      * [Message rules](#message-rules-1)
<!-- TOC -->

## Introduction

Metering data is the predicted or measured active energy consumption data associated with a specific metering point over a given period of time. Metering data is the basis for billing and is provided by metering point operators and used by other market participants (mainly open suppliers).

## Transmitting metering data

The metering point operator determines the active energy amounts in its metering points and transmits two-way hourly active energy amount data to the Datahub.

The aggregator transmits the energy quantities of demand response management.

Metering point operators transmit metering data per metering point under the following conditions:

1. for those metering points where data are read remotely, the initial metering data are transmitted to the Datahub by 10:00 every working day;
2. the final metering data for the calendar month at the metering points where data are read remotely are transmitted to the Datahub by the 5th day of the following month.

The amounts of grid and line losses are calculated by the Datahub.

The grid operator is the manager of load duration curves and responsible for the transmission of hourly amounts to the Datahub.

Grid operators and line operators can transmit metering data of metering points to the Datahub via a web interface by mass upload or by automatic data exchange message.

Relevant Datahub services have been set up to transmit metering data. The intended use process is as follows:

- The metering point operators sends a new or changed metering data message using the `meter-data` service.
- Since the processing of metering data in the Datahub is asynchronous, the Datahub first gives a quick response whether the message was received or not.
- The Datahub then queues the message.
- The metering point operator verifies the result of processing, using `meter-data/status` service (at the `originalDocumentIdentification` position of the message, the value of the attribute of the same name that was in the `header` of the previously transmitted metering data message must be transmitted. The UUID value must not be reused). Possible results are:
  - `PROCESSING` - processing not finished
  - `SUCCESSFUL` - processing finished successfully
  - `ÈRROR` - processing finished with errors.
- If the message is processed without errors, then the data are added or changed in the database and the Datahub makes the addition or change of metering data available to open suppliers through the `data-distribution/search` service. For more details, see [Data distribution](30-data-distribution.md).
- If errors occur while processing the message, the Datahub will generate an error report and make it available to the metering point operator in the response of the  `meter-data/status` service.
- The metering point operator reads the error report addressed to it and resolves it according to its internal business logic.

> [!WARNING]
> **PLEASE NOTE! The Datahub transmits the metering data entered by the grid operators in unaltered form. The Datahub does not check the content of the metering data.**

### Transmitting metering data via the web interface

In order to transmit data via the web interface user will need to navigate to "Metering data" page.

For easier metering data transmitting it is possible to download the template. To generate the template the resolution and time range needs to be selected, based on it the prefilled template is generated. It is important to choose the time range correctly - it needs to fit the resolution.

![Generating the template](../images/opp-ui/metering-data/metering-data-template1.png)

![Filling in the template](../images/opp-ui/metering-data/metering-data-template2.png)

To import metering data "Import" button needs to be clicked on the "Metering data" page. After that it is possible to add the metering data file. 

![Metering data import](../images/opp-ui/metering-data/metering-data-import.png)

In case there is a mistake in the file the system will notify the user:
1. Metering data can be added to several MS Excel file sheets. The system will tell the user on which sheet the problem is located.
2. In addition, it is possible to see the row where the problem is.
3. Error description helps to understand the issue.
4. After the problem is found and fixed "Cancel" should be clicked and import process should be repeated.

![Import error](../images/opp-ui/metering-data/metering-data-error.png)

### API messages

In the new Datahub, the ‘pos’ or ‘position’ attribute has been removed. The transmitter of metering data must define in the message the beginning of the period (pS) and the resolution (r), i.e. the frequency of data reading:

```json
"periods": [
  {
    "r": "PT1H",
    "aI": [
      {
        "pS": "2023-09-04T12:00:00.000Z",
        "inQty": {
          "rTime": "2023-09-04T12:48:13.368Z",
          "rType": "E",
          "kwh": 0
        },
        "outQty": {
          "rTime": "2023-09-04T12:48:13.368Z",
          "rType": "M",
          "kwh": 5
        }
      }
    ]
  }
]
```

Explanation of abbreviations used in the API service:

* r – resolution
* aI – account interval (interval of one reading result)
* pS – period start
* inQty – IN or the reading result of incoming energy
* outQty – OUT or the reading result of outgoing energy
* rTime – reading time
* rType – reading Type (E – estimated, M – read)

The Datahub does not check whether every one hour or 15 minute interval is filled with metering data. 

> [!NOTE] 
> The resolution of the data is rigidly fixed by the Datahub – for both electricity and gas, the resolution is one hour. In 2024, electricity will switch to the 15-minute resolution.
> 
> In the case of gas, it is also allowed to transmit daily data. In this case, the daily metering data must be added to the suitable gas day hour.

#### Messages

| Message                                   | Objective                                                           |
|-------------------------------------------|---------------------------------------------------------------------|
| `POST /api/{version}/meter-data`          | Create or update meter reading data                                 |
| `POST /api/{version}/meter-data/status`   | Find meter data processing status                                   |
| `POST /api/{version}/meter-data/import`   | Bulk import of metering data                                        |
| `POST /api/{version}/template/meter-data` | Generate and download the template for bulk import of metering data |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

> [!NOTE]
> A collection of sample messages is being created

#### Message rules

- The resolution value must match the global resolution applied in the given time period. For example, if the entire market switches to a resolution of 15 minutes on date X, then for metering data from date X the resolution value must be 15 minutes in the message.
- The time period value must be consistent with the resolution. For example:
  - if the resolution is one hour, the start time of the period must be the beginning of the hour (hh:00);
  - if the resolution is 15 minutes, the start time of the period must be a quarter of the hour (hh:00, hh:15, hh:30, hh:45).
- Electricity metering data are always transmitted in kWh up to three decimal places. 
- Gas metering data are transmitted in both kWh and cubic metres to three decimal places.
- The direction of the metering data is always presented as viewed by the metering point operator:
  - in – energy entering the grid (generation);
  - out – energy leaving the grid (consumption).
- The amounts of incoming and outgoing energy can also be transmitted in separate messages.
- It is permitted to correct metering data retroactively for up to 12 months.
- The `import` service requires the same template, that the service `export` returns.

> [!NOTE]
> The rights for transmitting and requesting data are described in [Authentication and authorisation](03-authentication-and-authorisation.md)

## Metering data requests

Relevant Datahub services have been set up to transmit metering data. Access to data is limited. The rules are described in [Authentication and authorisation](03-authentication-and-authorisation.md).

The following options are available for making metering data requests:

- Open suppliers can scan metering data changes using the `data-distribution/search` service.
- Authorised users can request metering data using the `search` service.

### Requesting metering data via the web interface

Metering data can be requested by navigating to "Metering data" page. There metering point EIC code and search period start need to be defined. If needed the end date can be added as well. 

![Searching metering data](../images/opp-ui/metering-data/metering-data-search.png)

### API messages

#### Messages

| Message                                 | Objective         |
|-----------------------------------------|-------------------|
| `POST /api/{version}/meter-data/search` | Find meter data   |
| `POST /api/{version}/meter-data/export` | Export meter data |

For a description of message structures and validations, see [Datahub description and general principles for data exchange](01-datahub-description-and-general-principles-for-data-exchange.md)

> [!NOTE]
> A collection of sample messages is being created

#### Message rules

- When searching for the Metering Data, the Market Participant can define the observation type and time. Following options are available:
  - READING_TIME - when observation time is provided, then system finds stored metering data by sent reading time values. 
  - SNAPSHOT_TIME - when observation time is provided, then system finds stored metering data by creation time in the Datahub.

> [!NOTE]
> The rights for transmitting and requesting data are described in [Authentication and authorisation](03-authentication-and-authorisation.md)
