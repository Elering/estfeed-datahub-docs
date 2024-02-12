# Tegevuskava

## API arendused

| Teema                     | Tüüp   | Otspunkt                                 | Kirjeldus                                                        | Valmimine  |
|---------------------------|--------|------------------------------------------|------------------------------------------------------------------|------------|
| Leping                    | `POST` | /api/v1/agreement                        | Lepingu loomine                                                  | Valmis     |
| Leping                    | `PUT`  | /api/v1/agreement                        | Lepingu uuendamine                                               | Valmis     |
| Leping                    | `POST` | /api/v1/agreement/search                 | Lepingute otsing                                                 | Valmis     |
| Leping                    | `POST` | /api/v1/agreement/export                 | Lepingute eksport                                                | Valmis     |
| Leping                    | `POST` | /api/v1/agreement/delete                 | Lepingu kustutamine                                              | Valmis     |
| Templiit                  | `POST` | /api/v1/template/meter                   | Mõõtepunkti masslisamise templiidi alla laadimine                | Valmis     |
| Mõõteandmed               | `POST` | /api/v1/meter-data                       | Mõõteandmete lisamine                                            | Valmis     |
| Ligipääsuõigus            | `POST` | /api/v1/authorization                    | Ligipääsuõiguse lisamine kasutajale                              | Valmis     |
| Kasutaja õigused          | `POST` | /api/v1/user/rights/search               | Kasutaja õiguste päring                                          | Valmis     |
| Kasutaja rolli tüüp       | `GET`  | /api/v1/user-role-type                   | Kasutaja rolli tüüpide päring                                    | Valmis     |
| Kasutaja tururoll         | `GET`  | /api/v1/user/market-roles                | Kasutaja tururollide päring                                      | Valmis     |
| Võrguteenuse arve         | `POST` | /api/v1/network-bill                     | Võrguteenuse arve lisamine                                       | Valmis     |
| Võrguteenuse arve         | `POST` | /api/v1/network-bill/search              | Võrguteenuse arve otsing                                         | Valmis     |
| Mõõteandmed               | `POST` | /api/v1/meter-data/export                | Mõõteandmete eksportimine                                        | Valmis     |
| Ühisarve võrguarve        | `POST` | /api/v1/joint-invoice                    | Ühisarve võrguarve lisamine                                      | Valmis     |
| Ühisarve võrguarve        | `POST` | /api/v1/joint-invoice/search             | Ühisarve võrguarve otsing                                        | Valmis     |
| Ühisarve võrguarve        | `POST` | /api/v1/joint-invoice/download           | Ühisarve võrguarve alla laadimine                                | Valmis     |
| Ligipääsuõigus            | `POST` | /api/v1/customer-authorization/search    | Kliendiportaalis antud ligipääsuõiguste otsing                   | Valmis     |
| Sisse- ja väljalülitamine | `POST` | /api/v1/connection-state/search          | Sisse- või väljalülitamise taotluste otsing                      | Valmis     |
| Sisse- ja väljalülitamine | `POST` | /api/v1/connection-state/message         | Sisse- või väljalülitamise taotlusele jätkusõnumite edastamine   | Valmis     |
| Sisse- ja väljalülitamine | `POST` | /api/v1/connection-state/message-history | Sisse- või väljalülitamise taotluste jätkusõnumite ajaloo otsing | Valmis     |
| Sisse- ja väljalülitamine | `POST` | /api/v1/connection-state/initiate        | Sisse- või väljalülitamise taotluse lisamine                     | Valmis     |
| Mõõteandmed               | `POST` | /api/v1/meter-data/status                | Mõõteandmete sõnumi töötlemise staatuse päring                   | Valmis     |
| Mõõteandmed               | `POST` | /api/v1/meter-data/search                | Mõõteandmete otsing                                              | Valmis     |
| Mõõteandmed               | `POST` | /api/v1/meter-data/import                | Mõõteandmete masslaadimine templiidi abil                        | Valmis     |
| Leping                    | `POST` | /api/v1/agreement/search/meter           | Mõõtepunkti lepingute otsing                                     | Valmis     |
| Ligipääsuõigus            | `POST` | /api/v1/authorization/search             | Kasutaja ligipääsuõiguste otsing                                 | Valmis     |
| Ligipääsuõigus            | `POST` | /api/v1/authorization/delete             | Kasutaja ligipääsuõiguse kustutamine                             | Valmis     |
| Andmete levitamine        | `POST` | /api/v1/data-distribution/search         | Erinevate andmeobjektide muudatuste teavitused                   | Valmis     |
| Klient                    | `PUT`  | /api/v1/customer                         | Kliendi ja tema metaandmete muutmine                             | 2024.02.19 |
| Klient                    | `POST` | /api/v1/customer                         | Kliendi ja tema metaandmete lisamine                             | 2024.02.19 |
| Klient                    | `POST` | /api/v1/customer/search                  | Kliendi ja tema metaandmete otsing                               | 2024.02.19 |
| Tehniline kasutaja        | `POST` | /api/v1/idr/technical-user               | Tehnilise kasutaja loomine                                       | 2024.02.19 |
| Tehniline kasutaja        | `PUT`  | /api/v1/idr/technical-user               | Tehnilise kasutaja kehtetuks muutmine                            | 2024.02.19 |
| Tehniline kasutaja        | `POST` | /api/v1/idr/technical-user/search        | Tehnilise kasutaja otsing                                        | 2024.02.19 |
| Tehniline kasutaja        | `POST` | /api/v1/idr/technical-user/role          | Tehnilise kasutaja rollide otsing                                | 2024.02.19 |
| Mõõtepunkt                | `PUT`  | /api/v1/meter                            | Mõõtepunkti andmete muutmine                                     | 2024.02.19 |
| Mõõtepunkt                | `POST` | /api/v1/meter                            | Mõõtepunkti lisamine                                             | 2024.02.19 |
| Mõõtepunkt                | `POST` | /api/v1/meter/search                     | Mõõtepunkti otsing                                               | 2024.02.19 |
| Mõõtepunkt                | `POST` | /api/v1/meter/search/customer            | Mõõtepunkti otsing kliendi EIC koodi alusel                      | 2024.02.19 |
| Mõõtepunkt                | `POST` | /api/v1/meter/search/border              | Piirimõõtepunkti otsing                                          | 2024.02.19 |
| Mõõtepunkt                | `POST` | /api/v1/meter/import                     | Mõõtepunktide massimport templiidi abil                          | 2024.02.19 |
| Mõõtepunkt                | `POST` | /api/v1/meter/export                     | Mõõtepunktide eksportimine                                       | 2024.02.19 |
| Bilanss                   | `POST` | /api/v1/balance-state/search             | Bilansihalduri piirkonnas toimunud muudatuste otsing             | 2024.03.01 |
| EIC                       | `POST` | /api/v1/eic/range                        | EIC vahemikust vabade EIC koodide otsing                         | 2024.03.01 |
| Raport                    | `POST` | /api/v1/report/export/json               | JSON formaadis raporti allalaadimine                             | 2024.03.31 |
| Raport                    | `POST` | /api/v1/report/export/excel              | MS Excel formaadis raporti allalaadimine                         | 2024.03.31 |
| Raport                    | `POST` | /api/v1/report/search                    | Raportite otsing                                                 | 2024.03.31 |
| Ühisarve võrguarve        | `PUT`  | /api/v1/joint-invoice                    | Ühisarve võrguarve muutmine                                      | 2024.05.15 |
