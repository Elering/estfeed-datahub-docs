# Reports

## Table of contents

<!-- TOC -->
* [Reports](#reports)
  * [Table of contents](#table-of-contents)
  * [Introduction](#introduction)
  * [Generating reports](#generating-reports)
  * [Transmitting reports](#transmitting-reports)
    * [API messages](#api-messages)
      * [Messages](#messages)
  * [Report descriptions](#report-descriptions)
    * [Grid operator report](#grid-operator-report)
    * [Open supplier report](#open-supplier-report)
    * [Open supplier summary report](#open-supplier-summary-report)
    * [Grid operator open supplier report](#grid-operator-open-supplier-report)
    * [Balance management report](#balance-management-report)
    * [Balance responsible party report No. 2](#balance-responsible-party-report-no-2)
    * [BHT report](#bht-report)
    * [Report of Non-Remote Read Metering Points](#report-of-non-remote-read-metering-points)
    * [Forecast Report of Non-Remote Read Metering Points](#forecast-report-of-non-remote-read-metering-points)
    * [Grid Operator Customer Report](#grid-operator-customer-report)
<!-- TOC -->

## Introduction

The Datahub regularly generates reports for open suppliers, grid operators and balance responsible parties.

## Generating reports

Summary reports are calculated and forwarded according to the following schedule:

- Daily reports approximately by 14:00 with the previous day’s metering data (including metering data from the beginning of the current calendar month).
- On the 1st day of the calendar month, the metering data from two and three months back are calculated retrospectively per calendar month.
- On the 8th day of the calendar month (00:00-01:00 in the first balance period), the metering data for the previous calendar month are calculated, which form the basis for the initial balance report.

Example of calculation times of aggregated data for balance reports:

|                        | January metering data summary report | February metering data summary report | March metering data summary report |
|------------------------|--------------------------------------|---------------------------------------|------------------------------------|
| Initial balance report | 8 February                           | 8 March                               | 8 April                            |
| Final balance report   | 1 April                              | 1 May                                 | 1 June                             |

> [!NOTE]
> The reports are calculated simultaneously for all electricity market operators and simultaneously for all gas market operators.

## Transmitting reports

- The reports are available to the parties through both the web interface and API.
- Operators can download each report as follows:
  - Using the API in JSON or EXCEL format
  - Using the web interface in EXCEL format

### API messages

#### Messages

| Message                                   | Objective                       |
|-------------------------------------------|---------------------------------|
| `POST /api/{version}/report/search`       | Find reports                    |
| `POST /api/{version}/report/export/excel` | Download report in Excel format |
| `POST /api/{version}/report/export/json`  | Download report in JSON format  |

## Report descriptions

All reports contain data for one calendar month. Most of the reports have been prepared by balance period. Consumption and production are indicated separately. Only data from metering points with valid grid agreements will be taken into account.

### Grid operator report

Recipients:

- **Grid operators**.

Frequency:

| | Electricity | Gas |
|---|---|---|
| Once per day, D+1 data aggregation takes place | at 10:00 (available approx. at 14:00) | at 14:00 (available approx. at 18:00) |
| Once per month on the 8th, M+1 data aggregation takes place | at 00:00 (available approx. at 10:00) | at 14:00 (available approx. at 18:00) |
| Once per month on the 1st, M+2 and M+3 data aggregation takes place | at 00:00 (available approx. at 07:00) | at 14:00 (available approx. at 18:00) |

Data:

- aggregated metering data of the amount that entered the grid through the grid operator’s border points (report page "GO_IN_LOSSES_PORTFOLIO");
- the amounts leaving the grid operator’s grid, indicated separately:
  - final amounts per open supplier – not including border metering points where the customer of the grid agreement is another grid operator + the grid operator’s grid loss metering point. The grid operator itself is also indicated as an open supplier if it acts as a seller and has sales agreements with market participants (report page "GO_OS_OUT");
  - the amount of the general service (there is a grid agreement in the standard metering point, but no sales agreement) (report page "GO_OS_OUT");
  - amounts per grid operator – sum of the border metering points per grid operator (report page "GO_GO_OUT");
- grid operator grid loss calculation: amounts entering – amounts leaving the grid (report page "GO_IN_LOSSES_PORTFOLIO");
- the aggregated amount of the grid operator’s own = own sales portfolio + general service + grid losses (report page "GO_IN_LOSSES_PORTFOLIO").

Column descriptions:

- **PAGE "GO GO OUT"**:
  - Sub-grid operator EIC (gridOperatorEIC)
  - Sub-grid operator – name of the sub-grid operator (gridOperatorName)
  - GO open supplier EIC – sub-grid operator’s open supplier EIC (gridOperatorBalanceProviderEIC)
  - GO open supplier – sub-grid operator’s open supplier name (gridOperatorBalanceProviderName)
  - Grid operator EIC (parentGridProviderEIC)
  - Grid operator – name of the grid operator (parentGridProviderName)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - Amounts entering the grid, kWh – amounts entering the grid of a grid operator from the grid of the sub-grid operator (inQuantity)
  - Amounts leaving the grid, kWh – amounts leaving the grid of a grid operator to the grid of the sub-grid operator (outQuantity)
  - Amounts entering the grid, m³ – amounts entering the grid of a grid operator from the grid of the sub-grid operator (gas reports only)
  - Amounts leaving the grid, m³ – amounts leaving the grid of a grid operator to the grid of the sub-grid operator (gas reports only)
  - Number of border metering points (meteringPointsTotal)
- **PAGE "GO OS OUT"**:
  - Grid operator EIC – EIC code of the grid operator (gridOperatorEIC)
  - Grid operator – name of the grid operator (gridOperatorName)
  - Open supplier EIC – open supplier’s EIC at the metering point of the grid agreement. (openSupplierEIC)
  - Open supplier – open supplier at the metering point of the grid agreement. (openSupplierName)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - Amounts entering the grid, kWh – amounts entering the grid of a grid operator from metering points that have a valid grid agreement and are not border metering points. Also general service is counted. (Pin) (inQuantityPortfolio)
  - Amounts leaving the grid, kWh – amounts leaving the grid of a grid operator from metering points that have a valid grid agreement and are not border metering points. Also general service is counted. (Pout) (outQuantityPortfolio)
  - Amounts entering the grid, m³ – gas volume in cubic metres (gas reports only)
  - Amounts leaving the grid, m³ – gas volume in cubic metres (gas reports only)
  - Number of metering points, pcs – number of metering points with a grid agreement (meteringPointsTotal)
- **PAGE "GO_IN_LOSSES_PORTFOLIO":**
  - Grid operator EIC – EIC code of the grid operator (gridOperatorEIC)
  - Grid operator – name of the grid operator (gridOperatorName)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - GO portfolio total kWh, Pin: Pin general service + Pin GO sales agreement (inQtyPortfolioGridOperator)
  - GO portfolio total kWh, Pout: Pout general service + Pout GO sales agreement + Pout grid loss (outQtyPortfolioGridOperator)
  - Quantity entering the grid (border metering points) – kWh: quantity entered into the grid from the master grid operator’s grid, kWh (inQuantityBorderPoints)
  - Quantity leaving the grid (border metering points) – kWh: quantity exited from the grid to other grid operators, kWh (outQuantityBorderPoints)
  - GO grid loss, kWh (qtyLosses)
    - Calculation: from master grid operator border metering points (Pin-Pout) – GO grid metering points with a valid grid agreement (Pout-Pin).
  - Only in gas reports:
    - GO portfolio consumption – kWh (goPortfolioConsumption)
      - Calculation: outQuantityPortfolioGridOperator + GO_OS_OUT.outQuantityPortfolio (general service quantities) + quantityLosses
    - GO portfolio total – m³, Pin: Pin universal service + Pin GO saled agreement (inQtyPortfolioGridOperatorM3)
    - GO portfolio total – m³, Pout: Pout universal service + Pout GO saled agreement + Pout grid losses (outQtyPortfolioGridOperatorM3)
    - Quantity entered into the grid (border metering points) – m³: quantity entered into the grid from the transmission system operator’s grid, m³ (inQuantityBorderPointsM3)
    - Quantity exited from the grid (border metering points) – m³: quantity exited from the grid to other grid operators, m³ (outQuantityBorderPointsM3)
    - GO portfolio consumption – m³ (goPortfolioConsumptionM3)
    - Ggrid losses – m³ (quantityLossesM3)

### Open supplier report

Recipients:

- **Open suppliers**

Frequency:

| | Electricity | Gas |
|---|---|---|
| Once per day, D+1 data aggregation takes place | at 10:00 (available approx. at 14:00) | at 14:00 (available approx. at 18:00) |
| Once per month on the 8th, M+1 data aggregation takes place | at 00:00 (available approx. at 10:00) | at 14:00 (available approx. at 18:00) |
| Once per month on the 1st, M+2 and M+3 data aggregation takes place | at 00:00 (available approx. at 07:00) | at 14:00 (available approx. at 18:00) |


Data:

- Amounts aggregated in the open supply portfolio by open suppliers and grid area for all metering points for which there is an open electricity supply agreement – not including border metering points where the customer of the grid agreement is another grid operator.

Column descriptions:

- **PAGE "OS_GO"**:
  - Open supplier EIC – open suppliers of the entire OS portfolio, including itself (openSupplierEIC)
  - Open supplier name – same as above (openSupplierName)
  - Grid operator EIC – EIC of the grid operator of the metering point (gridOperatorEIC)
  - Grid operator name – name of the grid operator of the metering point (gridOperatorName)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - Amounts entering the grid from the end customer, kWh – Pin amount entering the grid (all metering points that have a valid grid agreement and are not a GO-GO border point) (inQuantityPortfolio)
  - Amounts leaving the grid to the end customer, kWh – Pout amount leaving the grid of the grid operator (all metering points that have a valid grid agreement and are not a GO-GO border point) (outQuantityPortfolio)
  - Amounts entering the grid from the end customer, m³ (inQuantityPortfolioM3) (gas market only)
  - Amounts leaving the grid to the end customer, m³ (outQuantityPortfolioM3) (gas market only)
  - Amounts entering an isolated grid from the end customer, kWh – Pin amount entering the isolated grid (all isolated metering points that have a valid grid agreement and are not a GO-GO border point) (inQuantityIsolated) (electricity market only)
  - Amounts leaving an isolated grid to the end customer, kWh – Pout amount leaving the isolated grid (all isolated metering points that have a valid grid agreement and are not a GO-GO border point) (outQuantityIsolated) (electricity market only)
  - Number of metering points, pcs (meteringPointsTotal)

### Open supplier summary report

> [!WARNING] 
> Open supplier summary report is not in the initial scope

Recipients:

- **Open suppliers**

Frequency:

- The time of calculation (day and time) is set by the admin – it is calculated once at the beginning of the calendar month for the previous month.

Data:

Monthly amounts of open suppliers in the open supply portfolio by metering points and customers on the basis of open supply agreements.

Column descriptions:

- Data for the calendar month for each metering point with a valid grid agreement:
  - **PAGE "OS_CAHIN":**
    - Customer EIC – end consumer EIC (customerEIC)
    - Metering point EIC – end consumer metering point EIC (not including GO-GO points) (meteringPointEIC)
    - Open Supplier EIC – EIC of the open supplier at the metering point (openSupplierEIC)
    - Open supplier name – name of the open supplier at the metering point (openSupplierName)
    - Grid operator EIC – EIC of the grid operator of the metering point (gridOperatorEIC)
    - Grid operator name – name of the grid operator of the metering point (gridOperatorName)
    - Start of open supplier agreement – start time of the open supplier agreement at the metering point (osAgreementStart)
    - End of open supplier agreement – end time of the open supplier agreement at the metering point (osAgreementEnd)
    - Calculation period – calendar month (period)
    - Amount entering the grid from the end customer, kWh (inQuantity)
    - Amount leaving the grid to the end customer, kWh (outQuantity)

### Grid operator open supplier report

Recipients:

- **Grid operator open supplier**

Frequency:

| | Electricity | Gas |
|---|---|---|
| Once per day, D+1 data aggregation takes place | at 10:00 (available approx. at 14:00) | at 14:00 (available approx. at 18:00) |
| Once per month on the 8th, M+1 data aggregation takes place | at 00:00 (available approx. at 10:00) | at 14:00 (available approx. at 18:00) |
| Once per month on the 1st, M+2 and M+3 data aggregation takes place | at 00:00 (available approx. at 07:00) | at 14:00 (available approx. at 18:00) |

Data:

- aggregated metering data of the amount that entered the grid through the grid operator’s border points;
- the amounts leaving the grid operator’s grid, indicated separately:
  - final amounts of all open suppliers’ metering points for which there is an open supply agreement – not including border metering points where the customer of the grid agreement is another grid operator;
  - general service (there is a grid agreement in the standard metering point, but no sales agreement);
  - amount as a customer of other grid operators – sum of border metering points for grid operators (customer);
- grid operator’s grid loss.

Column descriptions:

- **PAGE "GO_IN_BORDER_OS"**
  - Grid operator EIC – EIC code of the grid operator (gridOperatorEIC)
  - Grid operator – name of the grid operator (gridOperatorName)
  - GO open supplier EIC – grid operator’s open supplier EIC (gridOperatorBalanceProviderEIC)
  - GO open supplier – grid operator’s open supplier name (gridOperatorBalanceProviderName)
  - Master grid operator EIC (parentGridProviderCustomerEIC)
  - Master grid operator – name of the master grid operator (parentGridProviderCustomerName)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - Amounts entering the grid, kWh – amounts entering the grid of a grid operator from the master grid operator (inQuantity)
  - Amounts leaving the grid, kWh – amounts leaving the grid of a grid operator to the grid of the master grid operator (outQuantity)
  - Amounts entering the grid, m³ – amounts entering the grid of a grid operator from the master grid operator (inQuantityM3) (gas market only)
  - Amounts leaving the grid, m³ – amounts leaving the grid of a grid operator to the grid of the master grid operator (outQuantityM3) (gas market only)
  - Number of metering points, pcs (meteringPointsTotal)
- **PAGE "GO_OUT_BORDER_OS"**
  - Sub-grid operator EIC (gridOperatorEIC)
  - Sub-grid operator – name of the sub-grid operator (gridOperatorName)
  - GO open supplier EIC – master grid operator’s open supplier EIC (gridOperatorBalanceProviderEIC)
  - GO open supplier – name of the open supplier of the master grid operator (gridOperatorBalanceProviderName)
  - Grid operator EIC (parentGridProviderCustomerEIC)
  - Grid operator name (parentGridProviderCustomerName)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - Amounts entering the grid, kWh – amounts entering the grid of a grid operator from the sub-grid operator (inQuantity)
  - Amounts leaving the grid, kWh – amounts leaving the grid of a grid operator to the grid of the sub-grid operator (outQuantity)
  - Amounts entering the grid, m³ – amounts entering the grid of a grid operator from the sub-grid operator (inQuantityM3) (gas market only)
  - Amounts leaving the grid, m³ – amounts leaving the grid of a grid operator to the grid of the sub-grid operator (outQuantityM3) (gas market only)
  - Number of metering points, pcs (meteringPointsTotal)
- **PAGE "GO_OS_GO"**
  - Grid operator EIC – EIC code of the grid operator (gridOperatorEIC)
  - Grid operator – name of the grid operator (gridOperatorName)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - Amounts entering the grid from an end customer with a grid and electricity agreement, kWh – Pin amount entering the grid (production) (inQtyWithAgr)
  - Amounts leaving the grid to an end customer with a grid and electricity agreement, kWh – Pout amount leaving the grid of the grid operator (consumption) (outQtyWithAgr)
  - Amounts entering the grid from a general service end customer with a grid agreement, kWh – Pin amount entering the grid (production) (inQtyPortfolioLastResortSupply)
  - Amounts leaving the grid to a general service end customer with a grid agreement, kWh – Pout amount leaving the grid of the grid operator (consumption) (outQtyPortfolioLastResortSupply)
  - Amounts entering the grid from the master grid operator’s grid, kWh – amounts entering the grid of the grid operator at border metering points (inQuantityBorder)
  - Amounts leaving the grid to the grid of the master grid operator, kWh – amounts leaving the grid of the grid operator at border metering points (Pout) (outQuantityBorder)
  - Grid operator grid loss, kWh (qtyLosses)
  - Number of border metering points, pcs (meteringPointsTotalBorder)
  - Number of metering points, pcs (meteringPointsTotal)
  - Only in gas reports:
    - Quantity entered into the grid from a last‑resort supply end customer under a grid agreement, m³ – quantity entered into the grid Pin (production) (inQtyPortfolioLastResortSupplyM3)
    - Quantity exited from the grid to a last‑resort supply end customer under grid agreement, m³ – quantity exited from the grid Pout (consumption) (outQtyPortfolioLastResortSupplyM3)
    - Quantity entered into the grid from the upstream grid operator’grid, m³ – quantity entered into the grid from the upstream grid operator’grid at border metering points (inQuantityBorderM3)
    - Quantity exited from the grid to the upstream grid operator’grid, m³ – quantity exited from the grid by the grid operator at border points (Pout) (outQuantityBorderM3)
    - Grid operatogrid losses, m³ (qtyLossesM3)
    - Grid operator portfolio consumption, kWh (goPortfolioConsumption)
    - Grid operator portfolio consumption, m³ (goPortfolioConsumptionM3)

### Balance management report

Recipients:

- **Balance responsible parties**

Frequency:

| | Electricity | Gas |
|---|---|---|
| Once per day, D+1 data aggregation takes place | at 10:00 (available approx. at 14:00) | at 14:00 (available approx. at 18:00) |
| Once per month on the 8th, M+1 data aggregation takes place | at 00:00 (available approx. at 10:00) | at 14:00 (available approx. at 18:00) |
| Once per month on the 1st, M+2 and M+3 data aggregation takes place | at 00:00 (available approx. at 07:00) | at 14:00 (available approx. at 18:00) |


Data:

- aggregated data from balance settlement metering points of the balance responsible party + open suppliers in its portfolio, which are included in the balance settlement area of the balance responsible party (so-called IN metering points);
- sales deducted from the balance settlement portfolio of the balance responsible party of the grid operator, gas agreements in the portfolios of other balancing responsible parties (so-called OUT border metering points);
- page "BP_OS" – aggregated data from balance settlement metering points of the balance responsible party and open suppliers in its portfolio, which are included in the balance settlement area of the balance responsible party (so-called IN balance settlement metering points);
- page "BP_GO" = sales deducted from the balance settlement portfolio of the balance responsible party of the grid operator, gas sales agreements in the portfolios of other balancing responsible parties (so-called OUT balance settlement metering points).

Column descriptions:

- **Page "BH_GO"**
  - Grid operator EIC – EIC code of the grid operator (gridOperatorEIC)
  - Grid operator – name of the grid operator (gridOperatorName)
  - Grid operator balance responsible party EIC (gridOperatorBalanceProviderEIC)
  - Grid operator balance responsible party name – the name of the grid operator’s balance responsible party (gridOperatorBalanceProviderName)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - Amounts entering the grid outside the portfolio, kWh – production that must be deducted from the balance portfolio – production at a metering point of a market participant not in the balance responsible party’s portfolio, Pin. All market participants’ metering points, including the grid operator’s border metering points where the balance responsible party of the market participant’s metering point differs from the balance responsible party of the grid operator (inQuantity)
  - Amounts leaving the grid outside the portfolio, kWh – consumption that must be deducted from the balance portfolio – consumption at a metering point of a market participant not in the balance responsible party’s portfolio, Pout. All market participants’ metering points, including the grid operator’s border metering points where the balance responsible party of the market participant’s metering point differs from the balance responsible party of the grid operator (outQuantity)
  - Amounts entering the isolated grid outside the portfolio, kWh. All market participants’ isolated metering points where the balance responsible party of the market participant’s metering point differs from the balance responsible party of the grid operator (inQuantityIsolated)
  - Amounts leaving the isolated grid outside the portfolio, kWh. All market participants’ isolated metering points where the balance responsible party of the market participant’s metering point differs from the balance responsible party of the grid operator (outQuantityIsolated)
  - Number of metering points, pcs (meteringPointsTotal)
- **Page "BH_OS"**
  - Balance responsible party EIC (openSupplierBalanceProviderEIC)
  - Balance responsible party – name of the balance responsible party (openSupplierBalanceProviderName)
  - Open Supplier EIC (openSupplierEIC)
  - Open supplier – name of the open supplier (openSupplierName)
  - Grid operator EIC – EIC code of the grid operator (gridOperatorEIC)
  - Grid operator – name of the grid operator (gridOperatorName)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - Amounts entering the grid, kWh – production at a metering point of a market participant in the balance responsible party’s portfolio, Pin. All market participants’ metering points, including the grid operator’s border metering points that are in the balance portfolio and whose grid operator is not in the balance portfolio of the same balance responsible party (inQuantity)
  - Amounts leaving the grid, kWh – consumption at a metering point of a market participant in the balance responsible party’s portfolio, Pout. All market participants’ metering points, including the grid operator’s border metering points that are in the balance portfolio and whose grid operator is not in the balance portfolio of the same balance responsible party (outQuantity)
  - Amounts entering the isolated grid, kWh. All market participants’ isolated metering points that are in the balance portfolio and whose grid operator is not in the balance portfolio of the same balance responsible party (inQuantityIsolated)
  - Amounts leaving the isolated grid, kWh. All market participants’ isolated metering points that are in the balance portfolio and whose grid operator is not in the balance portfolio of the same balance responsible party (outQuantityIsolated)
  - Number of metering points (meteringPointsTotal)

### Balance responsible party report No. 2
### (only electricity market)

Recipients:

- **Balance responsible parties**

Frequency:

| | Electricity |
|---|---|
| Once per day, D+1 data aggregation takes place | at 10:00 (available approx. at 14:00) |
| Once per month on the 8th, M+1 data aggregation takes place | at 00:00 (available approx. at 10:00) |
| Once per month on the 1st, M+2 and M+3 data aggregation takes place | at 00:00 (available approx. at 07:00) |


Data:

- Page "BH_OS_GO" – the amounts of the open suppliers of the balance responsible party and those in its portfolio, by grid operators’ grid areas.
- Page "BH_GO_OS_GO" – the amounts of the general service customers of the grid operators in the balance responsible party’s portfolio and the amount of grid losses.

Column descriptions:

- Aggregated metering data of the open suppliers in the balance portfolio, indicated separately:
  - amounts aggregated in the portfolio by open suppliers (including the balance responsible party) and grid area for all metering points for which there is an open electricity supply agreement – not including border metering points where the customer of the grid agreement is another grid operator;
  - portfolio of a grid operator in the balance portfolio, shown separately for general service and grid losses.
- **PAGE "BH_OS_GO"**
  - Open supplier EIC – open suppliers in the balance responsible party’s portfolio per metering point (openSupplierEIC)
  - Open supplier name – same as above, but its name (openSupplierName)
  - Grid operator EIC – EIC of the grid operator at the metering point (gridOperatorEIC)
  - Grid operator – name of the grid operator at the metering point (gridOperatorName)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - Amounts entering a grid in the balance responsible party’s portfolio from the end customer, kWh – Pin amount entering the grid (all metering points that have a valid grid agreement and are not a GO-GO border point) (inQuantity)
  - Amounts leaving a grid in the balance responsible party’s portfolio to the end customer, kWh – Pout amount leaving the grid of the grid operator (all metering points that have a valid grid agreement and are not a GO-GO border point) (outQuantity)
  - Amounts entering an isolated grid in the balance responsible party’s portfolio from the end customer, kWh – Pin amount entering the grid (all isolated metering points that have a valid grid agreement and are not a GO-GO border point) (inQuantityIsolated)
  - Amounts leaving an isolated grid in the balance responsible party’s portfolio to the end customer, kWh – Pout amount leaving the grid of the grid operator (all isolated metering points that have a valid grid agreement and are not a GO-GO border point) (outQuantity)
  - Number of metering points, pcs (meteringPointsTotal)
- **PAGE "BH_GO_OS_GO"**
  - Amounts entering a grid of a GO in the balance responsible party’s portfolio from a general service end customer with a grid agreement, kWh – Pin amount entering the grid (production) (inQtyPortfolioLastResortSupply)
  - Amounts leaving a grid of a GO in the balance responsible party’s portfolio to a general service end customer with a grid agreement, kWh – Pout amount leaving the grid of the grid operator (consumption) (outQtyPortfolioLastResortSupply)
  - Grid loss of a GO in the balance responsible party’s portfolio (qtyLosses)
  - Number of metering points, pcs (meteringPointsTotal)

### BHT report

> [!NOTE]
> BHT report is primarly meant for Elering however balance providers can access their BHT reports.

Recipients:

- **Balance responsible parties**
- **Elering AS**

Frequency:

| | Electricity | Gas |
|---|---|---|
| Once per day, D+1 data aggregation takes place | not generated | at 14:00 (available approx. at 18:00) |
| Once per month on the 8th, M+1 data aggregation takes place | at 00:00 (available approx. at 10:00) | at 14:00 (available approx. at 18:00) |
| Once per month on the 1st, M+2 and M+3 data aggregation takes place | at 00:00 (available approx. at 07:00) | at 14:00 (available approx. at 18:00) |


Column descriptions:

BHT report values are calculated based on Balance Provider report.

- **PAGE "BMS_RAPORT"**
  - Balance responsible party EIC (balanceProviderEic)
  - Balance period – time (date + time) marking the beginning of the balance period (DateTime)
  - Production - Production in metering points that belong to the balance provider portfolio but grid operator belong to another portfolio. From these values metering points where grid operator belongs to the balance provider portfolio but open supplier does not are subtracted. Isolated metering points are counted as well. (Portfolio Production)
  - Consumption - Consumption in metering points that belong to the balance provider portfolio but grid operator belong to another portfolio. From these values metering points where grid operator belongs to the balance provider portfolio but open supplier does not are subtracted. Isolated metering points are counted as well. (Portfolio Consumption)
  - Saldo - is being calculated based on previous columns: Portfolio Production - Portfolio Consumption (Portfolio Saldo)
  
#### Report of Non-Remote Read Metering Points 
### (Gas Market Only)

Recipients:
- **Balance Responsible Parties**

Frequency:

| | Gas |
|---|---|
| Once per month on the 28th. The report is compiled for the following month | at 01:30 (available approx. at 10:00) |



**Sheet "NON_REMOTE_READ_MP MM.YYYY"**
- Metering Point EIC – EIC code of the non-remote read metering point (meteringPointEIC)
- Period – column header is dynamic MM.YYYY (e.g. 07.2026) indicating the month and year the report applies to (MM.YYYY)
- Customer EIC – EIC code of the customer (grid agreement customer) of the non-remote read metering point (customerEIC)
- Connection State – connection status of the metering point (whether connected or not) (connectionState)

#### Forecast Report of Non-Remote Read Metering Points
### (Gas Market Only)

Recipients:
- **Balance Responsible Parties**

Frequency:

| | Gas |
|---|---|
| Once per month on the 28th. The report is compiled for the following month | at 02:00 (available approx. at 10:00) |


**Sheet "FORECAST_DATA MM.YYYY"**
- Grid Operator EIC – EIC code of the grid operator of the non-remote read metering point (gridOperatorEic)
- Grid Operator Name – name of the grid operator of the non-remote read metering point (gridOperatorName)
- Balance Period – time indicating the start of the balance period (date + time) (DateTime)
- Quantity Entered into Grid, kWh – quantity entered into the grid from the upstream grid operator (inQuantityKwh)
- Quantity Exited from Grid, kWh – quantity exited from the grid to the upstream grid operator’s grid (outQuantityKwh)
- Number of Metering Points (pcs) (meteringPointsTotal)

#### Grid Operator Customer Report 
### (Gas Market Only)

Recipients:
- **Grid Operators**

Frequency:

| | Gas |
|---|---|
| Once per month on the 8th, preparation of the M+1 report | at 14:00 (available approx. at 18:00) |
| Once per month on the 1st, preparation of the M+1, M+2 and M+3 reports | at 14:00 (available approx. at 18:00) |


**Sheet "GO_MP"**
- Metering Point EIC – EIC code of the metering point (meteringPointEIC)
- Gas Supplier EIC – EIC of the market participant supplying gas at the metering point (openSupplierEIC)
- Customer EIC – EIC code of the metering point customer (customerEIC)
- Customer Name – name of the metering point customer (customerName)
- Cancelled – if thd agreement was terminated during the period, value is 1, otherwise 0 (Canceled)
- Period Start – start of the current month at 07:00 or, in case of a negrid agreement, thd agreement start date (periodStarts)
- Period End – report generation date or, if thgrid agreement ended during the current month, thd agreement end date (periodEnds)
- Hours – validity of thd agreement in hours during the reporting month (hours)
- Number of Transmissions of Entered Quantities – total count of transmitted metering data (including zero quantities) (inNumber)
- Number of Transmissions of Exited Quantities – total count of transmitted metering data (including zero quantities) (outNumber)
- Production m3 – cubic meters injected into the grid (inM3)
- Consumption m3 – cubic meters withdrawn from the grid (outM3)
- Production kWh – kWh injected into the grid (inKwh)
- Consumption kWh – kWh withdrawn from the grid (outKwh)
