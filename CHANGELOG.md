## [EDH-2485] Release 0.6.1

- __2024-05-09__ - released to __TEST-PUBLIC__

|   Issue   | Type | Priority|                              Title                             |
|-----------|------|---------|----------------------------------------------------------------|
|  EDH-2486 |  Bug |  Medium |  OPP UI - The Modify agreement process does not work on the UI |

## [EDH-2480] Release 0.6.0

- __2024-05-09__ - released to __TEST-PUBLIC__

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

