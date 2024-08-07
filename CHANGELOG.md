## [EDH-2766] Release 0.10.0

- __2024-07-30__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                              Title                                              |
|-----------|--------|-----------|-------------------------------------------------------------------------------------------------|
|  EDH-2740 |   Bug  |  Highest  |                          [DD] GS agreement is not distributed properly                          |
|  EDH-2507 |   Bug  |  Critical |                         Admin role can delete estfeed admin role via UI                         |
|  EDH-2715 |   Bug  |  Critical |                        Cannot remove ValidTo from a border grid agreement                       |
|  EDH-2626 |  Story |  Highest  |                           [RPT] Move Reporting features to new service                          |
|  EDH-2322 |  Story |   Medium  |             [OPP-BE][MPD] Define observationTime value when gathering Metering Data             |
|  EDH-2533 |  Story |   Medium  |  [OPP][TEMP] Implement solution for updating existing identities with new business object types |

## [EDH-2721] Release 0.9.0

- __2024-07-17__ - released to __TEST-PUBLIC__

|   Issue   |  Type  |  Priority |                                  Title                                  |
|-----------|--------|-----------|-------------------------------------------------------------------------|
|  EDH-2670 |   Bug  |  Critical |       Existing agreements are not displayed in New agreement form       |
|  EDH-892  |  Story |   Medium  |  [OPP-UI][OPP-BE][MPD] Metering data search to support data aggregation |
|  EDH-2541 |  Story |   Medium  |               datahub.elering.ee Cookiebot implementation               |

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
|  EDH-2367 |   Bug  |  Medium |                                             [DD] swagger sample does not contain id                                            |
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

