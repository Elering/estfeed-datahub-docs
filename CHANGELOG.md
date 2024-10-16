## [EDH-3315] Release 0.18.2

- __2024-10-16__ - released to __TEST-PUBLIC__

|                                  Issue                                 | Type |  Priority |                                      Title                                      |
|------------------------------------------------------------------------|------|-----------|---------------------------------------------------------------------------------|
|  [EDH-3308](https://github.com/Elering/estfeed-datahub-docs/issues/90) |  Bug |  Critical |                 "POST /meter-data" has random lags in processing                |
|  [EDH-3321](https://github.com/Elering/estfeed-datahub-docs/issues/96) |  Bug |  Critical |  Data distribution search 500, Could not open JPA EntityManager for transaction |
|  [EDH-3319](https://github.com/Elering/estfeed-datahub-docs/issues/95) |  Bug |  Critical |                 Data distribution search is slow in GO-LIVE test                |

## [EDH-3299] Release 0.18.1

- __2024-10-14__ - released to __TEST-PUBLIC__

|   Issue   | Type | Priority|                  Title                 |
|-----------|------|---------|----------------------------------------|
|  EDH-3291 |  Bug |  Medium |  ERROR: Metering data processing fails |

## [EDH-3275] Release 0.18.0

- __2024-10-14__ - released to __TEST-PUBLIC__

|   Issue   | Type | Priority|                                         Title                                         |
|-----------|------|---------|---------------------------------------------------------------------------------------|
|  EDH-2636 |  Bug |  Medium |                  Estonian Customer can be created without PERSONAL_ID                 |
|  EDH-2623 |  Bug |  Minor  |  Latitude/Longitute coordinate fields not shown in the "Edit" modal of Metering Point |

## [EDH-3250] Release 0.17.1

- __2024-10-08__ - released to __TEST-PUBLIC__

|   Issue   | Type |  Priority |                                          Title                                          |
|-----------|------|-----------|-----------------------------------------------------------------------------------------|
|  EDH-3216 |  Bug |  Critical |  createBulkMeterData fails immediately when TimescaleDB deadlocked during MDM data send |

## [EDH-3239] Release 0.17.0

- __2024-10-08__ - released to __TEST-PUBLIC__

|                                  Issue                                 |  Type  |  Priority |                                                      Title                                                      |
|------------------------------------------------------------------------|--------|-----------|-----------------------------------------------------------------------------------------------------------------|
|                                EDH-2971                                |   Bug  |   Medium  |                                Some metering points not found based on Client EIC                               |
|  [EDH-3208](https://github.com/Elering/estfeed-datahub-docs/issues/80) |   Bug  |  Critical |                           [TEMP] DD message creation fails silently for unknown reason                          |
|  [EDH-3171](https://github.com/Elering/estfeed-datahub-docs/issues/79) |   Bug  |  Critical |                            For some grid agreements ValidTo can't be removed/changed                            |
|  [EDH-3147](https://github.com/Elering/estfeed-datahub-docs/issues/75) |  Story |  Highest  |                     Border point customer has no access border metering point metering data                     |
|                                EDH-3087                                |  Story |  Critical |           [BREAKING CHANGE] hasContent (boolean) has been added to Data distribution search response            |
|                                EDH-2883                                |  Story |   Medium  |  [OPP-BE][TEMP] Adjust customer update rules to eliminate error message when a customer is created successfully |
|                                EDH-3195                                |  Story |  Highest  |                           [DD] Distribute deleted GS agreement first and create after                           |

## [EDH-3196] Release 0.16.0

- __2024-10-08__ - released to __TEST-PUBLIC__

|                                  Issue                                 |  Type  |  Priority |                                                     Title                                                     |
|------------------------------------------------------------------------|--------|-----------|---------------------------------------------------------------------------------------------------------------|
|                                EDH-3020                                |   Bug  |   Medium  |                        Missing DD messages (GRID change deletes SUPPLY and changes GS)                        |
|                                EDH-3038                                |   Bug  |   Medium  |      When downloading metering data for longer period of time only 3,5 months worth of data is downloaded     |
|                                EDH-2975                                |   Bug  |  Critical |                    Cannot upload metering data on autumn clock change (03 hour duplicated)                    |
|                                EDH-2898                                |   Bug  |   Minor   |                         Meter data template quantity values should be in 0,000 format                         |
|  [EDH-3157](https://github.com/Elering/estfeed-datahub-docs/issues/78) |   Bug  |  Critical |                           Grid agreement can't be added in roles PO, LO, CO and CDN                           |
|                                EDH-3016                                |   Bug  |   Medium  |                             Not possible to add grid agreement with 1 day duration                            |
|                                EDH-2664                                |   Bug  |   Medium  |                                 Delete data duplication in swagger definitions                                |
|                                EDH-3064                                |   Bug  |  Critical |              "meter/search/customer" returns different amount of MP-s if legalConsent=true/false              |
|                                EDH-2928                                |   Bug  |   Medium  |  /agreement/search/meter serviceProviderName history displays only the latest version of the name in response |
|                                EDH-2815                                |  Story |  Highest  |                               [OPP-BE] Improve performance of Meter Data Export                               |

## [EDH-3127] Release 0.15.0

- __2024-09-19__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                                        Title                                                        |
|-----------|--------|-----------|---------------------------------------------------------------------------------------------------------------------|
|  EDH-3100 |   Bug  |  Critical |                               Reports fail due to not being able to handle meter data                               |
|  EDH-3000 |   Bug  |   Medium  |                  Generate metering point EIC codes "Copy" button gives empty success message on UI                  |
|  EDH-2914 |   Bug  |   Medium  |  [UI] Connection state change reply as Open Supplier gets error about preferredDate that is not displayed in the UI |
|  EDH-2890 |   Bug  |  Critical |                 Automatic empty MP search when starting a new agreement (GO), can cause opp-api OOM                 |
|  EDH-3102 |   Bug  |   Medium  |                  (GRID) agreement can be extended to overlap other existing GRID agreement in a MP                  |
|  EDH-3084 |   Bug  |  Highest  |                                    EIC generator generates out of range EIC codes                                   |
|  EDH-3156 |  Story |  Critical |                    [BREAKING CHANGE] DD limit findDataDistributions response max pageSize to 100                    |
|  EDH-3024 |  Story |  Highest  |                           Update DD rules for SUPPLY agreement in case of automatic delete                          |
|  EDH-3017 |  Story |  Highest  |                                   DD messages about (BORDER_)GRID agreement delete                                  |
|  EDH-3081 |  Story |  Critical |                          Metering data read pagination needs to cover 1 year metering data                          |

## [EDH-3099] Release 0.14.0

- __2024-09-17__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                         Title                                        |
|-----------|--------|-----------|--------------------------------------------------------------------------------------|
|  EDH-3028 |   Bug  |   Medium  |          Role OPEN_SUPPLIER missing role type VIEW_BALANCE_SETTLEMENT_POINT          |
|  EDH-2890 |   Bug  |  Critical |  Automatic empty MP search when starting a new agreement (GO), can cause opp-api OOM |
|  EDH-3075 |   Bug  |  Critical |                    GENERAL_SERVICE agreement has no valid_to date                    |
|  EDH-2970 |   Bug  |   Medium  |      Impossible to add/change agreements when PARENT MP has more than 1 CHILD MP     |
|  EDH-2900 |  Story |  Highest  |                       [RPT-BE] Improve performance of Reporting                      |

## [EDH-3012] Release 0.13.0

- __2024-09-03__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                              Title                                              |
|-----------|--------|-----------|-------------------------------------------------------------------------------------------------|
|  EDH-2917 |   Bug  |  Critical |              TraceId missing from reporting endpoints after the move to rpt service             |
|  EDH-2951 |   Bug  |  Critical |                         Wrong METERING_DATA DD messages to OPEN_SUPPLIER                        |
|  EDH-2970 |   Bug  |   Medium  |           Impossible to add/change agreements when PARENT MP has more than 1 CHILD MP           |
|  EDH-2955 |  Story |   Medium  |  [OPP] Remove version from joint invoice search response and latestVersionOnly from the request |
|  EDH-2750 |  Story |  Highest  |      [TEMP] Improve Meter EIC generation algorithm - 15th char doesn't have to be "-" sign      |

## [EDH-2920] Release 0.12.0

- __2024-08-23__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                         Title                                        |
|-----------|--------|-----------|--------------------------------------------------------------------------------------|
|  EDH-2890 |   Bug  |  Critical |  Automatic empty MP search when starting a new agreement (GO), can cause opp-api OOM |
|  EDH-2917 |   Bug  |  Critical |        TraceId missing from reporting endpoints after the move to rpt service        |
|  EDH-2538 |   Bug  |  Critical |                      Wrong DD message for OS about GS agreement                      |
|  EDH-2897 |   Bug  |   Medium  |                    Excel imports give empty success message on UI                    |
|  EDH-2873 |   Bug  |  Critical |             Connection request "read" doesn't update automatically on UI             |
|  EDH-2775 |   Bug  |   Medium  |           Joint invoice processing error msg is not mapped to API response           |
|  EDH-2670 |   Bug  |  Critical |              Existing agreements are not displayed in New agreement form             |
|  EDH-2292 |   Bug  |   Medium  |                 Adding organization with ID Type results in an error                 |
|  EDH-2770 |   Bug  |   Medium  |                    Unclear error message for new supply agreement                    |
|  EDH-2850 |   Bug  |  Critical |    Metering data upload (Excel) produces incorrect metering type and reading time    |
|  EDH-720  |  Story |   Medium  |                       Implement scheduling of report generation                      |
|  EDH-2789 |  Story |  Highest  |     [DD] Improve deleted agreement distribution receiver based on portfolio tree     |
|  EDH-2788 |  Story |  Highest  |          [DD] Restrict agreement distribution based on endUserAgreementType          |
|  EDH-2522 |  Story |   Medium  |                              Portfolio agreement UI view                             |

## [EDH-2829] Release 0.11.0

- __2024-08-14__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                                                            Title                                                                           |
|-----------|--------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  EDH-2818 |   Bug  |  Critical |                          [DD] Agreement distribution shows up as an object in the search response, but swagger says it is an array                         |
|  EDH-2717 |   Bug  |  Critical |  DD is not sent to Open Supplier when GRID agreement date has changed, Internal ID of Service Provider cannot be resolved, queue: dd_distribute_data_req_q |
|  EDH-2806 |   Bug  |   Medium  |                                              In Estonian UI, date next to person's name is not shown correctly                                             |
|  EDH-2381 |   Bug  |  Highest  |              "mpm.error.business.not-exists.metering-point" error in case adding agreement, where validFrom is in past and MP is created today             |
|  EDH-2535 |  Story |  Highest  |                                                            Estonian translation for UI / notMVP                                                            |
|  EDH-1684 |  Story |   Medium  |                                           [OPP-UI][OPP-BE] Extend Search metering point flow with implicit access                                          |
|  EDH-2713 |  Story |   Medium  |                                              [OPP-BE] Limit number of Metering Points to be exported to 50 000                                             |

## [EDH-2766] Release 0.10.0

- __2024-07-30__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                              Title                                              |
|-----------|--------|-----------|-------------------------------------------------------------------------------------------------|
|  EDH-2740 |   Bug  |  Highest  |                          [DD] GS agreement is not distributed properly                          |
|  EDH-2507 |   Bug  |  Critical |                         Admin role can delete estfeed admin role via UI                         |
|  EDH-2873 |   Bug  |  Critical |                   Connection request "read" doesn't update automatically on UI                  |
|  EDH-2715 |   Bug  |  Critical |                        Cannot remove ValidTo from a border grid agreement                       |
|  EDH-2626 |  Story |  Highest  |                           [RPT] Move Reporting features to new service                          |
|  EDH-2322 |  Story |   Medium  |             [OPP-BE][MPD] Define observationTime value when gathering Metering Data             |
|  EDH-2533 |  Story |   Medium  |  [OPP][TEMP] Implement solution for updating existing identities with new business object types |

## [EDH-2721] Release 0.9.0

- __2024-07-17__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                                                            Title                                                                           |
|-----------|--------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  EDH-2670 |   Bug  |  Critical |                                                 Existing agreements are not displayed in New agreement form                                                |
|  EDH-2717 |   Bug  |  Critical |  DD is not sent to Open Supplier when GRID agreement date has changed, Internal ID of Service Provider cannot be resolved, queue: dd_distribute_data_req_q |
|  EDH-2538 |   Bug  |  Critical |                                                         Wrong DD message for OS about GS agreement                                                         |
|  EDH-892  |  Story |   Medium  |                                           [OPP-UI][OPP-BE][MPD] Metering data search to support data aggregation                                           |
|  EDH-2541 |  Story |   Medium  |                                                        datahub.elering.ee Cookiebot implementation                                                         |

## [EDH-2669] Release 0.8.1

- __2024-07-05__ - released to __TEST-PUBLIC__

|   Issue   | Type |  Priority |                     Title                    |
|-----------|------|-----------|----------------------------------------------|
|  EDH-2678 |  Bug |  Highest  |  [DD] authentication of technical user fails |
|  EDH-2643 |  Bug |  Critical |       Agreements - search doesn't fail       |

## [EDH-2657] Release 0.8.0

- __2024-07-05__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                                    Title                                                   |
|-----------|--------|-----------|------------------------------------------------------------------------------------------------------------|
|  EDH-2507 |   Bug  |  Critical |                               Admin role can delete estfeed admin role via UI                              |
|  EDH-1866 |   Bug  |   Medium  |                      Create Joint Invoice API: added traceID to unsuccessful request                       |
|  EDH-2601 |   Bug  |  Critical |                           SUPPLY agreement can start earlier, than GRID agreement                          |
|  EDH-2493 |  Story |   Medium  |                           DD - change who can access info about Service Provider                           |
|  EDH-2490 |  Story |   Medium  |                                 [DD] Agreement change reason to be accurate                                |
|  EDH-2582 |  Story |  Critical |                             "transmissionNetworkEic" update should be possible                             |
|  EDH-2521 |  Story |  Highest  |                                    Joint Invoice - removed PUT endpoint                                    |
|  EDH-2371 |  Story |   Medium  |  [OPP-BE] Improve import metering data from excel for Market Participants with large Metering Point number |
|  EDH-2368 |  Story |   Medium  |               [OPP-BE] Add legalConsent functionality to metering data query for LEGAL_PERSON              |
|  EDH-2253 |  Story |   Medium  |              [OPP-BE][MPM] Avoid considering GENERAL_SERVICE agreements being valid in future              |
|  EDH-1682 |  Story |   Medium  |                           Extend Search agreements flow with connected agreements                          |

## [EDH-2591] Release 0.7.1

- __2024-06-20__ - released to __TEST-PUBLIC__

|   Issue   | Type |  Priority |                                                          Title                                                          |
|-----------|------|-----------|-------------------------------------------------------------------------------------------------------------------------|
|  EDH-2590 |  Bug |   Medium  |  In Search customer data flow (/api/v1/customer/search), the response does not contain the validFrom and validTo values |
|  EDH-2555 |  Bug |  Critical |                            [OPP] Error during GRID_OPERATORS_OPEN_SUPPLIER report generation                            |

## [EDH-2548] Release 0.7.0

- __2024-06-20__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                       Title                                       |
|-----------|--------|-----------|-----------------------------------------------------------------------------------|
|  EDH-2500 |   Bug  |   Medium  |              [TEMP] NullPointerException: General Service generation              |
|  EDH-2474 |   Bug  |   Medium  |               Named supplier can now submit connection state request              |
|  EDH-2432 |   Bug  |   Medium  |                  Cannot modify JOINT_INVOICE agreement in the UI                  |
|  EDH-2427 |   Bug  |   Medium  |  Cannot update GRID agreement's validTo to less than SUPPLY agreement's validFrom |
|  EDH-1864 |   Bug  |   Medium  |    Fixed bug when searching joint invoices by dataPeriodStart and dataPeriodEnd   |
|  EDH-2550 |   Bug  |  Critical |                 Open Supplier and Grid Operator report is failing                 |
|  EDH-2526 |   Bug  |   Lowest  |                 Aggregator meter data icon tooltip text is missing                |
|  EDH-2498 |   Bug  |   Medium  |     OS role should not see "template" button under "metering data" menu point     |
|  EDH-2478 |   Bug  |  Critical |                        Metering data not updated via import                       |
|  EDH-712  |  Story |   Medium  |                  [OPP-BE][MPD] Generate Balance Provider 2 report                 |
|  EDH-2257 |  Story |   Medium  |      [OPP-BE][MPM] POST /meter/search/customer should not use past agreements     |
|  EDH-2243 |  Story |   Medium  |                [TEMP] Multiple EIC ranges for one company supported               |
|  EDH-2637 |  Story |   Medium  |                Reports are still in ALPHA state / not tested enough               |
|  EDH-1815 |  Story |   Medium  |               Metering data is data distributed after import from UI              |
|  EDH-967  |  Story |   Medium  |                         [OPP] Balance Settlement Point API                        |
|  EDH-897  |  Story |   Medium  |                       [OPP-UI] Balance settlement points UI                       |
|  EDH-2370 |  Story |  Highest  |        When adding new Supply agreement, you can search for metering data         |
|  EDH-2146 |  Story |   Medium  |                 [OPP-UI] Create multiple agreements simultaneously                |

## [EDH-2510] Release 0.6.2

- __2024-06-20__ - released to __TEST-PUBLIC__

|   Issue   |  Type  | Priority|                                   Title                                   |
|-----------|--------|---------|---------------------------------------------------------------------------|
|  EDH-2257 |  Story |  Medium |  [OPP-BE][MPM] POST /meter/search/customer should not use past agreements |

## [EDH-2485] Release 0.6.1

- __2024-05-30__ - released to __TEST-PUBLIC__

|   Issue   | Type | Priority|                              Title                             |
|-----------|------|---------|----------------------------------------------------------------|
|  EDH-2486 |  Bug |  Medium |  OPP UI - The Modify agreement process does not work on the UI |

## [EDH-2480] Release 0.6.0

- __2024-05-30__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                                   Title                                                  |
|-----------|--------|-----------|----------------------------------------------------------------------------------------------------------|
|  EDH-2434 |   Bug  |   Medium  |                                Cannot modify PORTFOLIO agreement in the UI                               |
|  EDH-2432 |   Bug  |   Medium  |                              Cannot modify JOINT_INVOICE agreement in the UI                             |
|  EDH-2361 |   Bug  |   Medium  |                       Modifying functionality missing for named supplier agreement                       |
|  EDH-2402 |   Bug  |   Medium  |                       "validFrom is not a valid property" while adding new Customer                      |
|  EDH-2401 |   Bug  |   Medium  |     Metering points UI doesn't display Customer EIC even if there's an active customer with agreement    |
|  EDH-2309 |   Bug  |   Medium  |                                 Metering points not found by Customer EIC                                |
|  EDH-2035 |   Bug  |   Medium  |                           Error description metering data status is low quality                          |
|  EDH-2444 |   Bug  |  Critical |              Overlapping OS agreements can be created by extending the previous OS agreement             |
|  EDH-2366 |   Bug  |   Medium  |                                    Generate EIC returns used  EIC-code                                   |
|  EDH-2293 |   Bug  |   Lowest  |                       After successfully adding a new agreement EIC fields turn red                      |
|  EDH-2447 |   Bug  |   Medium  |                            GO gets DD message if he updated the MP - Now fixed                           |
|  EDH-2445 |   Bug  |   Medium  |                     NAMED_SUPPLY and PORTFOLIO_SUPPLY agreements are not distributed                     |
|  EDH-2440 |   Bug  |   Medium  |                              Missing DD-s after adding OPEN_SUPPLY agreement                             |
|  EDH-2204 |   Bug  |   Medium  |                                      DD not created for GS agreement                                     |
|  EDH-344  |  Story |   Medium  |                                 [OPP-BE] Metering points import via file                                 |
|  EDH-2115 |  Story |   Medium  |  POST /agreement/search/meter - access restriction, response and aggregator metering point logic updates |
|  EDH-711  |  Story |   Medium  |                              [OPP-BE][MPD] Generate Balance Provider report                              |
|  EDH-2248 |  Story |   Medium  |                               Generate free EIC values when multiple ranges                              |
|  EDH-2123 |  Story |   Medium  |                            Active named supplier can update customer metadata                            |
|  EDH-2020 |  Story |   Lowest  |                             Create customer - validate business registry code                            |
|  EDH-2291 |  Story |   Medium  |                Join IN and OUT measurements together in the /network-bill/search response                |
|  EDH-2286 |  Story |   Medium  |                                      Networkbill day/night optional                                      |

## [EDH-2426] Release 0.5.3

- __2024-05-16__ - released to __TEST-PUBLIC__

|   Issue   | Type | Priority|                          Title                          |
|-----------|------|---------|---------------------------------------------------------|
|  EDH-2408 |  Bug |  Medium |  [DD] Agreement distribution fails for SUPPLY agreement |

## [EDH-2397] Release 0.5.2

- __2024-05-09__ - released to __TEST-PUBLIC__

|   Issue   | Type |  Priority |                                       Title                                       |
|-----------|------|-----------|-----------------------------------------------------------------------------------|
|  EDH-2396 |  Bug |  Critical |  Unexpected unauthorized error message for some users of some market participants |

## [EDH-2386] Release 0.5.1

- __2024-05-09__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |               Title              |
|-----------|--------|-----------|----------------------------------|
|  EDH-2356 |  Story |  Critical |  Truncate very long log messages |

## [EDH-2377] Release 0.5.0

- __2024-05-09__ - released to __TEST-PUBLIC__

|   Issue   |  Type  | Priority|                                                              Title                                                             |
|-----------|--------|---------|--------------------------------------------------------------------------------------------------------------------------------|
|  EDH-2367 |   Bug  |  Medium |                                        [MPM] Improve agreement sync flow with new status                                       |
|  EDH-2209 |   Bug  |  Medium |                                     [DD] SUPPLY agreement is distributed to named supplier                                     |
|  EDH-1926 |   Bug  |  Minor  |                                [MPD] NetworkBill for ELECTRICITY allows "measurementUnit": "M3"                                |
|  EDH-2279 |   Bug  |  Minor  |                               POST /meter/search/customer response contains versions information                               |
|  EDH-2292 |   Bug  |  Medium |                                      Adding organization with ID Type results in an error                                      |
|  EDH-2271 |   Bug  |  Medium |  /meter/search/customer returns "opp.error.technical.general" if "legalConsent": true while searching by physical person's EIC |
|  EDH-2278 |   Bug  |  Medium |                                      "Modify" button visible for General Service agreement                                     |
|  EDH-2262 |  Story |  Medium |                                              [CDM] Add new billing method B2B_BILL                                             |
|  EDH-2109 |  Story |  Medium |                              Identifier + country combination must be unique while adding identity                             |
|  EDH-2406 |  Story |  Medium |                                            Reports now available, but not tested yet                                           |
|  EDH-2093 |  Story |  Medium |                                 [OPP-BE] Return customer's billing data only to named supplier                                 |
|  EDH-1985 |  Story |  Medium |                                 [OPP-BE] Metering data import with file produces import report                                 |
|  EDH-1610 |  Story |  Medium |       Display related agreements for found MP-s, while adding/modifying (border)grid, open supply or aggreation agreement      |
|  EDH-720  |  Story |  Medium |                                            Implement scheduling of report generation                                           |
|  EDH-344  |  Story |  Medium |                                            [OPP-BE] Metering points import via file                                            |

## [EDH-2369] Release 0.4.2

- __2024-05-09__ - released to __TEST-PUBLIC__

|   Issue   | Type |  Priority |             Title             |
|-----------|------|-----------|-------------------------------|
|  EDH-2345 |  Bug |  Critical |  Some data distribution fixes |

## [EDH-2349] Release 0.4.1

- __2024-04-25__ - released to __TEST-PUBLIC__

|   Issue   | Type |  Priority |                                       Title                                       |
|-----------|------|-----------|-----------------------------------------------------------------------------------|
|  EDH-2337 |  Bug |  Critical |  Using ee.. username JWT authentication token fails to authN in Data Distribution |

## [EDH-2284] Release 0.4.0

- __2024-04-23__ - released to __TEST-PUBLIC__

|   Issue   |  Type  | Priority |                                                               Title                                                               |
|-----------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------|
|  EDH-2016 |   Bug  |  Medium  |                                     New SUPPLY agreement doesn't end previous SUPPLY agreement                                    |
|  EDH-2328 |  Story |  Highest |  IMPORTANT: Data distribution got it's own separate Swagger UI: https://public-test-dd-datahub.elering.ee/swagger-ui/index.html#/ |
|  EDH-2142 |  Story |  Medium  |                                          [DD] DD records are not in chronological order.                                          |
|  EDH-1965 |  Story |  Medium  |                                  [OPP-UI][OPP-BE][AUTHZ] Display assignable roles for admin users                                 |
|  EDH-713  |  Story |  Medium  |                                            [OPP-BE][MPD] Generate Grid Operator report                                            |
|  EDH-2124 |  Story |  Medium  |                                             Add new BILLING_METHOD value: SELF_SERVICE                                            |
|  EDH-2321 |  Story |  Highest |                              IMPORTANT: Username format has changed from pnoee-394xx.. to ee394xxz..                              |
|  EDH-1880 |  Story |  Medium  |                         [OPP-BE] Improve Metering Data Excel export & import by supporting multiple sheets                        |
|  EDH-507  |  Story |  Medium  |                        [OPP-UI][OPP-BE] Add Customer IDs to search filters in agreement search and download                       |
|  EDH-2108 |  Story |  Medium  |                                       [OPP-UI] Search for EMBASSY while adding new agreement                                      |

## [EDH-2158] Release 0.3.0

- __2024-04-23__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                         Title                                         |
|-----------|--------|-----------|---------------------------------------------------------------------------------------|
|  EDH-2125 |   Bug  |   Medium  |                Metering data UI doesn't display quantity if qty = 0.00                |
|  EDH-2101 |   Bug  |   Minor   |        [OPP-UI] Connection state - allows to request disconnection on past date       |
|  EDH-1964 |   Bug  |   Minor   |         List of tech. users - the heading is sometimes not rendered correctly         |
|  EDH-2104 |   Bug  |  Critical |               [TEMP-API] findAllMeteringPointsWithAgreements OutOfMemory              |
|  EDH-960  |  Story |   Medium  |                 Add new supply, (border)grid or aggregation agreement                 |
|  EDH-1985 |  Story |   Medium  |             [OPP-BE] Metering data import with file produces import report            |
|  EDH-507  |  Story |   Medium  |  [OPP-UI][OPP-BE] Add Customer IDs to search filters in agreement search and download |
|  EDH-713  |  Story |   Medium  |                      [OPP-BE][MPD] Generate Grid Operator report                      |
|  EDH-1912 |  Story |  Highest  |                         [DD] Create Data distribution service                         |

## [EDH-2156] Release 0.2.0

|   Issue   |  Type  | Priority|                                               Title                                              |
|-----------|--------|---------|--------------------------------------------------------------------------------------------------|
|  EDH-1169 |   Bug  |  Medium |          System generates BORDER_SUPPLY agreement with no actual validity period length          |
|  EDH-2021 |   Bug  |  Medium |                             Sending metering data to non-existent MP                             |
|  EDH-2073 |   Bug  |  Medium |                             [OPP-UI] Connection state creation fails                             |
|  EDH-1968 |  Story |  Medium |  [OPP-UI][OPP-BE][TEMP] Introduce location filter in Metering Point /search and /export endpoint |
|  EDH-1960 |  Story |  Medium |             [OPP-BE] Remove customer and service provider from agreement distribution            |
|  EDH-1882 |  Story |  Medium |               [OPP-BE] Introduce portfolio tree for data distribution - agreements               |
|  EDH-1302 |  Story |  Medium |                           [OPP-BE] Search Customer agreements REST API                           |
|  EDH-640  |  Story |  Medium |                   [OPP-BE] Distribute agreement create, update, delete payloads                  |
|  EDH-464  |  Story |  Medium |                                 [OPP-BE] EIC API /eic/range flow                                 |
|  EDH-2002 |  Story |  Medium |                               [OPP-UI] Show error messages on Modal                              |

## [EDH-2129] Release 0.1.1 - test public only

- __2024-03-26__ - released to __TEST-PUBLIC__

|   Issue   | Type |  Priority |                                   Title                                   |
|-----------|------|-----------|---------------------------------------------------------------------------|
|  EDH-2034 |  Bug |  Critical |  /api/v1/meter returning that ProductionSource is mandatory even if false |

