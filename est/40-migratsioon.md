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

| Vana XML teenus              | Uus REST teenus                                                                       | Link teenuse kirjeldusele                                    |
|------------------------------|---------------------------------------------------------------------------------------|--------------------------------------------------------------|
| RequestCustomerEIC           | `POST` ja `PUT` `/api/{version}/customer`                                             | [Kliendi EIC](04-kliendi-eic.md)                             |
|                              | `POST` `/api/{version}/customer/search`                                               | [Kliendi EIC](04-kliendi-eic.md)                             |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = CUSTOMER_DATA`  | [Andmete levitamine](30-andmete-levitamine.md)               |
| NotifyMeteringPointData      | `POST` ja `PUT` `/api/{version}/meter`                                                | [Mõõtepunktid](05-mootepunktid.md)                           |
|                              | `POST` ja `PUT` `/api/{version}/meter/import`                                         |                                                              |
|                              | `POST` ja `PUT` `/api /{version}/agreement` kus `agreementType = GRID`                | [Lepingud](06-lepingud.md)                                   |
|                              | `POST` `/api /{version}/agreement/delete`                                             |                                                              |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = METERING_POINT` | [Andmete levitamine](30-andmete-levitamine.md)               |
| NotifyGridAgreementChange    | `POST` `/api /{version}/data-distribution/search` kus `resourceType = AGREEMENT`      | [Andmete levitamine](30-andmete-levitamine.md)               |
| RequestMeteringPointsData    | `POST` `/api/{version}/meter/search/customer`                                         | [Mõõtepunktid](05-mootepunktid.md)                           |
|                              | `POST` `/api/{version}/agreement/search/meter`                                        | [Lepingud](06-lepingud.md)                                   |
| NotifySupplyAgreement        | `POST` ja `PUT` `/api /{version}/agreement` kus `agreementType = SUPPLY`              | [Lepingud](06-lepingud.md)                                   |
|                              | `POST` `/api /{version}/agreement/delete`                                             |                                                              |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = AGREEMENT`      | [Andmete levitamine](30-andmete-levitamine.md)               |
| EnergyReport                 | `POST` `/api/{version}/metering-data/natural-gas`                                     | [Metering data](12-metering-data.md)                        |
|                              | `POST` `/api/{version}/metering-data/natural-gas/import`                              |                                                             |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = METERING_DATA`  | [Andmete levitamine](30-andmete-levitamine.md)               |
| EnergyReportResult           | `POST` `/api /{version}/meter-data/status`                                            | [Mõõteandmed](12-mooteandmed.md)                             |
| NetworkBill                  | `POST` ja `PUT` `/api/{version}/network-bill`                                         | [Võrguteenuse arve](13-vorguteenuse-arve.md)                 |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = NETWORK_BILL`   | [Andmete levitamine](30-andmete-levitamine.md)               |
| RequestMeteringDataHistory   | `POST` `/api/{version}/meter-data/search`                                             | [Mõõteandmed](12-mooteandmed.md)                             |
| NotifyCustomerAuthorization  | `POST` `/api/customer-authorization/search`                                           | [Ligipääsuõigus](15-ligipaasuoigus.md)                       |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = PERMISSION`     | [Andmete levitamine](30-andmete-levitamine.md)               |
| NotifyJointInvoiceAgreement  | `POST` ja `PUT` `/api /{version}/agreement` kus `agreementType = JOINT_INVOICE`       | [Lepingud](06-lepingud.md)                                   |
|                              | `POST` `/api /{version}/agreement/delete`                                             |                                                              |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = AGREEMENT`      | [Andmete levitamine](30-andmete-levitamine.md)               |
| NotifyPortfolioAgreement     | `POST` ja `PUT` `/api /{version}/agreement` kus `agreementType = PORTFOLIO_SUPPLIER`  | [Lepingud](06-lepingud.md)                                   |
|                              | `POST` `/api /{version}/agreement/delete`                                             |                                                              |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = AGREEMENT`      | [Andmete levitamine](30-andmete-levitamine.md)               |
| NotifyNamedSupplierAgreement | `POST` ja `PUT` `/api /{version}/agreement` kus `agreementType = NAMED_SUPPLIER`      | [Lepingud](06-lepingud.md)                                   |
|                              | `POST` `/api /{version}/agreement/delete`                                             |                                                              |
|                              | `POST` `/api /{version}/data-distribution/search` kus `resourceType = AGREEMENT`      | [Andmete levitamine](30-andmete-levitamine.md)               |
| RequestAgreementCoordination | *teenus on valmimisel*                                                                | -                                                            |
| ReplyAgreementCoordination   | *teenus on valmimisel*                                                                | -                                                            |
| ConfirmAgreementCoordination | *teenus on valmimisel*                                                                | -                                                            |
| ForwardInvoice               | `POST` ja `PUT` `/api/{version}/joint-invoice`                                        | [Ühisarve](14-yhisarve.md)                                   |
|                              | `POST` `/api/{version}/joint-invoice/search`                                          |                                                              |
|                              | `POST` `/api/{version}/joint-invoice/download`                                        |                                                              |
| RequestConnectionState       | `POST` `/api/{version}/connection-state/initiate`                                     | [Välja- ja sisselülitamine](21-valja-ja-sisse-lylitamine.md) |
|                              | `POST` `/api/{version}/connection-state/search`                                       |                                                              |
| ReplyRequestConnectionState  | `POST` `/api/{version}/connection-state/message`                                      |                                                              |
|                              | `POST` `/api/{version}/connection-state/message-history`                              |                                                              |
|                              | `POST` `/api/{version}/connection-state/search`                                       |                                                              |
| SendMessage                  | *teenus on valmimisel*                                                                | -                                                            |
| BalanceState                 | `POST /api/{version}/balance-settlement-point/change`                                 | [Bilansipiirkond](10-bilansipiirkond.md)                     |
| AggregatedMeteringDataReport | Vaata sektsiooni "Report"                                                             | [Raportid](20-raportid.md)                                   |
| Report                       | `POST /api/{version}/report/search`                                                   | [Raportid](20-raportid.md)                                   |
|                              | `POST /api/{version}/report/export/xlsx`                                              | -                                                            |
|                              | `POST /api/{version}/report/export/json`                                              | -                                                            |

API-de valmimise kohta leiab lisainformatsiooni [siit](50-tegevuskava.md)

## Suurimad erinevused

Võrreldes varasema Andmelaoga on uues Estfeed Datahubis järgnevad suuremad muudatused.

- Kliendi lisamine ja muutmine on lepingust sõltumatu. Kui kliendi nime on viimase kahe aasta jooksul GAVP-s muudetud jääb kehtima Estfeed Datahubis olev nimi. Paraku ei ole meil võimalik kindlaks teha kumb nimi on õige.
- Muutunud on mõõtepunkti tehnilised andmed, täpsemalt loe nende kohta [siit](05-mõõtepunktid.md).
- Mõõteandmete edastamisel pole vaja enam arvutada ega edastada "pos" väärtust. Selle asemel on kasutusel perioodi alguse plus resolutsiooni kombinatsioon.
- Lisandunud on eraldi piirimõõtepunkti (BORDER) ja piirimõõtepunkti lepingu (BORDER_GRID) definitsioonid
- Lisandunud on võimalus edastada kliendi metaandmetena arvelduseks vajalikke andmeid.
- Andmeladu genereerib GENERAL_SERVICE lepinguid automaatselt ja levitab seda infot võrguettevõtjale ja nimetatud müüjale.
- API kasutamiseks vajalike tehniliste kasutajakontode toe loomine.
- Mõõteandmete vastuvõtmise ja töötlemise protsess on muutunud asünkroonseks. Töötlemise tulemuse saab pärida teenusest `/meter-data/status`
- Raporteid on võimalik alla laadida JSON formaadis, kuid mitte XML formaadis.
- Ühel turuosalisel saab olla ka mitu EIC koodide vahemikku.
- _Billing sequence_ asemel on nüüd kasutusel _reading time_. GO saab mõõteandmete edastamisel defineerida _reading time_ väärtuse ja OS/NS saavad selle väärtuse järgi mõõteandmeid otsida
- Mõõteandmeid saab veebiliidesest korraga alla laadida vaid ühe mõõtepunkti kaupa.