# Migratsioon vanast süsteemist uude

## Sisukord

- [Migratsioon vanast süsteemist uude](#migratsioon-vanast-süsteemist-uude)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Andmevahetusliidese teenuste võrdlus](#andmevahetusliidese-teenuste-võrdlus)
  - [Lisandunud funktsionaalsus](#lisandunud-funktsionaalsus)

## Sissejuhatus

Käesolev dokument on loodud ajutiseks abivahendiks arendajatele, et aidata neil toime tulla Andmelao uuenduste ja versioonivahetusega. Pärast uuele Andmelao versioonile üleminekut kaotab käesolev dokument oma aktuaalsuse ja eemaldatakse siit repositooriumist.

## Andmevahetusliidese teenuste võrdlus

Uus Andmeladu kasutab kaasaegsemat REST andmevahetusliidest. Sellest tulenevalt muutuvad kõik andmevahetusliidese teenused. Allolev tabel kõrvutab vanad ja uued teenused.

| Vana XML teenus              | Kas kuulub MVP skoopi | Uus REST teenus                         |
|------------------------------|-----------------------|-----------------------------------------|
| RequestCustomerEIC           | MVP                   | `/api/{version}/customer`               |
| NotifyMeteringPointData      | MVP                   | `/api/{version}/meter`                  |
| NotifyGridAgreementChange    | MVP                   | `/api /{version}/agreement`             |
| RequestMeteringPointsData    | MVP                   | `/api/{version}/meter/search/customer`  |
| NotifySupplyAgreement        | MVP                   | `/api /{version}/agreement`             |
| EnergyReport                 | MVP                   | `/api/{version}/meter-data`             |
| EnergyReportResult           | MVP                   | `/api/{version}/meter-data/status`      |
| NetworkBill                  | MVP                   | `/api/{version}/network-bill`           |
| RequestMeteringDataHistory   | MVP                   | `/api/{version}/meter-data/search`      |
| NotifyCustomerAuthorization  | MVP                   | `/api/customer-authorization`           |
| CustomerMetadata             | MVP                   | *Teenus on väljatöötamisel*             |
| NotifyJointInvoiceAgreement  | MVP                   | `/api/{version}/agreement`              |
| NotifyPortfolioAgreement     | MVP                   | `/api /{version}/agreement`             |
| NotifyNamedSupplierAgreement | MVP                   | `/api /{version}/agreement`             |
| RequestAgreementCoordination | -                     | `/api/{version}/agreement-coordination` |
| ReplyAgreementCoordination   | -                     | `/api/{version}/agreement-coordination` |
| ConfirmAgreementCoordination | -                     | `/api/{version}/agreement-coordination` |
| ForwardInvoice               | MVP                   | `/api/{version}/forward-invoice`        |
| RequestConnectionState       | -                     | `/api/{version}/connection-state`       |
| ReplyRequestConnectionState  | -                     | `/api/{version}/connection-state`       |
| SendMessage                  | -                     | `/api/{version}/direct-message`         |
| BalanceState                 | MVP                   | `/api/{version}/balance-state`          |
| AggregatedMeteringDataReport | MVP                   | *Teenus on väljatöötamisel*             |
| Report                       | -                     | *Teenus on väljatöötamisel*             |

## Lisandunud funktsionaalsus

Võrrelded varasema Andmelaoga on uues Andmelaos juba arendatud või arendamisel järgmised uued funktsionaalsused:

- Lisandunud on uus lepingu tüüp - [Agregeerimisleping](05.6-agregeerimisleping.md).
- Niinimetatud ülem-mõõtepunkti kontseptsioon.
- Mõõteandmete asünkroonne töötlus.
- Asukoha andmetesse on lisandunud ADS-i ADR_ID ja kommentaar.
- Mõõtmise resolutsioonide hulka on lisandunud ka 15min võimekus.
- Uued klienditüübi valikud: ENERGY_STORAGE_UNIT, CHARGING_POINT_OPERATOR.
- Tootmise olemasolu ja tüüp: SOLAR, WIND, HYDRO, BIOGAS, BIOMASS, NATURAL_GAS, OIL_SHALE, OTHER_RENEWABLE, OTHER_NON_RENEWABLE.
- Arvulised väärtused: salvestusvõimsus (storageCapacity), salvestusenergia (storageEnergy), tootmisvõimsus (productionCapacity) ja ülekandevõimsus (transmissionCapacity).
- Ülekandevõrgu alajaam
- Korteriühistu tunnus
- Laadimispunkti tunnus
