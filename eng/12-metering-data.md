# Metering data

## Table of contents

<!-- TOC -->
* [Metering data](#metering-data)
  * [Table of contents](#table-of-contents)
  * [Introduction](#introduction)
    * [Net measured metering data](#net-measured-metering-data)
    * [Examples of Net‑Metered Electricity Quantities](#examples-of-net-metered-electricity-quantities)
    * [Changes for web interface user](#changes-for-web-interface-user)
    * [Changes for API user](#changes-for-api-user)
  * [Transmitting metering data](#transmitting-metering-data)
    * [Throttling of metering data input](#throttling-of-metering-data-input)
    * [Transmitting metering data via the web interface](#transmitting-metering-data-via-the-web-interface)
    * [Transmitting metering data via Excel](#transmitting-metering-data-via-excel)
      * [Possible errors when filling out Excel](#possible-errors-when-filling-out-excel)
    * [API messages](#api-messages)
      * [Messages](#messages)
      * [Message rules](#message-rules)
  * [Metering data requests](#metering-data-requests)
    * [legalConsent](#legalconsent)
    * [Observation time type](#observation-time-type)
    * [Requesting metering data via the web interface](#requesting-metering-data-via-the-web-interface)
    * [API messages](#api-messages)
      * [Messages](#messages-1)
<!-- TOC -->

## Introduction

Metering data is the predicted or measured active energy consumption data associated with a specific metering point over a given period of time. Metering data is the basis for billing and is provided by metering point operators and used by other market participants (mainly open suppliers).

###  Net measured metering data

As of **01.08.2026** grid operators are required to set net measured metering data for bidirectional metering points to the Estfeed Datahub. The data must be calculated by the grid operator by subtracting consumption from production. Testing in the test environment is possible, if market participants admin does not have access to the test evironment then write to datahub@elering.ee to sign a test environment agreement with Elering.

### Examples of Net‑Metered Electricity Quantities

**Example 1 (more production):**
| Metering data type / direction | Quantity |
|-----------------------------------------|---------------------------|
| Production (IN)    | 15 kWh |
| Consumption (OUT)   | 10 kWh |
| Net – production (NET IN) | 5 kWh |
| Net – consumption (NET OUT) | 0 kWh |

**Example 2 (more consumption):**
| Metering data type / direction | Quantity |
|-----------------------------------------|---------------------------|
| Production (IN)    | 10 kWh |
| Consumption (OUT) | 15 kWh |
| Net – production (NET IN) | 0 kWh |
| Net – consumption (NET OUT) | 5 kWh |

#### Changes for web interface user

Metering data can still be submitted via Excel, but the Excel structure will change. The new Excel template will be available for download from the web interface starting from 20.07.2026.

> [!WARNING]
> The import and template API solutions will also be updated, but these APIs are intended for the web interface and are therefore not described in detail in this documentation.

> [!WARNING]
> Since this functionality is still under development, not all new APIs are yet documented in Swagger.

#### Changes for API user

> [!WARNING]
>  Starting from 20.07.2026 11:00 grid operators can't use `POST /api/v1/meter-data` message to add metering data. Other roles, for example line operator or aggregator can continue to send metering data via V1 API for 6 months after the go live of this functionality. 

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

**NB! until 20.07.2026 the `meter-data` service is used for submitting electricity metering data**

- The metering point operator sends a new or updated metering data message using the service `metering-data/electricity` for the transmission of electricity meter data (as of 20.07.2026 11:00) and `metering-data/natural-gas` for the transmission of gas meter data (as of November 2026).
- As metering data processing is performed asynchronously in the Data Hub, the Data Hub first provides a rapid response indicating whether the message was successfully received or not.
- Since the processing of metering data in the Datahub is asynchronous, the Datahub first gives a quick response whether the message was received or not.
- The Datahub then queues the message.
- The metering point operator verifies the result of processing, using `meter-data/status` service (at the `originalDocumentIdentification` position of the message, the value of the attribute of the same name that was in the `header` of the previously transmitted metering data message must be transmitted. The UUID value must not be reused). Possible results are:
  - `PROCESSING` - processing not finished
  - `SUCCESSFUL` - processing finished successfully
  - `ERROR` - processing finished with errors.
- If the message is processed without errors, then the data are added or changed in the database and the Datahub makes the addition or change of metering data available to open suppliers through the data-distribution service. For more details, see [Data distribution](30-data-distribution.md).
- If errors occur while processing the message, the Datahub will generate an error report and make it available to the metering point operator in the response of the  `meter-data/status` service.
- The metering point operator reads the error report addressed to it and resolves it according to its internal business logic.

> [!WARNING]
> **PLEASE NOTE! The Datahub transmits the metering data entered by the grid operators in unaltered form. The Datahub does not check the content of the metering data.**

> [!WARNING]
> When sending metering data via the V2 API, there is a limit on the number of periods that can be included in a single Excel file or API message. A maximum of 35,040 periods of metering data can be sent at once. This means that when sending data for one day at a time, a single Excel file or API message can contain data for up to 365 metering points. For longer periods, the number of metering points must be reduced accordingly.

> [!WARNING]
> `meter-data/status` API doesn't return records, that are created more than 7 days ago.

> [!NOTE]
> It is worth knowing that there is a very small, but in theory still possible situation where the Data Warehouse receives a metering data message and responds with a "processing started" response, but in reality the message remains unprocessed and no ´meter_data_status´ record is created about it either.
> The metering point manager should keep track of what has been received from each metering data message and whether the processing ended with a result. If some of the metering data messages do not receive any result, it must be assumed that an unexpected problem occurred in the Datahub when processing the metering data (e.g. unexpected shut down of the application) and the metering data must be transmitted again.
> There are different options for monitoring the results. E.g. check the status one by one based on `originalDocumentIdentification` (in case the data volumes are small) or scan the `SUCCESSFUL` and `ERROR` statuses and internally keep track of which messages have reached the final state

### Throttling of metering data input

Processing of received meteringdata is a 2-step process:
- the metering result is received (202) and placed in the processing queue;
- the metering data processor takes the metering results from the queue, writes the status, saves metering data to the database and updates the status.

If the measurement data processing is slower than new results are received, the processing queue starts to grow.

If the queue already has data of 100,000 requests, then the POST /meter-data endpoint responds with
- HTTP status 503
- HTTP header Retry-After: 300

The solution is based on the specifications:
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/503
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Retry-After

### Transmitting metering data via the web interface

In order to transmit data via the web interface user will need to navigate to "Metering data" page.

For easier metering data transmitting it is possible to download the template. To generate the template the resolution and time range needs to be selected, based on it the prefilled template is generated. It is important to choose the time range correctly - it needs to fit the resolution.

![Generating the template](../images/opp-ui/metering-data/metering-data-template1.png)

![Filling in the template](../images/opp-ui/metering-data/metering-data-template2.png)

To import metering data "Import" button needs to be clicked on the "Metering data" page. After that it is possible to add the metering data file. Guide how to fill the Excel file can be found here: [Transmitting metering data via Excel](#transmitting-metering-data-via-excel).

![Metering data import](../images/opp-ui/metering-data/metering-data-import.png)

In case there is a mistake in the file the system will notify the user:
1. Metering data can be added to several MS Excel file sheets. The system will tell the user on which sheet the problem is located.
2. In addition, it is possible to see the row where the problem is.
3. Error description helps to understand the issue.
4. After the problem is found and fixed "Cancel" should be clicked and import process should be repeated.

![Import error](../images/opp-ui/metering-data/metering-data-error.png)

### Transmitting metering data via Excel

Metering data can be sent using an Excel file. It can be uploaded via [the web interface](#transmitting-metering-data-via-web-interface) or by using the API `metering-data/import` service.

To send metering data, start by downloading the metering data template from the web interface. Instructions for this can be found here: [transmitting metering data via the web interface](#transmitting-metering-data-via-web-interface).

Below are the descriptions and examples of Excel columns:


# Examples of Net-Metered Electricity Quantities

| Column Name | Market | Description | Example | Mandatory? |
|------------|--------|-------------|---------|------------|
| Meter EIC | Electricity, Gas | EIC code of the metering point. The code must be included in all rows of the table. The market participant must be the owner of the metering point. Measurement data for multiple metering points may be submitted in a single file; they may be listed sequentially on one sheet or distributed across multiple Excel sheets. | 38ZEE-1000009--Z | Yes |
| Period Start | Electricity, Gas | Start of the period. The timestamp indicating the period to which the consumption/production quantities apply. It is recommended to use the date format provided in the template. Measurement data cannot be submitted with an incorrect date format. Correct format: dd.mm.yyyy hh:mm. | 01.11.2024 00:00:00 | Yes |
| IN Quantity kWh | Electricity, Gas | Quantity fed into the grid. | 1.534 | No, if “OUT Quantity kWh” is provided |
| OUT Quantity kWh | Electricity, Gas | Quantity taken from the grid. | 1.234 | No, if “IN Quantity kWh” is provided |
| IN Quantity m3 | Gas | Quantity fed into the grid, in cubic meters. | 1.534 | No, if “OUT Quantity m3” is provided |
| OUT Quantity m3 | Gas | Quantity taken from the grid, in cubic meters. | 1.234 | No, if “IN Quantity m3” is provided |
| NET IN Quantity kWh | Electricity | Net quantity fed into the grid. | 0.300 | Allowed for market roles GRID_OPERATOR and CLOSED_DISTRIBUTION_NETWORK. Must not be filled if “inQty” and “outQty” are missing. If one net quantity is filled, the other must also be filled. If filled then: a) Must be 0.000 if “netOutQty” is greater than 0.000 b) Must be 0.000 if both “inQty” and “outQty” are 0.000 c) Exactly 3 decimal places. |
| NET OUT Quantity kWh | Electricity | Net quantity taken from the grid. | 0.000 | Allowed for market roles GRID_OPERATOR and CLOSED_DISTRIBUTION_NETWORK. Must not be filled if “inQty” and “outQty” are missing. If one net quantity is filled, the other must also be filled. If filled then: a) Must be 0.000 if “netInQty” is greater than 0.000 b) Must be 0.000 if both “inQty” and “outQty” are 0.000 c) Exactly 3 decimal places. |
| Reading Type IN | Electricity, Gas | Measurement type of the quantity fed into the grid: measured or estimated. In the Excel template, the correct option can be selected from a dropdown menu by clicking the arrow next to the cell. | METERED or ESTIMATED | Yes, if “IN Quantity kWh” is filled |
| Reading Type OUT | Electricity, Gas | Measurement type of the quantity taken from the grid: measured or estimated. In the Excel template, the correct option can be selected from a dropdown menu by clicking the arrow next to the cell. | METERED or ESTIMATED | Yes, if “OUT Quantity kWh” is filled |

For successful transmission of metering data, it is essential that the Excel file is completed correctly and meets all requirements.

#### Possible errors when filling out Excel

| Issue                              | Solution                                                         |
|------------------------------------|-------------------------------------------------------------------|
| The metering data resolution is incorrect. | On the electricity market, it is only possible to submit data with a 15‑minute resolution. On the gas market, it is possible to submit data with a 1‑hour and 1‑day resolution. |
| The metering point does not belong to the market participant. | The market participant can only send metering data to metering points they own. |
| The file contains empty Excel sheets. | Although metering data can be divided across multiple sheets, ensure that the Excel file does not contain completely empty or otherwise unnecessary sheets. |
| The file contains formulas. | Data should be entered in plain text format - without formulas. |
| The time and resolution do not match. | For 1-hour resolution, period start times should correspond to full hours. For 15-minute resolution, period start times should correspond to quarter hours. |
| The time is in the wrong format. | The "Period start" time format must match that used in the template. The "Reading time" format must match the "Period start" time format. |
| All mandatory columns are not filled. | The table above indicates which fields are required. |
| Some rows are missing the metering point EIC code. | The metering point EIC code must be added to all rows in the table. |
| The Excel file is sent using an incorrect market role. | Metering data can only be sent by the grid operator, line operator, closed distribution network, and charging point operator. If a market participant operates in multiple roles, the appropriate role must be selected at the time of sending. |

### API messages

**Metering data search**

In the new API request, an additional attribute `Purpose` is introduced. The purpose of the request should be specified, for example whether the request is made for billing purposes or for querying own metering points. Initially, adding this value does not affect the response, but in the future it will also influence the response. The purpose of this change is to make API queries faster and support querying by multiple metering point EIC codes. Energy service provider should not add the purpose to the request.

Possible purposes in the open supplier role:
- `OPEN_SUPPLY` – the primary way for open suppliers to query metering data
- `PORTFOLIO` – querying metering data as a balance responsible party
- `BILLING` – querying data for billing purposes

Possible purposes in metering point manager role:
- `OWN_MP_MANAGEMENT` – querying data of own metering points
- `OTHER` – querying data of other metering points

Initially, metering data can only be searched one metering point at a time, but in the future it will also be possible to query data for multiple metering points simultaneously.

Explanation of abbreviations used in the API service:

| abbreviation | explanation | market | implementation info |
|--------------|-------------|--------|----------------------|
| periods | interval of one measurement result (15 minutes for electricity, 1 hour for gas) | Electricity, Gas |
| pS | Period Start | Electricity, Gas | |
| inQty | IN, i.e., incoming energy measurement result | Electricity, Gas | |
| outQty | OUT, i.e., outgoing energy measurement result | Electricity, Gas | |
| netInQty | net production (NET IN) | Electricity | from 01.08.2026 |
| netOutQty | net consumption (NET OUT) | Electricity | from 01.08.2026 |
| rTime | Reading Time, i.e., time of measurement | Electricity, Gas | |
| rType | Reading Type (E – estimated, M – read) | Electricity, Gas | |
| kwh | measured quantities in kWh | Electricity, Gas | |
| m3 | measured quantities in cubic meters | Electricity, Gas | |


The Datahub does not check whether every one hour or 15 minute interval is filled with metering data. 

> [!NOTE]
> The resolution of the data is rigidly fixed by the Datahub – electricity resolution is 15 minutes from 01.04.2025. The resolution for gas is one hour.> 
> In the case of gas, it is also allowed to transmit daily data. In this case, the daily metering data must be added to the suitable gas day hour.

#### Messages

| Message                                     | Purpose                                                              | Market |
|---------------------------------------------|----------------------------------------------------------------------|---------|
| `POST /api/V2/metering-data/electricity` | Adding metering data | Electricity |
| `POST /api/V2/metering-data/natural-gas` | Adding metering data | Gas |
| `GET /api/V2/metering-data/electricity`| Metering data search | Electricity |
| `GET /api/V2/metering-data/natural-gas`| Metering data search | Gas|
| `GET /api/V2/metering-data/electricity/template` | Generating and downloading a template for bulk upload of metering data | Electricity |
| `GET /api/V2/metering-data/natural-gas/template` | Generating and downloading a template for bulk upload of metering data | Gas |
| `POST /api/V1/meter-data/status`     | Querying the processing status of a metering data message            | Electricity, Gas |
| `POST /api/V2/metering-data/electricity/import` | Bulk upload of metering data using a template | Electricity |
| `POST /api/V2/metering-data/natural-gas/import` | Bulk upload of metering data using a template | Gas |
| `POST /api/V1/meter-data` | Adding metering data for grid operators and closed distribution grid operators, valid until 20 July 2026 | Electricity |
| `POST /api/V1/meter-data/search` | This version cannot be used to search net-metered electricity quantities from 01 August 2026 | Electricity |


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
- The time period of the metering data is allowed to be in the future. The current limit is 45 days. Each measurement is validated separately. If some values are further in the future, then allowed, then system replies with ERROR, the error code is `period-start-too-far-in-future`.
- The `import` service requires the same template, that the service `export` or `metering-data/electricity/template` / `metering-data/natural-gas/template` returns.

## Metering data requests

Relevant Datahub services have been set up to transmit metering data. Access to data is limited. The rules are described in [Role-based access rights](03.01-role-based-access-rights.md).

The following options are available for making metering data requests:

- Open suppliers, named suppliers and portfolio providers can scan metering data changes using the data-distribution service.
- Authorised users can request metering data using the `GET /metering-data/` service.

### legalConsent

Both physical and legal persons can grant access rights to data through the client portal. The rules are described in [Role-based access rights](03.01-role-based-access-rights.md).

Physical person data can only be queried when the client has given access rights through the client portal. For legal persons and organizations there is an alternative workflow where the legal person or organization gives access outside the system. In this case the right has to be given in written form and the open supplier needs to be able to prove it exists.

In this case Open Supplier can add `"legalConsent": true` to `GET /metering-data/` service. This allows metering data to be requested for any metering point, as long as the customer that has grid agreement is a legal person or organization.

> [!CAUTION] 
> It is only allowed to use `"legalConsent": true` when open supplier has customer's written authorization to request data. Legitimate usage of this service is monitored.

### Observation time type

Compared to the old system, the `billingSequence` concept has disappeared. Instead, the metering point manager transmits the reading time (**reading time**) together with the metering data.
When receiving metering data, the Datahub adds a data storing time (**snapshot time**) to the data.

Since both time values are available in the Datahub, the Datahub allows to search for metering data based on these time values. Examples:

1. The open supplier is interested in the last known metering data at metering point X. For this, he has 2 options:
  * Omits `observationTimeType` and `observationTime` attributes in the message
  * sets the attributes in the message:
    * `observationTimeType` = `SNAPSHOT_TIME`.
    * `observationTime` = current date and time
2. The open supplier is interested of metering data at metering point X as of 01.01.2024 00:00. To do this, it sets the attributes in the message:
  * `observationTimeType` = `SNAPSHOT_TIME`
  * `observationTime` = `2024-01-01T00:00:00+02:00`
3. The open supplier is interested of the metering data at the metering point X, where the reading time is not greater than 31.12.2023 23:59. To do this, it sets the attributes in the message:
  * `observationTimeType` = `READING_TIME`
  * `observationTime` = `2023-12-31T23:59:59+02:00`

> [!WARNING]
> At the moment, the `observationTimeType` = `SNAPSHOT_TIME` and `observationTime` combination (example nr 2) is not supported. Development task is created and planned to be finished during year 2024.

### Requesting metering data via the web interface

Metering data can be requested by navigating to "Metering data" page. There metering point EIC code and search period start need to be defined. If needed the end date can be added as well. 

![Searching metering data](../images/opp-ui/metering-data/metering-data-search.png)

In order to download metering data to Excel file first "Search" button has to be clicked. After that the "Download" button will be active.

### API messages

#### Messages

| Message                                   | Purpose                   | Market |
|-------------------------------------------|---------------------------|--------|
| `GET /api/{version}/metering-data/electricity` | Searching metering data       | Electricity |
| `GET /api/{version}/metering-data/natural-gas` | Searching metering data | Gas |
| `GET /api/{version}/metering-data/electricity/export` | Exporting metering data | Electricity |
| `GET /api/{version}/metering-data/natural-gas/export` | Exporting metering data | Gas |

