## 2025-03-06

|   Issue   |  Type  |  Priority |                                                Title                                               |
|-----------|--------|-----------|----------------------------------------------------------------------------------------------------|
|  EDH-3877 |  Story |  Highest  |                               [RPT] parameterize metering data queue                               |
|  EDH-3916 |   Bug  |  Critical |  Removing border grid's validTo does not create proper border supplies in case of portfolio change |
|  EDH-3647 |  Story |  Highest  |                                   API meter-data POST throttling                                   |

## 2025-03-04

|   Issue   | Type | Priority|                   Title                  |
|-----------|------|---------|------------------------------------------|
|  EDH-3890 |  Bug |  Medium |  TEMP reorganizeMarketModel fails in DEV |

## 2025-02-28

|   Issue   |  Type  | Priority |                             Title                            |
|-----------|--------|----------|--------------------------------------------------------------|
|  EDH-2518 |  Story |  Medium  |  Add metering point to agreement without the search function |
|  EDH-4072 |  Story |  Highest |           AUTHZ springAmqp version update to 3.2.2           |

## 2025-02-27

|   Issue   |   Type   | Priority |                                                        Title                                                       |
|-----------|----------|----------|--------------------------------------------------------------------------------------------------------------------|
|  EDH-3892 |    Bug   |  Highest |                      "/meter/search/customer" returns MP-s, where the GRID agreement has ended                     |
|  EDH-3904 |    Bug   |  Medium  |  The process of sending meter data doesn't finish, when uploading meter data with excel and mpd connection is down |
|  EDH-4188 |  Release |  Medium  |                                                   Release 1.0.39                                                   |

## 2025-02-26

|   Issue   |  Type | Priority|                                    Title                                   |
|-----------|-------|---------|----------------------------------------------------------------------------|
|  EDH-3594 |  Bug  |  Medium |               No DELETE/UPDATE GRID to OS (future agreements)              |
|  EDH-4143 |  Task |  Medium |  Add last_modified_time column to rpt_snapshot_header and start filling it |

## 2025-02-21

|                                  Issue                                  |  Type  | Priority |                 Title                 |
|-------------------------------------------------------------------------|--------|----------|---------------------------------------|
|  [EDH-4037](https://github.com/Elering/estfeed-datahub-docs/issues/166) |  Story |  Highest |  networkBill for Border Meteringpoint |

## 2025-02-19

|   Issue   |  Type  | Priority |                                 Title                                 |
|-----------|--------|----------|-----------------------------------------------------------------------|
|  EDH-3089 |  Story |  Medium  |             General service not distinguishable in reports            |
|  EDH-3615 |  Story |  Highest |  [RPT] Introduce intermediate layer to save time on report generation |

## 2025-02-18

|   Issue   | Type | Priority |                                 Title                                 |
|-----------|------|----------|-----------------------------------------------------------------------|
|  EDH-3879 |  Bug |  Highest |  [TEMP] Users with permissions can not log in to EFKP - general error |

## 2025-02-17

|   Issue   |  Type |  Priority |                                               Title                                              |
|-----------|-------|-----------|--------------------------------------------------------------------------------------------------|
|  EDH-3097 |  Task |   Medium  |                        Missing role privileges for notMVP functionalities                        |
|  EDH-3972 |  Bug  |  Critical |          [LIVE] missingCache: GRID agreement version change will take cache out of sync          |
|  EDH-3435 |  Bug  |   Medium  |  Cannot query DD records during the summer/winter time changeover when the day is 25 hours long. |

## 2025-02-12

|                                  Issue                                  |  Type  |  Priority |                             Title                             |
|-------------------------------------------------------------------------|--------|-----------|---------------------------------------------------------------|
|  [EDH-3947](https://github.com/Elering/estfeed-datahub-docs/issues/151) |  Story |  Critical |  Joint invoice GRID/SUPPLY/GENERAL_SERVICE validation removal |

## 2025-02-11

|   Issue   | Type |  Priority |                            Title                            |
|-----------|------|-----------|-------------------------------------------------------------|
|  EDH-3786 |  Bug |  Critical |  Increased memory consumption with 3.2.0 springAmqpVersion  |

## 2025-02-10

|                                  Issue                                  | Type |  Priority |                             Title                             |
|-------------------------------------------------------------------------|------|-----------|---------------------------------------------------------------|
|  [EDH-4030](https://github.com/Elering/estfeed-datahub-docs/issues/167) |  Bug |  Critical |  [OPP] joint/invoice download produces deadlock on MSSQL side |

## 2025-01-31

|                                  Issue                                  | Type | Priority |                                                  Title                                                  |
|-------------------------------------------------------------------------|------|----------|---------------------------------------------------------------------------------------------------------|
|  [EDH-3666](https://github.com/Elering/estfeed-datahub-docs/issues/145) |  Bug |  Highest |  RPT: technical user cant receive reports when making request POST {{rptRestHost}}/api/v1/report/search |
|  [EDH-3844](https://github.com/Elering/estfeed-datahub-docs/issues/161) |  Bug |  Highest |                                          rTime missing from DD                                          |
|                                 EDH-3501                                |  Bug |  Highest |                             Customer and SP EICs missing from the DD message                            |
|                                 EDH-3453                                |  Bug |  Medium  |             Metering data Excels have doubled rows with wrong period time and no quantities             |

## 2025-01-29

|   Issue   |  Type  | Priority|                          Title                         |
|-----------|--------|---------|--------------------------------------------------------|
|  EDH-3853 |  Story |  Medium |  [PARM] automatic APPROVE of AGGREGATOR, OPEN_SUPPLIER |

## 2025-01-27

|                                  Issue                                  |  Type  |  Priority |                     Title                    |
|-------------------------------------------------------------------------|--------|-----------|----------------------------------------------|
|  [EDH-3839](https://github.com/Elering/estfeed-datahub-docs/issues/162) |  Story |  Critical |  DD sequence in case of OPEN_SUPPLIER change |

## 2025-01-23

|                                  Issue                                  | Type | Priority |                                     Title                                    |
|-------------------------------------------------------------------------|------|----------|------------------------------------------------------------------------------|
|  [EDH-3641](https://github.com/Elering/estfeed-datahub-docs/issues/143) |  Bug |  Highest |                   Duplicated metering points in the tables                   |
|                                 EDH-3688                                |  Bug |  Highest |  temp-api created duplicate COMPANY_ID when logging in through client portal |

## 2025-01-22

|                                  Issue                                  | Type |  Priority |                                      Title                                     |
|-------------------------------------------------------------------------|------|-----------|--------------------------------------------------------------------------------|
|                                 EDH-2653                                |  Bug |   Medium  |            System doesn't show the latest metadata on various pages            |
|                                 EDH-2972                                |  Bug |   Medium  |       Aggregator can see AGG agreements, that are not related to this MP       |
|  [EDH-3711](https://github.com/Elering/estfeed-datahub-docs/issues/149) |  Bug |   Medium  |                 Wrong DD about GRID agreement update to old OS                 |
|                                 EDH-3635                                |  Bug |  Highest  |        System distributes Metering Data with not existing datetime value       |
|                                 EDH-3790                                |  Bug |  Critical |           CreateCustomer generates customer with already existing EIC          |
|                                 EDH-2876                                |  Bug |   Medium  |        Get Agreements By Customer RPC request commodityType not working        |
|                                 EDH-3685                                |  Bug |  Highest  |  [PARM] Login from EFKP creates several un-necessary customer metadata records |

## 2025-01-17

|   Issue   | Type | Priority |          Title         |
|-----------|------|----------|------------------------|
|  EDH-3733 |  Bug |  Highest |  Dual MPD + Timescale  |

## 2025-01-16

|                                  Issue                                  |  Type  |  Priority |                                                            Title                                                           |
|-------------------------------------------------------------------------|--------|-----------|----------------------------------------------------------------------------------------------------------------------------|
|                                 EDH-3393                                |   Bug  |   Medium  |  TEMP reorganizeMarketModel ignores commodityTypes when doing automatic cache refresh in the end of the reorganize process |
|  [EDH-3636](https://github.com/Elering/estfeed-datahub-docs/issues/157) |  Story |  Critical |                                            Allow to end the GRID agreement today                                           |

## 2025-01-15

|   Issue   | Type | Priority |                              Title                              |
|-----------|------|----------|-----------------------------------------------------------------|
|  EDH-3803 |  Bug |  Highest |  Report generation should not stop at single MP/agreement error |

## 2025-01-10

|   Issue   | Type |  Priority |                                               Title                                               |
|-----------|------|-----------|---------------------------------------------------------------------------------------------------|
|  EDH-3741 |  Bug |  Critical |  temp fails to sync metering points during get-metering-points-by-customer and efkp can't be used |

## 2025-01-09

|                                  Issue                                  | Type |  Priority |                                      Title                                      |
|-------------------------------------------------------------------------|------|-----------|---------------------------------------------------------------------------------|
|  [EDH-3687](https://github.com/Elering/estfeed-datahub-docs/issues/146) |  Bug |  Critical |  POST /api/v1/meter/search searching by customers, doesn't give correct results |

## 2025-01-02

|                                  Issue                                  |  Type  |  Priority |                  Title                 |
|-------------------------------------------------------------------------|--------|-----------|----------------------------------------|
|  [EDH-3636](https://github.com/Elering/estfeed-datahub-docs/issues/157) |  Story |  Critical |  Allow to end the GRID agreement today |

## 2024-12-30

|                                  Issue                                  | Type |  Priority |                                      Title                                      |
|-------------------------------------------------------------------------|------|-----------|---------------------------------------------------------------------------------|
|  [EDH-3687](https://github.com/Elering/estfeed-datahub-docs/issues/146) |  Bug |  Critical |  POST /api/v1/meter/search searching by customers, doesn't give correct results |

## 2024-12-20

|                                  Issue                                  | Type |  Priority |                                Title                               |
|-------------------------------------------------------------------------|------|-----------|--------------------------------------------------------------------|
|  [EDH-3742](https://github.com/Elering/estfeed-datahub-docs/issues/154) |  Bug |  Critical |  Previous SUPPLY should not be restored when new SUPPLY is deleted |

## 2024-12-19

|   Issue   | Type |  Priority |                                           Title                                          |
|-----------|------|-----------|------------------------------------------------------------------------------------------|
|  EDH-3664 |  Bug |  Critical |  The created_time generation logic in the mpd_meter_data_..._history table is incorrect. |

## 2024-12-18

|   Issue   |   Type   |  Priority |                                      Title                                     |
|-----------|----------|-----------|--------------------------------------------------------------------------------|
|  EDH-3678 |    Bug   |  Critical |  DD reports healthy state even though no consumers on dd_distribute_data_req_q |
|  EDH-3707 |  Release |   Medium  |                                 Release 0.23.42                                |

## 2024-12-16

|   Issue   | Type |  Priority |                              Title                             |
|-----------|------|-----------|----------------------------------------------------------------|
|  EDH-3660 |  Bug |  Critical |  Cache out of sync after closing old agreement and opening new |

## 2024-12-13

|   Issue   | Type |  Priority |                              Title                             |
|-----------|------|-----------|----------------------------------------------------------------|
|  EDH-3660 |  Bug |  Critical |  Cache out of sync after closing old agreement and opening new |

## 2024-12-12

|                                  Issue                                  |  Type  |  Priority |                                 Title                                 |
|-------------------------------------------------------------------------|--------|-----------|-----------------------------------------------------------------------|
|  [EDH-3599](https://github.com/Elering/estfeed-datahub-docs/issues/152) |  Story |  Critical |  The PP of the owner of the  MP should not get access to MD or its DD |

## 2024-12-11

|                                  Issue                                  | Type |  Priority |                                    Title                                   |
|-------------------------------------------------------------------------|------|-----------|----------------------------------------------------------------------------|
|                                 EDH-3693                                |  Bug |  Critical |  Can't assign 31.12.2024 as ValidTo date for a P/NS (and other) agreements |
|  [EDH-3686](https://github.com/Elering/estfeed-datahub-docs/issues/147) |  Bug |  Critical |              SUPPLY.validFrom can be more than 48h in the past             |

## 2024-12-09

|   Issue   | Type |  Priority |                            Title                           |
|-----------|------|-----------|------------------------------------------------------------|
|  EDH-2826 |  Bug |   Medium  |    Imperfect metering data excels not imported / notMVP    |
|  EDH-3448 |  Bug |  Critical |  Reports time out querying 15 minute metering data in live |

## 2024-12-07

|                                  Issue                                  | Type |  Priority |                                  Title                                 |
|-------------------------------------------------------------------------|------|-----------|------------------------------------------------------------------------|
|  [EDH-3651](https://github.com/Elering/estfeed-datahub-docs/issues/142) |  Bug |  Critical |  POST /api/v1/agreement/search/meter doesn't work every time correctly |
|                                 EDH-3646                                |  Bug |  Critical |          OPP: Application stops listening to RabbitMQ queue(s)         |

## 2024-12-06

|   Issue   | Type |  Priority |              Title             |
|-----------|------|-----------|--------------------------------|
|  EDH-3649 |  Bug |  Critical |  Joint-invoice files not found |

## 2024-12-05

|   Issue   | Type |  Priority |                                   Title                                   |
|-----------|------|-----------|---------------------------------------------------------------------------|
|  EDH-3617 |  Bug |  Critical |  Metering data is aggregated by UTC days in GetAggregatedMeteringData RPC |

## 2024-12-04

|                                  Issue                                  |  Type  |  Priority |                             Title                            |
|-------------------------------------------------------------------------|--------|-----------|--------------------------------------------------------------|
|                                 EDH-3195                                |  Story |  Critical |  [DD] Distribute deleted GS agreement first and create after |
|  [EDH-3653](https://github.com/Elering/estfeed-datahub-docs/issues/141) |   Bug  |  Critical |         "Name is null" error in PERMISSION DD search         |
|                                 EDH-3646                                |   Bug  |  Critical |     OPP: Application stops listening to RabbitMQ queue(s)    |

## 2024-12-03

|   Issue   | Type |  Priority |                                Title                                |
|-----------|------|-----------|---------------------------------------------------------------------|
|  EDH-3618 |  Bug |  Critical |  opp-api fails to process create meter data requests and loses data |
|  EDH-3611 |  Bug |  Critical |     Customer EIC creation not possible if customer exists in db     |

## 2024-12-02

|   Issue   |  Type  |  Priority |                                Title                                |
|-----------|--------|-----------|---------------------------------------------------------------------|
|  EDH-3483 |  Story |  Critical |              [dbo].[opp_meter_data_status] cleanup task             |
|  EDH-3618 |   Bug  |  Critical |  opp-api fails to process create meter data requests and loses data |
|  EDH-3603 |   Bug  |  Critical |     Wrong response for OPEN_SUPPLIER in "agreement/search/meter"    |

## 2024-11-29

|   Issue   |  Type  |  Priority |                                Title                               |
|-----------|--------|-----------|--------------------------------------------------------------------|
|  EDH-3575 |   Bug  |  Critical |   Agreement DELETE throws error, but delete is actually performed  |
|  EDH-3589 |   Bug  |  Critical |  TEMP: creates duplicate META records (not expiring previous ones) |
|  EDH-3483 |  Story |  Critical |             [dbo].[opp_meter_data_status] cleanup task             |

## 2024-11-28

|   Issue   |  Type  |  Priority |               Title              |
|-----------|--------|-----------|----------------------------------|
|  EDH-3558 |  Story |  Critical |  Crosschecks have commodity type |

## 2024-11-27

|   Issue   | Type |  Priority |                                    Title                                   |
|-----------|------|-----------|----------------------------------------------------------------------------|
|  EDH-3561 |  Bug |  Critical |  DDs to old OS and PP - DELETE extra, UPDATE_BECAUSE_SUPPLY_DELETE missing |

## 2024-11-26

|   Issue   |  Type  |  Priority |                              Title                              |
|-----------|--------|-----------|-----------------------------------------------------------------|
|  EDH-3556 |   Bug  |  Critical |                    PARM: company not created                    |
|  EDH-3483 |  Story |  Critical |            [dbo].[opp_meter_data_status] cleanup task           |
|  EDH-3572 |   Bug  |  Critical |  /api/v1/meter/search/customer is slow for specific customerEic |

## 2024-11-25

|   Issue   | Type |  Priority |                       Title                       |
|-----------|------|-----------|---------------------------------------------------|
|  EDH-3543 |  Bug |  Critical |  UPDATE_BC_SUPPLY_CREATE DD message to future BRP |

## 2024-11-24

|   Issue   | Type |  Priority |                                    Title                                    |
|-----------|------|-----------|-----------------------------------------------------------------------------|
|  EDH-3545 |  Bug |  Critical |  Agreement editor role alone doesn't allow to create new  SUPPLY agreements |

## 2024-11-23

|   Issue   | Type |  Priority |                                    Title                                    |
|-----------|------|-----------|-----------------------------------------------------------------------------|
|  EDH-3545 |  Bug |  Critical |  Agreement editor role alone doesn't allow to create new  SUPPLY agreements |
|  EDH-3356 |  Bug |  Critical |        Service provider sees metering points based on past PARM right       |

## 2024-11-22

|   Issue   | Type |  Priority |                           Title                           |
|-----------|------|-----------|-----------------------------------------------------------|
|  EDH-3533 |  Bug |  Critical |  OPP: quartz not excuting new or updated jobs from config |
|  EDH-3538 |  Bug |  Critical |      MPD does not retry on simple TimescaleDB errors      |
|  EDH-3544 |  Bug |  Critical |      POST customer-authorization/search doesn't work      |

## 2024-11-21

|   Issue   |  Type  |  Priority |                                       Title                                      |
|-----------|--------|-----------|----------------------------------------------------------------------------------|
|  EDH-3306 |  Story |  Critical |               Change the logic of createdTime in /meter-data/status              |
|  EDH-3391 |   Bug  |  Critical |  DD cleanup produces OOMkills, and is expensive on MSSQL CPU and transaction log |
|  EDH-3529 |   Bug  |  Critical |                    PARM-GAVP No CONTACT_EMAIL or CONTACT_PHONE                   |

## 2024-11-20

|   Issue   |  Type  |  Priority |                                Title                               |
|-----------|--------|-----------|--------------------------------------------------------------------|
|  EDH-3494 |  Story |  Critical |      Open Supplier gets too much data with PARM access rights      |
|  EDH-3487 |   Bug  |  Critical |  opp-api meter-data status deadlock while processing metering data |

## 2024-11-19

|   Issue   | Type |  Priority |                                Title                               |
|-----------|------|-----------|--------------------------------------------------------------------|
|  EDH-3396 |  Bug |  Critical |  OPP-API meter-data/status is slow, missing indexes (status, etc)  |
|  EDH-3424 |  Bug |  Critical |  Missing indexes for temp.cdm_customer_meta (high MSSQL CPU usage) |

## 2024-11-18

|   Issue   |  Type  | Priority |               Title              |
|-----------|--------|----------|----------------------------------|
|  EDH-2816 |  Story |  Highest |  [OPP-BE] Improve Agreement flow |

## 2024-11-15

|   Issue   |  Type  |  Priority |                                    Title                                    |
|-----------|--------|-----------|-----------------------------------------------------------------------------|
|  EDH-3446 |   Bug  |  Critical |                DD createdTime is not compliant with ISO-8601                |
|  EDH-3265 |   Bug  |   Medium  |  GS agreement regenerated and DDs are sent about long expired GS agreements |
|  EDH-3454 |   Bug  |  Critical |                      PARM gets from XRC unknown Company                     |
|  EDH-3441 |  Story |  Highest  |     Remove flows from parent border MP-s from Balance Provider 2 report     |

## 2024-11-14

|   Issue   | Type |  Priority |                               Title                               |
|-----------|------|-----------|-------------------------------------------------------------------|
|  EDH-3339 |  Bug |  Critical |  Portfolio agreement modify - Type of customer is incorrect error |

## 2024-11-13

|   Issue   | Type |  Priority |                 Title                |
|-----------|------|-----------|--------------------------------------|
|  EDH-3464 |  Bug |  Critical |  In UI user modify modal not opening |

## 2024-11-11

|   Issue   |   Type   |  Priority |                                  Title                                  |
|-----------|----------|-----------|-------------------------------------------------------------------------|
|  EDH-3430 |    Bug   |   Medium  |            Fix logging level for "Uncompressed message size:"           |
|  EDH-3374 |  Release |   Medium  |                              Release 0.20.0                             |
|  EDH-2493 |   Story  |   Medium  |          DD - change who can access info about Service Provider         |
|  EDH-3409 |   Task   |   Medium  |                     OPP UI - generic modal refactor                     |
|  EDH-3349 |    Bug   |  Critical |              PARM does EAVP request when identity not found             |
|  EDH-3155 |    Bug   |  Highest  |  Balance Provider 2 report is generated for all Open Suppliers / notMVP |

## 2024-11-07

|   Issue   |   Type   |  Priority |                              Title                             |
|-----------|----------|-----------|----------------------------------------------------------------|
|  EDH-3352 |   Story  |  Critical |  [DD] Data distribution search performance improvements - I-II |
|  EDH-3434 |  Release |   Medium  |                         Release 0.22.1                         |

## 2024-11-04

|   Issue   |  Type  |  Priority |                       Title                       |
|-----------|--------|-----------|---------------------------------------------------|
|  EDH-3359 |  Story |  Highest  |    [RPT] Adjust BRP report and BHT calculation    |
|  EDH-3319 |   Bug  |  Critical |  Data distribution search is slow in GO-LIVE test |
|  EDH-3332 |   Bug  |  Highest  |   BHT and Balance Provider report has wrong data  |

## 2024-10-30

|   Issue   |  Type  | Priority |                              Title                              |
|-----------|--------|----------|-----------------------------------------------------------------|
|  EDH-2901 |  Story |  Highest |  [MPM] Implement automatic error handling of Market Model flows |

## 2024-10-25

|   Issue   |  Type  |  Priority |                                         Title                                        |
|-----------|--------|-----------|--------------------------------------------------------------------------------------|
|  EDH-3270 |  Story |  Highest  |                     Report generation responses too big for queue                    |
|  EDH-3062 |   Bug  |   Minor   |                       infinispan: data written out of sequence                       |
|  EDH-2901 |  Story |  Highest  |            [MPM] Implement automatic error handling of Market Model flows            |
|  EDH-2639 |   Bug  |  Critical |  balance-settlement-point/search times out, might cause infinispan outOfMemory error |
|  EDH-3333 |   Bug  |   Medium  |                Error, when some BRP searches balance settlement points               |

## 2024-10-18

|   Issue   |   Type   | Priority|      Title      |
|-----------|----------|---------|-----------------|
|  EDH-3357 |  Release |  Medium |  Release 0.19.1 |

## 2024-10-17

|   Issue   |   Type   |  Priority |                                            Title                                            |
|-----------|----------|-----------|---------------------------------------------------------------------------------------------|
|  EDH-2948 |   Story  |  Highest  |  [MPM] Process Metering Point processes in Agreement flows parallel to increase performance |
|  EDH-3286 |    Bug   |   Medium  |             Metering point search access log - wrong legal basis for AGG and BRP            |
|  EDH-3301 |    Bug   |  Critical |                          Can't give authorization to technical user                         |
|  EDH-3295 |    Bug   |   Medium  |                         MPD - ERROR: ON CONFLICT DO UPDATE 10.10.24                         |
|  EDH-3334 |  Release |   Medium  |                                        Release 0.19.0                                       |

## 2024-10-15

|   Issue   |   Type   |  Priority |                       Title                       |
|-----------|----------|-----------|---------------------------------------------------|
|  EDH-3308 |    Bug   |  Critical |  "POST /meter-data" has random lags in processing |
|  EDH-3315 |  Release |   Medium  |                   Release 0.18.2                  |

## 2024-10-11

|   Issue   |  Type  |  Priority |                            Title                           |
|-----------|--------|-----------|------------------------------------------------------------|
|  EDH-3223 |  Story |  Critical |  Balance Provider 2 report counts border supply agreements |
|  EDH-3289 |   Bug  |   Medium  |  ERROR: duplicate key value violates unique constraint 71  |

## 2024-10-10

|   Issue   |  Type  | Priority|                                         Title                                         |
|-----------|--------|---------|---------------------------------------------------------------------------------------|
|  EDH-3173 |  Story |  Medium |                        Enable JDBC observation in applications                        |
|  EDH-2636 |   Bug  |  Medium |                  Estonian Customer can be created without PERSONAL_ID                 |
|  EDH-2623 |   Bug  |  Minor  |  Latitude/Longitute coordinate fields not shown in the "Edit" modal of Metering Point |

## 2024-10-09

|   Issue   | Type |  Priority |                          Title                         |
|-----------|------|-----------|--------------------------------------------------------|
|  EDH-2960 |  Bug |  Critical |  Unknown Company from Business Registry is not created |

## 2024-10-08

|   Issue   |  Type  | Priority |                             Title                             |
|-----------|--------|----------|---------------------------------------------------------------|
|  EDH-3108 |  Story |  Highest |  Cache loading improvements / tool to add missing MP to cache |
|  EDH-3241 |   Bug  |  Medium  |                      Live Infinispan slow                     |

## 2024-10-03

|   Issue   | Type |  Priority |                                          Title                                          |
|-----------|------|-----------|-----------------------------------------------------------------------------------------|
|  EDH-3246 |  Bug |  Critical |                 TEMP: cache uploading does not work when cache is empty                 |
|  EDH-3216 |  Bug |  Critical |  createBulkMeterData fails immediately when TimescaleDB deadlocked during MDM data send |

## 2024-10-02

|   Issue   |  Type  |  Priority |                                                          Title                                                         |
|-----------|--------|-----------|------------------------------------------------------------------------------------------------------------------------|
|  EDH-3147 |  Story |  Highest  |                         Border point customer has no access border metering point metering data                        |
|  EDH-3087 |  Story |  Critical |  [BREAKING CHANGE] hasContent (boolean) and contentMissingReason have been added to Data distribution search response  |
|  EDH-3175 |  Story |  Highest  |                               Change Open Supplier report to only count Supply agreements                              |
|  EDH-3205 |   Bug  |  Critical |                           Wrong metering points are displayed when searching by Customer EIC                           |
|  EDH-2822 |  Story |  Highest  |                              Improve admin/ agreement-search meter-data-search performance                             |

## 2024-09-27

|   Issue   | Type |  Priority |                     Title                    |
|-----------|------|-----------|----------------------------------------------|
|  EDH-3215 |  Bug |  Critical |  Deadlock issues during agreement operations |

## 2024-09-25

|   Issue   |  Type  |  Priority |                             Title                            |
|-----------|--------|-----------|--------------------------------------------------------------|
|  EDH-2544 |  Story |   Medium  |        TEMP: mpm integrationTests failing on first run       |
|  EDH-2933 |  Task  |  Critical |  DD limit findDataDistributions response max pageSize to 100 |
|  EDH-2815 |  Story |  Highest  |       [OPP-BE] Improve performance of Meter Data Export      |
|  EDH-2664 |   Bug  |   Medium  |        Delete data duplication in swagger definitions        |

## 2024-09-18

|   Issue   |  Type  |  Priority |                                         Title                                        |
|-----------|--------|-----------|--------------------------------------------------------------------------------------|
|  EDH-3017 |  Story |  Highest  |                   DD messages about (BORDER_)GRID agreement delete                   |
|  EDH-3081 |  Story |  Critical |           Metering data read pagination needs to cover 1 year metering data          |
|  EDH-2890 |   Bug  |  Critical |  Automatic empty MP search when starting a new agreement (GO), can cause opp-api OOM |
|  EDH-3077 |  Story |  Highest  |                 Refactor upload infinispan cache in reaorganize flow                 |

## 2024-09-12

|   Issue   |  Type  | Priority |                                Title                                |
|-----------|--------|----------|---------------------------------------------------------------------|
|  EDH-3028 |   Bug  |  Medium  |  Role OPEN_SUPPLIER missing role type VIEW_BALANCE_SETTLEMENT_POINT |
|  EDH-2845 |  Story |  Medium  |                       BHT report to XML format                      |
|  EDH-2900 |  Story |  Highest |              [RPT-BE] Improve performance of Reporting              |
|  EDH-2316 |  Story |  Highest |  [Infinispan] Implement NESTED functionality in Infinispan codebase |

## 2024-08-30

|   Issue   |  Type  |  Priority |                                          Title                                         |
|-----------|--------|-----------|----------------------------------------------------------------------------------------|
|  EDH-2917 |   Bug  |  Critical |         TraceId missing from reporting endpoints after the move to rpt service         |
|  EDH-2951 |   Bug  |  Critical |                    Wrong METERING_DATA DD messages to OPEN_SUPPLIER                    |
|  EDH-2207 |  Task  |  Highest  |                    opp-ui: upgrade keycloak.js from 22.0.5 to 24.0.2                   |
|  EDH-1867 |   Bug  |   Medium  |                    Create Joint Invoice API: NAMED_SUPPLY not found                    |
|  EDH-2750 |  Story |  Highest  |  [TEMP] Improve Meter EIC generation algorithm - 15th char doesn't have to be "-" sign |
|  EDH-2884 |   Bug  |  Critical |                 Many "could not find pathkey item to sort" errors - MPD                |

## 2024-08-15

|   Issue   |  Type  |  Priority |                                         Title                                        |
|-----------|--------|-----------|--------------------------------------------------------------------------------------|
|  EDH-2890 |   Bug  |  Critical |  Automatic empty MP search when starting a new agreement (GO), can cause opp-api OOM |
|  EDH-720  |  Story |   Medium  |                       Implement scheduling of report generation                      |
|  EDH-2538 |   Bug  |  Critical |                      Wrong DD message for OS about GS agreement                      |
|  EDH-2522 |  Story |   Medium  |                              Portfolio agreement UI view                             |
|  EDH-2700 |  Story |  Highest  |                      Cross-check function: mpm_agreement - cache                     |
|  EDH-2850 |   Bug  |  Critical |    Metering data upload (Excel) produces incorrect metering type and reading time    |

## 2024-07-31

|   Issue   |  Type  | Priority|                                   Title                                  |
|-----------|--------|---------|--------------------------------------------------------------------------|
|  EDH-2325 |  Task  |  Medium |  Update OWASP dependency check to major version 10 in other applications |
|  EDH-1684 |  Story |  Medium |  [OPP-UI][OPP-BE] Extend Search metering point flow with implicit access |

## 2024-07-17

|   Issue   |  Type  |  Priority |                                              Title                                              |
|-----------|--------|-----------|-------------------------------------------------------------------------------------------------|
|  EDH-2626 |  Story |  Highest  |                           [RPT] Move Reporting features to new service                          |
|  EDH-2740 |   Bug  |  Highest  |                          [DD] GS agreement is not distributed properly                          |
|  EDH-2507 |   Bug  |  Critical |                         Admin role can delete estfeed admin role via UI                         |
|  EDH-2322 |  Story |   Medium  |             [OPP-BE][MPD] Define observationTime value when gathering Metering Data             |
|  EDH-2533 |  Story |   Medium  |  [OPP][TEMP] Implement solution for updating existing identities with new business object types |

## 2024-07-11

|   Issue   |   Type   |  Priority |                                  Title                                  |
|-----------|----------|-----------|-------------------------------------------------------------------------|
|  EDH-892  |   Story  |   Medium  |  [OPP-UI][OPP-BE][MPD] Metering data search to support data aggregation |
|  EDH-2670 |    Bug   |  Critical |       Existing agreements are not displayed in New agreement form       |
|  EDH-2721 |  Release |   Medium  |                              Release 0.9.0                              |
|  EDH-2538 |    Bug   |  Critical |                Wrong DD message for OS about GS agreement               |
|  EDH-2621 |   Story  |  Highest  |                      [RPT] Create Reporting service                     |

## 2024-07-04

|   Issue   |   Type   | Priority|           Title          |
|-----------|----------|---------|--------------------------|
|  EDH-2697 |  Release |  Medium |  Release 0.8.2 - EI LISA |

## 2024-07-03

|   Issue   |   Type   | Priority|      Title     |
|-----------|----------|---------|----------------|
|  EDH-2669 |  Release |  Medium |  Release 0.8.1 |

## 2024-07-01

|   Issue   |  Type  |  Priority |                                         Title                                        |
|-----------|--------|-----------|--------------------------------------------------------------------------------------|
|  EDH-2639 |   Bug  |  Critical |  balance-settlement-point/search times out, might cause infinispan outOfMemory error |
|  EDH-2615 |  Story |  Critical |               Log related data that caused marketmodel generation error              |

## 2024-06-27

|   Issue   |  Type  | Priority |                       Title                       |
|-----------|--------|----------|---------------------------------------------------|
|  EDH-1639 |  Story |  Medium  |       Use pod name in rabbit connection name      |
|  EDH-2472 |  Story |  Highest |  Superadmin feature for Metering Data (for Green) |

## 2024-06-19

|   Issue   | Type |  Priority |              Title              |
|-----------|------|-----------|---------------------------------|
|  EDH-2584 |  Bug |  Critical |  TEMP & OPP memory optimization |

## 2024-06-13

|   Issue   | Type | Priority|                          Title                          |
|-----------|------|---------|---------------------------------------------------------|
|  EDH-2599 |  Bug |  Medium |  [TEMP] Reogranize market model log and config refactor |

## 2024-06-12

|   Issue   | Type |  Priority |                                Title                               |
|-----------|------|-----------|--------------------------------------------------------------------|
|  EDH-2555 |  Bug |  Critical |  [OPP] Error during GRID_OPERATORS_OPEN_SUPPLIER report generation |

## 2024-06-11

|   Issue   |  Type  | Priority|                                     Title                                     |
|-----------|--------|---------|-------------------------------------------------------------------------------|
|  EDH-712  |  Story |  Medium |                [OPP-BE][MPD] Generate Balance Provider 2 report               |
|  EDH-1864 |   Bug  |  Medium |  Fixed bug when searching joint invoices by dataPeriodStart and dataPeriodEnd |
|  EDH-897  |  Story |  Minor  |                     [OPP-UI] Balance settlement points UI                     |
|  EDH-2499 |   Bug  |  Medium |  [acl] Error: Converted access log request is empty, skip sending access log  |

## 2024-06-03

|   Issue   | Type |  Priority |                Title                |
|-----------|------|-----------|-------------------------------------|
|  EDH-2230 |  Bug |  Critical |  Reorganize Market Model of all MPs |

## 2024-05-29

|   Issue   |  Type  |  Priority |                                   Title                                   |
|-----------|--------|-----------|---------------------------------------------------------------------------|
|  EDH-2509 |   Bug  |  Critical |                 [TEMP] High load queries in DB on startup                 |
|  EDH-2257 |  Story |   Medium  |  [OPP-BE][MPM] POST /meter/search/customer should not use past agreements |
|  EDH-2452 |   Bug  |  Critical |              [Reports] Report fails with Duplicate key error              |

## 2024-05-23

|   Issue   |   Type   | Priority|      Title     |
|-----------|----------|---------|----------------|
|  EDH-2485 |  Release |  Medium |  Release 0.6.1 |

## 2024-05-22

|   Issue   |  Type  | Priority|                                    Title                                    |
|-----------|--------|---------|-----------------------------------------------------------------------------|
|  EDH-344  |  Story |  Medium |                   [OPP-BE] Metering points import via file                  |
|  EDH-711  |  Story |  Medium |                [OPP-BE][MPD] Generate Balance Provider report               |
|  EDH-295  |  Story |  Minor  |            [TEMP] Error messages have temp as service descriptor            |
|  EDH-2327 |  Story |  Medium |                      [CDM] Find customer meta bulk RPC                      |
|  EDH-2044 |   Bug  |  Minor  |    When adding market role to legal person, it takes effect from next day   |
|  EDH-2066 |  Story |  Medium |  [OPP-BE] [MPD] Introduce resolution property to getAggregatedMeterData RPC |
|  EDH-900  |  Story |  Medium |                 [DD] Data distribution table cleanup process                |

## 2024-05-13

|   Issue   | Type | Priority|                          Title                          |
|-----------|------|---------|---------------------------------------------------------|
|  EDH-2408 |  Bug |  Medium |  [DD] Agreement distribution fails for SUPPLY agreement |

## 2024-05-08

|   Issue   | Type |  Priority |                                       Title                                       |
|-----------|------|-----------|-----------------------------------------------------------------------------------|
|  EDH-2396 |  Bug |  Critical |  Unexpected unauthorized error message for some users of some market participants |

## 2024-05-07

|   Issue   |  Type  |  Priority |               Title              |
|-----------|--------|-----------|----------------------------------|
|  EDH-2356 |  Story |  Critical |  Truncate very long log messages |

## 2024-05-02

|   Issue   |  Type  | Priority|                                                  Title                                                  |
|-----------|--------|---------|---------------------------------------------------------------------------------------------------------|
|  EDH-1915 |  Story |  Medium |                 [DD] Extend Create data distribution RPC with other distributed entities                |
|  EDH-1210 |  Story |  Medium |                       [ACL] Balance Settlement Point API /change access log event                       |
|  EDH-1926 |   Bug  |  Minor  |                     [MPD] NetworkBill for ELECTRICITY allows "measurementUnit": "M3"                    |
|  EDH-2044 |   Bug  |  Minor  |                  When adding market role to legal person, it takes effect from next day                 |
|  EDH-1434 |  Task  |  Medium |                                 parm-api: add new purpose with liquibase                                |
|  EDH-1906 |  Story |  Medium |  [MPM] Reorganize aggregation points in balance_state table in case of non-AGGREGATION agreement action |
|  EDH-344  |  Story |  Medium |                                 [OPP-BE] Metering points import via file                                |
|  EDH-723  |  Story |  Medium |                                  [OPP-UI] Reports UI page + REST client                                 |

## 2024-04-29

|   Issue   | Type |  Priority |             Title             |
|-----------|------|-----------|-------------------------------|
|  EDH-2345 |  Bug |  Critical |  Some data distribution fixes |

## 2024-04-25

|   Issue   | Type |  Priority |                                       Title                                       |
|-----------|------|-----------|-----------------------------------------------------------------------------------|
|  EDH-2337 |  Bug |  Critical |  Using ee.. username JWT authentication token fails to authN in Data Distribution |

## 2024-04-18

|   Issue   |  Type  | Priority|                                         Title                                         |
|-----------|--------|---------|---------------------------------------------------------------------------------------|
|  EDH-2098 |  Story |  Medium |                 [PARM][DD] Data distribution - CustomerAuthorizations                 |
|  EDH-742  |  Story |  Medium |                        [ACL] Agreement /search access log event                       |
|  EDH-2195 |   Bug  |  Medium |                  mpd: use timestamp type columns instead timestamptz                  |
|  EDH-713  |  Story |  Medium |                      [OPP-BE][MPD] Generate Grid Operator report                      |
|  EDH-2231 |   Bug  |  Medium |                     API accepts and ignores not-valid attributest                     |
|  EDH-724  |  Story |  Medium |                             [OPP-BE] Reports Excel export                             |
|  EDH-507  |  Story |  Medium |  [OPP-UI][OPP-BE] Add Customer IDs to search filters in agreement search and download |
|  EDH-722  |  Story |  Medium |                       [OPP-BE] Get Reports API /search POST flow                      |

## 2024-04-12

|   Issue   |   Type   | Priority|      Title     |
|-----------|----------|---------|----------------|
|  EDH-2158 |  Release |  Medium |  Release 0.3.0 |

## 2024-03-28

|   Issue   |  Type  | Priority |                                         Title                                         |
|-----------|--------|----------|---------------------------------------------------------------------------------------|
|  EDH-960  |  Story |  Medium  |                 Add new supply, (border)grid or aggregation agreement                 |
|  EDH-507  |  Story |  Medium  |  [OPP-UI][OPP-BE] Add Customer IDs to search filters in agreement search and download |
|  EDH-1677 |  Story |  Medium  |           Turn off AVP flag separately on ELECTRICITY and NATURAL_GAS market          |
|  EDH-2053 |   Bug  |   Minor  |                    ChronoUnit addTo() doesn't account for leap year                   |
|  EDH-713  |  Story |  Medium  |                      [OPP-BE][MPD] Generate Grid Operator report                      |
|  EDH-2036 |  Story |  Medium  |                      [OPP-BE] [MPD] Performance Improvements II.                      |
|  EDH-732  |  Story |  Medium  |                        [ACL] Customer /search access log event                        |
|  EDH-1912 |  Story |  Highest |                         [DD] Create Data distribution service                         |

## 2024-03-25

|   Issue   | Type |  Priority |                            Title                            |
|-----------|------|-----------|-------------------------------------------------------------|
|  EDH-2104 |  Bug |  Critical |  [TEMP-API] findAllMeteringPointsWithAgreements OutOfMemory |

## 2024-03-18

|   Issue   | Type |  Priority |                                   Title                                   |
|-----------|------|-----------|---------------------------------------------------------------------------|
|  EDH-2034 |  Bug |  Critical |  /api/v1/meter returning that ProductionSource is mandatory even if false |

## 2024-03-14

|   Issue   |  Type  | Priority|                                               Title                                              |
|-----------|--------|---------|--------------------------------------------------------------------------------------------------|
|  EDH-1959 |  Story |  Medium |                    Fill audit fields when creating, updating or deleting data                    |
|  EDH-2005 |   Bug  |  Medium |                         VIEW_DATA_DISTRIBUTION is not added to ADMIN role                        |
|  EDH-1169 |   Bug  |  Medium |          System generates BORDER_SUPPLY agreement with no actual validity period length          |
|  EDH-464  |  Story |  Medium |                                 [OPP-BE] EIC API /eic/range flow                                 |
|  EDH-1968 |  Story |  Medium |  [OPP-UI][OPP-BE][TEMP] Introduce location filter in Metering Point /search and /export endpoint |

## 2024-03-06

|   Issue   |  Type  |  Priority |                                  Title                                 |
|-----------|--------|-----------|------------------------------------------------------------------------|
|  EDH-650  |  Story |   Medium  |         [OPP-BE] Balance Settlement Point API /change POST flow        |
|  EDH-2068 |   Bug  |   Medium  |    OPP - Open API incorrectly generates responses in case of errors.   |
|  EDH-1123 |   Bug  |  Critical |  [MPM] Update SUPPLY agreement - allows termination on the current day |

## 2024-02-29

|   Issue   |  Type  | Priority |                                            Title                                           |
|-----------|--------|----------|--------------------------------------------------------------------------------------------|
|  EDH-2007 |  Task  |  Highest |                 ACL_VIEW_Access_Log 1 month restriction needs to be removed                |
|  EDH-1952 |  Story |  Medium  |                      [OPP-BE][MPD][Cache] Performance Improvements I.                      |
|  EDH-1715 |  Story |  Medium  |  [MPM] Introduce TSO role and determine Balance Responsible Parties in balance_state_table |
|  EDH-1709 |  Story |  Medium  |       [MPM] Reorganize balance_state table in case of CREATE NAMED SUPPLIER agreement      |
|  EDH-456  |  Story |  Medium  |                      [OPP-BE] Metering data export - Populate template                     |
|  EDH-467  |  Story |  Medium  |                    [OPP-UI] Metering data import via file + validations                    |

## 2024-02-21

|   Issue   | Type | Priority|                          Title                          |
|-----------|------|---------|---------------------------------------------------------|
|  EDH-1977 |  Bug |  Medium |  Meter data does not save despite the SUCCESSFUL result |

## 2024-02-15

|   Issue   |  Type  | Priority|                        Title                       |
|-----------|--------|---------|----------------------------------------------------|
|  EDH-1752 |  Story |  Medium |  [MPD] Implement getAggregatedMeterData RPC server |
|  EDH-1510 |  Story |  Medium |    [OPP-BE] Implement POST /api/v1/customer flow   |
|  EDH-491  |  Story |  Medium |   [OPP-UI] Metering data status UI page + client   |
|  EDH-344  |  Story |  Medium |      [OPP-BE] Metering points import via file      |
|  EDH-921  |  Story |  Medium |              Customer PUT API and flow             |

## 2024-02-08

|   Issue   | Type | Priority |                          Title                          |
|-----------|------|----------|---------------------------------------------------------|
|  EDH-1904 |  Bug |  Highest |  temp-api infinite loop on "find_customer_meta" request |

## 2024-01-31

|   Issue   |  Type  | Priority|                              Title                              |
|-----------|--------|---------|-----------------------------------------------------------------|
|  EDH-468  |  Story |  Medium |       [OPP-BE] Metering data import via file + validations      |
|  EDH-1692 |  Story |  Medium |  [OPP-BE] Modify OPP POST /api/v1/authorization/delete API flow |

## 2024-01-18

|   Issue   |  Type  | Priority |                          Title                         |
|-----------|--------|----------|--------------------------------------------------------|
|  EDH-692  |  Story |  Medium  |            [MPM] Create Balance State model            |
|  EDH-626  |  Story |  Medium  |           Network Bill API /search POST flow           |
|  EDH-796  |  Story |  Medium  |          [AUTHZ] Create Market Role RPC server         |
|  EDH-483  |  Story |  Medium  |  [OPP-UI] User authorization UI page + REST API client |
|  EDH-344  |  Story |  Medium  |        [OPP-BE] Metering points import via file        |
|  EDH-1103 |   Bug  |  Highest |              MP can be found with a delay              |

## 2024-01-15

|   Issue   | Type | Priority |        Title        |
|-----------|------|----------|---------------------|
|  EDH-1724 |  Bug |  Highest |  temp-api deadlocks |

## 2023-12-19

|   Issue   |  Type  | Priority|                 Title                |
|-----------|--------|---------|--------------------------------------|
|  EDH-1529 |  Story |  Medium |  [IDR] Implement generateEic RPC API |

## 2023-12-14

|   Issue   |  Type  | Priority|                          Title                          |
|-----------|--------|---------|---------------------------------------------------------|
|  EDH-1537 |  Story |  Medium |                 Master Data Generator I.                |
|  EDH-455  |  Story |  Medium |     [OPP-UI] Metering data export - General features    |
|  EDH-337  |  Story |  Medium |  [OPP-UI] Metering points import via file + validations |
|  EDH-1510 |  Story |  Medium |      [OPP-BE] Implement POST /api/v1/customer flow      |
|  EDH-596  |  Story |  Minor  |   [MPD] Create metering data - error message contents   |
|  EDH-1221 |  Story |  Medium |      [MPM] Introduce General Service in DB and APIs     |

## 2023-11-30

|   Issue   |  Type  |  Priority |                                      Title                                     |
|-----------|--------|-----------|--------------------------------------------------------------------------------|
|  EDH-1546 |  Story |  Critical |                         Add name to RequestCustomerEIC                         |
|  EDH-625  |  Story |   Medium  |                         Joint invoice /create bulk API                         |
|  EDH-733  |  Story |   Medium  |                     Joint invoice /search access log event                     |
|  EDH-624  |  Story |   Medium  |                           Get Network Bill RPC server                          |
|  EDH-1136 |  Story |   Medium  |  [AUTHZ] Use External ID of User in Authorization flow instead of Internal ID  |
|  EDH-346  |  Story |   Medium  |     [OPP-UI] Navigate from Metering points page to Agreements with filters     |
|  EDH-980  |  Story |   Medium  |  [OPP-UI] Add sourceType filter to OPP-UI and OPP-BE related to Metering Point |

## 2023-11-16

|   Issue   |  Type  | Priority|                            Title                            |
|-----------|--------|---------|-------------------------------------------------------------|
|  EDH-638  |  Story |  Medium |             Joint Invoice API /search POST flow             |
|  EDH-734  |  Story |  Medium |           Metering point /search access log event           |
|  EDH-627  |  Story |  Medium |                Create Network Bill RPC server               |
|  EDH-1959 |  Story |  Medium |  Fill audit fields when creating, updating or deleting data |
|  EDH-403  |  Story |  Minor  |                  [OPP] Update Access Token                  |
|  EDH-450  |  Story |  Medium |   [OPP-BE] Metering Point API /meter/search/customer flow   |

## 2023-11-06

|   Issue   | Type | Priority|                         Title                         |
|-----------|------|---------|-------------------------------------------------------|
|  EDH-1463 |  Bug |  Medium |  EIC validation fails for EIC code "28ZNG-10000006-0" |

## 2023-10-27

|   Issue  |  Type  | Priority|              Title              |
|----------|--------|---------|---------------------------------|
|  EDH-728 |  Story |  Medium |  Set up Access Log microservice |

## 2023-10-18

|   Issue   | Type |  Priority |                                         Title                                        |
|-----------|------|-----------|--------------------------------------------------------------------------------------|
|  EDH-1070 |  Bug |  Highest  |            [MPM] Create agreements - supplier change 14 days ahead fails             |
|  EDH-1355 |  Bug |  Critical |                [XYZ] cache meteringPointsByServiceProvider not filled                |
|  EDH-1075 |  Bug |  Highest  |  [OPP-UI] Named Supplier agreement creation requests external id to bhave EIC format |

## 2023-10-11

|   Issue   |  Type  | Priority|                                                         Title                                                        |
|-----------|--------|---------|----------------------------------------------------------------------------------------------------------------------|
|  EDH-1045 |  Story |  Minor  |                                             [MPD] Upgrade to Gradle 8.0+                                             |
|  EDH-1046 |  Story |  Minor  |                                            [AUTHZ] Upgrade to Gradle 8.0+                                            |
|  EDH-449  |  Story |  Medium |                       [OPP-UI] Navigate from Metering data page to Metering points with filters                      |
|  EDH-496  |  Story |  Medium |                                      [OPP-BE] Metering points API authorization                                      |
|  EDH-953  |  Story |  Minor  |                                             [PARM] Upgrade to Gradle 8.0+                                            |
|  EDH-962  |  Story |  Medium |  [OPP-BE][OPP-UI] Authorization - Find Metering Points By Owner EIC and Role - GO, AGR, LO, ISO, PO, CPO perspective |

## 2023-09-28

|   Issue   |  Type  | Priority |                                  Title                                 |
|-----------|--------|----------|------------------------------------------------------------------------|
|  EDH-548  |  Story |  Medium  |  [OPP-UI][OPP-BE][MPM] Add user defined Agreement ID to search filters |
|  EDH-1255 |   Bug  |  Highest |                    [PARM] [TEMP] Serialization issue                   |
|  EDH-1022 |  Story |  Medium  |        [OPP-BE/AUTHZ] Filter user roles by service provider role       |

## 2023-09-18

|   Issue   |  Type  | Priority|                         Title                         |
|-----------|--------|---------|-------------------------------------------------------|
|  EDH-1000 |  Story |  Medium |                [TEMP] SpringBoot update               |
|  EDH-454  |  Story |  Medium |    [OPP-BE] Metering Data API /meter-data POST flow   |
|  EDH-889  |  Story |  Medium |      [MPD] Modify Create Metering Data RPC server     |
|  EDH-939  |   Bug  |  Medium |  [OPP-UI] Metering data - IN values are not displayed |
|  EDH-1139 |   Bug  |  Medium |                   Deadlock: parm-api                  |

## 2023-09-05

|   Issue   |  Type  | Priority|                                                 Title                                                 |
|-----------|--------|---------|-------------------------------------------------------------------------------------------------------|
|  EDH-1001 |  Story |  Medium |                                        [PARM] SpringBoot update                                       |
|  EDH-941  |  Story |  Medium |                                  [MPM] Introduce Metering Point Type                                  |
|  EDH-1002 |  Story |  Medium |                                        [MPD] SpringBoot update                                        |
|  EDH-844  |  Story |  Medium |                           [OPP-BE] Update agreement API /agreement PUT flow                           |
|  EDH-840  |  Story |  Medium |  [TEMP] Check if Market Participant is Owner of Metering Point in when Creating or Updating Agreement |

## 2023-08-23

|   Issue   | Type | Priority|             Title            |
|-----------|------|---------|------------------------------|
|  EDH-1078 |  Bug |  Medium |  AVP messages duplicate Id-s |

## 2023-08-17

|   Issue   |  Type  | Priority|                        Title                        |
|-----------|--------|---------|-----------------------------------------------------|
|  EDH-864  |  Story |  Medium |        [OPP-BE] Modify GET /agreements flow         |
|  EDH-453  |  Story |  Medium |         [OPP-BE] Create Metering data client        |
|  EDH-330  |  Story |  Medium |  [OPP-UI] Border points UI based on Metering points |
|  EDH-1003 |  Story |  Medium |              [AUTHZ] SpringBoot update              |

## 2023-08-14

|   Issue  |  Type  | Priority|                     Title                     |
|----------|--------|---------|-----------------------------------------------|
|  EDH-480 |  Story |  Medium |  [OPP-BE] Check user context in HTTP requests |

## 2023-07-19

|   Issue  |  Type  | Priority|                                          Title                                         |
|----------|--------|---------|----------------------------------------------------------------------------------------|
|  EDH-852 |  Story |  Medium |  [OPP-BE][MPM] Extend get agreement flow to give back the external ID of the agreement |
|  EDH-938 |  Story |  Medium |     [MPM] Introduce BORDER_GRID and BORDER_SUPPLY type of agreements non-TEMP side     |
|  EDH-444 |  Story |  Medium |                   [OPP-BE] User Market Role selector REST API server                   |
|  EDH-445 |  Story |  Medium |                    [OPP-UI] Metering data export - General features                    |
|  EDH-858 |  Story |  Medium |                   [MPD] Extend application properties with resolution                  |

## 2023-07-13

|   Issue   | Type |  Priority |                      Title                     |
|-----------|------|-----------|------------------------------------------------|
|  EDH-1015 |  Bug |  Critical |  duplicate metering points in temp-api v0.17.0 |

## 2023-07-06

|   Issue  |  Type  | Priority|                               Title                              |
|----------|--------|---------|------------------------------------------------------------------|
|  EDH-583 |  Story |  Medium |              [MPM] Update agreements RPC server 1/2              |
|  EDH-512 |  Story |  Medium |          [OPP-BE] GET /api/v1/meter/border REST API flow         |
|  EDH-862 |  Story |  Medium |       [OPP-UI] Check user context in HTTP requests frontend      |
|  EDH-888 |  Story |  Medium |                 [MPD] Change Metering Data model                 |
|  EDH-854 |  Story |  Medium |  [AUTHZ] Get authorization by Market Participant Role RPC server |

## 2023-06-22

|   Issue  |  Type  |  Priority |                                   Title                                   |
|----------|--------|-----------|---------------------------------------------------------------------------|
|  EDH-937 |   Bug  |  Critical |                      Getting null in temp-api v0.15.x                     |
|  EDH-576 |  Story |   Medium  |                [TEMP] EIC service provider range validation               |
|  EDH-481 |  Story |   Medium  |               [OPP-BE] Create user authorization RPC client               |
|  EDH-803 |  Story |   Medium  |                    [OPP-UI] Named Supplier Agreement UI                   |
|  EDH-851 |   Bug  |   Minor   |  [MPD/OPP-BE] Pagination for metering data query allows decimals for page |

## 2023-06-08

|   Issue  |  Type  | Priority|                     Title                     |
|----------|--------|---------|-----------------------------------------------|
|  EDH-335 |  Story |  Medium |  [OPP-BE] Metering Point API /meter POST flow |
|  EDH-478 |  Story |  Medium |  [AUTHZ] Create user authorization RPC server |

## 2023-05-15

|   Issue  |  Type  | Priority|                                            Title                                           |
|----------|--------|---------|--------------------------------------------------------------------------------------------|
|  EDH-443 |  Story |  Medium |                         [OPP-BE] Get user authorization RPC client                         |
|  EDH-447 |  Story |  Medium |                        [OPP-UI] Metering data UI page + REST client                        |
|  EDH-591 |   Bug  |  Minor  |  [MPD] Create metering data - billingSequence - allows decimals and shouldn't be mandatory |

## 2023-05-10

|   Issue  |  Type  | Priority|                    Title                   |
|----------|--------|---------|--------------------------------------------|
|  EDH-345 |  Story |  Medium |  [AUTHZ] Get user authorization RPC server |

## 2023-04-20

|   Issue  |  Type  | Priority|                                  Title                                  |
|----------|--------|---------|-------------------------------------------------------------------------|
|  EDH-748 |  Story |  Medium |           [PARM] Extend Get received permissions with filters           |
|  EDH-593 |   Bug  |  Minor  |  [MPD] Create metering data - error 500 when request has no pos element |

## 2023-03-31

|   Issue  | Type | Priority|                       Title                      |
|----------|------|---------|--------------------------------------------------|
|  EDH-541 |  Bug |  Medium |  parentMeterEic should be optional search filter |

## 2022-12-08

|   Issue  |  Type  | Priority|                               Title                               |
|----------|--------|---------|-------------------------------------------------------------------|
|  EDH-254 |  Task  |  Medium |  [TEMP] Limit Agreement scope in Get Metering points for Customer |
|  EDH-259 |  Story |  Medium |           [OPP] Implement Metering Point REST API server          |

## 2022-11-25

|   Issue  |  Type  | Priority |                       Title                       |
|----------|--------|----------|---------------------------------------------------|
|  EDH-265 |  Story |  Highest |  [TEMP] IDR - Resolve disjoined identites problem |

## 2022-11-24

|   Issue  |  Type  | Priority|                    Title                    |
|----------|--------|---------|---------------------------------------------|
|  EDH-256 |  Story |  Medium |  [OPP] Implement Agreements REST API server |

## 2022-11-22

|   Issue  | Type | Priority |        Title       |
|----------|------|----------|--------------------|
|  EDH-266 |  Bug |  Highest |  IDR cases problem |

## 2022-11-10

|   Issue  |  Type  |Priority|                   Title                   |
|----------|--------|--------|-------------------------------------------|
|  EDH-205 |  Story |  Minor |  [TEMP] CDM API - Create Cutomer Metadata |

## 2022-10-24

|   Issue  |  Type |Priority|                     Title                     |
|----------|-------|--------|-----------------------------------------------|
|  EDH-250 |  Task |  Minor |  Remove Elering specific data from Liquibase. |

## 2022-10-21

|   Issue  |  Type  | Priority |                          Title                          |
|----------|--------|----------|---------------------------------------------------------|
|  EDH-189 |  Story |  Highest |  [TEMP] Metadata API - Get Metering points for Customer |

