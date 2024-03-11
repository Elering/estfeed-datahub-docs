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

| Vana XML teenus              | Uus REST teenus                                                                               | Link teenuse kirjeldusele                                    |
|------------------------------|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| RequestCustomerEIC           | `POST` `/api/{version}/customer`                                                              | [Kliendi EIC](04-kliendi-eic.md)                             |
|                              | `POST` `/api/{version}/customer/search`                                                       | [Kliendi EIC](04-kliendi-eic.md)                             |
| NotifyMeteringPointData      | `POST` ja `PUT` `/api/{version}/meter`                                                        | [Mõõtepunktid](05-mootepunktid.md)                           |
|                              | `POST` ja `PUT` `/api /{version}/agreement` kus `agreementType = GRID`                        | [Mõõtepunktid](05-mootepunktid.md)                           |
| NotifyGridAgreementChange    | `POST` `/api /{version}/data-distribution/search` kus `resourceType = AGREEMENT`              | [Andmete levitamine](30-andmete-levitamine.md)               |
| RequestMeteringPointsData    | `POST` `/api/{version}/meter/search/customer`                                                 | [Kliendi EIC](04-kliendi-eic.md)                             |
| NotifySupplyAgreement        | `POST` ja `PUT` `/api /{version}/agreement` kus `agreementType = SUPPLY`                      | [Lepingud](06-lepingud.md)                                   |
| EnergyReport                 | `POST` `/api/{version}/meter-data`                                                            | [Mõõteandmed](12-mooteandmed.md)                             |
| EnergyReportResult           | `POST` `/api /{version}/meter-data/status`                                                    | [Mõõteandmed](12-mooteandmed.md)                             |
| NetworkBill                  | `POST` `/api/{version}/network-bill`                                                          | [Võrguteenuse arve](13-vorguteenuse-arve.md)                 |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = NETWORK_BILL`           | [Andmete levitamine](30-andmete-levitamine.md)               |
| RequestMeteringDataHistory   | `POST` `/api/{version}/meter-data/search`                                                     | [Mõõteandmed](12-mooteandmed.md)                             |
| NotifyCustomerAuthorization  | `POST` `/api/customer-authorization/search`                                                   | [Mõõteandmed](12-mooteandmed.md)                             |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = CUSTOMER_AUTHORIZATION` | [Andmete levitamine](30-andmete-levitamine.md)               |
| CustomerMetadata             | *teenus on valmimisel*                                                                        | -                                                            |
| NotifyJointInvoiceAgreement  | `POST` ja `PUT` `/api /{version}/agreement` kus `agreementType = JOINT_INVOICE`               | [Lepingud](06-lepingud.md)                                   |
| NotifyPortfolioAgreement     | `POST` ja `PUT` `/api /{version}/agreement` kus `agreementType = PORTFOLIO_SUPPLIER`          | [Lepingud](06-lepingud.md)                                   |
| NotifyNamedSupplierAgreement | `POST` ja `PUT` `/api /{version}/agreement` kus `agreementType = NAMED_SUPPLIER`              | [Lepingud](06-lepingud.md)                                   |
| RequestAgreementCoordination | *teenus on valmimisel*                                                                        | -                                                            |
| ReplyAgreementCoordination   | *teenus on valmimisel*                                                                        | -                                                            |
| ConfirmAgreementCoordination | *teenus on valmimisel*                                                                        | -                                                            |
| ForwardInvoice               | `POST` `/api/{version}/joint-invoice`                                                         | [Ühisarve](14-yhisarve.md)                                   |
|                              | `POST` `/api/{version}/joint-invoice/download`                                                | [Ühisarve](14-yhisarve.md)                                   |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = JOINT_INVOICE`          | [Andmete levitamine](30-andmete-levitamine.md)               |
| RequestConnectionState       | `POST` `/api/{version}/connection-state/initiate`                                             | [Sisse ja välja lülitamine](21-valja-ja-sisse-lylitamine.md) |
|                              | `POST` `/api/{version}/connection-state/message`                                              | [Sisse ja välja lülitamine](21-valja-ja-sisse-lylitamine.md) |
|                              | `POST` `/api/{version}/connection-state/message-history`                                      | [Sisse ja välja lülitamine](21-valja-ja-sisse-lylitamine.md) |
|                              | `POST` `/api/{version}/connection-state/search`                                               | [Sisse ja välja lülitamine](21-valja-ja-sisse-lylitamine.md) |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = CONNECTION_STATE`       | [Andmete levitamine](30-andmete-levitamine.md)               |
| ReplyRequestConnectionState  | `POST` `/api/{version}/connection-state/message`                                              | [Sisse ja välja lülitamine](21-valja-ja-sisse-lylitamine.md) |
|                              | `POST` `/api/{version}/connection-state/message-history`                                      | [Sisse ja välja lülitamine](21-valja-ja-sisse-lylitamine.md) |
|                              | `POST` `/api/{version}/connection-state/search`                                               | [Sisse ja välja lülitamine](21-valja-ja-sisse-lylitamine.md) |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = CONNECTION_STATE`       | [Andmete levitamine](30-andmete-levitamine.md)               |
| SendMessage                  | *teenus on valmimisel*                                                                        | -                                                            |
| BalanceState                 | *teenus on valmimisel*                                                                        | -                                                            |
| AggregatedMeteringDataReport | *teenus on valmimisel*                                                                        | -                                                            |
| Report                       | *teenus on valmimisel*                                                                        | -                                                            |

API-de valmimise kohta leiab lisainformatsiooni [siit](50-tegevuskava.md)

## Lisandunud funktsionaalsus

Võrreldes varasema Andmelaoga on uues Andmelaos juba arendatud või arendamisel järgmised uued funktsionaalsused:

- Lisandunud on uus lepingu tüüp - [Agregeerimisleping](06.6-agregeerimisleping.md).
- Kliendi lisamine ja muutmine on lepingust sõltumatu.
- Niinimetatud ülem-mõõtepunkti kontseptsioon.
- Asukoha andmetesse on lisandunud ADS-i ADR_ID ja kommentaar.
- Mõõtmise resolutsioonide hulka on lisandunud ka 15min võimekus.
- Uued klienditüübi valikud: ENERGY_STORAGE_UNIT, CHARGING_POINT_OPERATOR.
- Tootmise olemasolu ja tüüp: SOLAR, WIND, HYDRO, BIOGAS, BIOMASS, NATURAL_GAS, OIL_SHALE, OTHER_RENEWABLE, OTHER_NON_RENEWABLE.
- Arvulised väärtused: salvestusvõimsus (storageCapacity), salvestusenergia (storageEnergy), tootmisvõimsus (productionCapacity) ja ülekandevõimsus (transmissionCapacity).
- Ülekandevõrgu alajaam
- Korteriühistu tunnus
- Laadimispunkti tunnus
- Mõõteandmete resolutsioon on energiatüübi kaupa fikseeritud rakenduse konfiguratsioonis ning mõõteandmete sõnumis resolutsiooni enam juhtida ei saa.
- Mõõteandmete edastamisel pole vaja enam arvutada ega edastada "pos" väärtust. Selle asemel on kasutusel perioodi alguse plus resolutsiooni kombinatsioon.
- Lisandunud on eraldi piirimõõtepunkti (BORDER) ja piirimõõtepunkti lepingu (BORDER_GRID) definitsioonid
- Lisandunud on võimalus edastada kliendi metaandmetena ühisarve võrguarve jaoks vajalikke arvelduse andmeid.
- Andmeladu genereerib GENERAL_SERVICE lepinguid automaatselt ja levitab seda infot võrguettevõtjale ja nimetatud müüjale.
- API kasutamiseks vajalike tehniliste kasutajakontode toe loomine.
- Mõõteandmete vastuvõtmise ja töötlemise protsess on muutunud asünkroonseks. Töötlemise tulemuse saab pärida teenusest `/meter-data/status`
