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
| Võrguteenuse arve         | `POST` | /api/v1/network-bill                     | Võrguteenuse arve lisamine                                       | 2024.01.18 |
| Võrguteenuse arve         | `POST` | /api/v1/network-bill/search              | Võrguteenuse arve otsing                                         | 2024.01.18 |
| Mõõteandmed               | `POST` | /api/v1/meter-data/export                | Mõõteandmete eksportimine                                        | 2024.01.18 |
| Ühisarve võrguarve        | `POST` | /api/v1/joint-invoice                    | Ühisarve võrguarve lisamine                                      | 2024.01.18 |
| Ühisarve võrguarve        | `POST` | /api/v1/joint-invoice/search             | Ühisarve võrguarve otsing                                        | 2024.01.18 |
| Ühisarve võrguarve        | `POST` | /api/v1/joint-invoice/download           | Ühisarve võrguarve alla laadimine                                | 2024.01.18 |
| Ligipääsuõigus            | `POST` | /api/v1/customer-authorization/search    | Kliendiportaalis antud ligipääsuõiguste otsing                   | 2024.01.18 |
| Sisse- ja väljalülitamine | `POST` | /api/v1/connection-state/search          | Sisse- või väljalülitamise taotluste otsing                      | 2024.01.31 |
| Sisse- ja väljalülitamine | `POST` | /api/v1/connection-state/message         | Sisse- või väljalülitamise taotlusele jätkusõnumite edastamine   | 2024.01.31 |
| Sisse- ja väljalülitamine | `POST` | /api/v1/connection-state/message-history | Sisse- või väljalülitamise taotluste jätkusõnumite ajaloo otsing | 2024.01.31 |
| Sisse- ja väljalülitamine | `POST` | /api/v1/connection-state/initiate        | Sisse- või väljalülitamise taotluse lisamine                     | 2024.01.31 |
| Mõõteandmed               | `POST` | /api/v1/meter-data/status                | Mõõteandmete sõnumi töötlemise staatuse päring                   | 2024.01.31 |
| Mõõteandmed               | `POST` | /api/v1/meter-data/search                | Mõõteandmete otsing                                              | 2024.01.31 |
| Mõõteandmed               | `POST` | /api/v1/meter-data/import                | Mõõteandmete masslaadimine templiidi abil                        | 2024.01.31 |
| Leping                    | `POST` | /api/v1/agreement/search/meter           | Mõõtepunkti lepingute otsing                                     | 2024.01.31 |
| Ligipääsuõigus            | `POST` | /api/v1/authorization/search             | Kasutaja ligipääsuõiguste otsing                                 | 2024.01.31 |
| Ligipääsuõigus            | `POST` | /api/v1/authorization/delete             | Kasutaja ligipääsuõiguse kustutamine                             | 2024.01.31 |
| Andmete levitamine        | `POST` | /api/v1/data-distribution/search         | Erinevate andmeobjektide muudatuste teavitused                   | 2024.01.31 |
| Klient                    | `PUT`  | /api/v1/customer                         | Kliendi ja tema metaandmete muutmine                             | 2024.02.13 |
| Klient                    | `POST` | /api/v1/customer                         | Kliendi ja tema metaandmete lisamine                             | 2024.02.13 |
| Klient                    | `POST` | /api/v1/customer/search                  | Kliendi ja tema metaandmete otsing                               | 2024.02.13 |
| Tehniline kasutaja        | `POST` | /api/v1/idr/technical-user               | Tehnilise kasutaja loomine                                       | 2024.02.13 |
| Tehniline kasutaja        | `PUT`  | /api/v1/idr/technical-user               | Tehnilise kasutaja kehtetuks muutmine                            | 2024.02.13 |
| Tehniline kasutaja        | `POST` | /api/v1/idr/technical-user/search        | Tehnilise kasutaja otsing                                        | 2024.02.13 |
| Tehniline kasutaja        | `POST` | /api/v1/idr/technical-user/role          | Tehnilise kasutaja rollide otsing                                | 2024.02.13 |
| Mõõtepunkt                | `PUT`  | /api/v1/meter                            | Mõõtepunkti andmete muutmine                                     | 2024.02.13 |
| Mõõtepunkt                | `POST` | /api/v1/meter                            | Mõõtepunkti lisamine                                             | 2024.02.13 |
| Mõõtepunkt                | `POST` | /api/v1/meter/search                     | Mõõtepunkti otsing                                               | 2024.02.13 |
| Mõõtepunkt                | `POST` | /api/v1/meter/search/customer            | Mõõtepunkti otsing kliendi EIC koodi alusel                      | 2024.02.13 |
| Mõõtepunkt                | `POST` | /api/v1/meter/search/border              | Piirimõõtepunkti otsing                                          | 2024.02.13 |
| Mõõtepunkt                | `POST` | /api/v1/meter/import                     | Mõõtepunktide massimport templiidi abil                          | 2024.02.13 |
| Mõõtepunkt                | `POST` | /api/v1/meter/export                     | Mõõtepunktide eksportimine                                       | 2024.02.13 |
| Bilanss                   | `POST` | /api/v1/balance-state/search             | Bilansihalduri piirkonnas toimunud muudatuste otsing             | 2024.03.12 |
| Raport                    | `POST` | /api/v1/report/export/json               | JSON formaadis raporti allalaadimine                             | 2024.03.31 |
| Raport                    | `POST` | /api/v1/report/export/excel              | MS Excel formaadis raporti allalaadimine                         | 2024.03.31 |
| Raport                    | `POST` | /api/v1/report/search                    | Raportite otsing                                                 | 2024.03.31 |
