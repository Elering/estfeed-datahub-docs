# REST API versioonihaldus ja hoolduspoliitika

- [Sissejuhatus](#sissejuhatus)
- [Versioneerimise põhimõtted](#versioneerimise-põhimõtted)
- [API elutsükli etapid](#api-elutsükli-etapid)
- [Üleminekuperioodid](#üleminekuperioodid)
- [Migreerimisjuhised](#migreerimisjuhised)
- [Teavitused](#teavitused)
- [API versioonid ja ülemineku tähtajad](#api-versioonid-ja-ülemineku-tähtajad)

## Sissejuhatus

See dokument kirjeldab Estfeed Datahub REST API-de versiooni strateegiat, sealhulgas elutsükli etappe, aegumise kuupäevasid ja ülemineku reegleid.

## Versioneerimise põhimõtted

- REST API-d versioneeritakse kasutades **põhiversiooni numbrit** URL-is:
  - Näide:  
    - `https://datahub.elering.ee/api/v1/...`  
    - `https://datahub.elering.ee/api/v2/...`

- **Väikesed muudatused** (tagasiühilduvad) võivad olla tehtud ilma uut versiooni loomata.  
- **Tagasiühildumatud muudatused** toovad alati kaasa uue põhiversiooni.

## API elutsükli etapid

Iga API versioon läbib järgmised etapid:

1. **Aktiivne** – Täielikult toetatud.  
2. **Aegunud** – Kasutamine on veel võimalik, kuid sulgemine on planeeritud.  
3. **Suletud** – Kasutamine ei ole enam võimalik.

## Üleminekuperioodid

- **Vähemalt 6-kuuline üleminekuperiood** on garanteeritud pärast versiooni *aegunuks* märkimist.  
- Selle perioodi jooksul vana ja uus versioon töötavad paralleelselt.  

## Migreerimisjuhised

- Alusta uusi integratsioone alati **viimase aktiivse versiooniga**.  
- Kui kasutad aegunud versiooni:
  - Planeeri üleminek **enne lõpetamise kuupäeva**.  
  - Järgi avaldatud migreerimisjuhendeid sujuvaks üleminekuks.
- Täpsem info uue versiooni kohta on leitav vastava teema dokumentatsiooni lehelt ja Swaggerist.

## Teavitused

- Kõik versioonide uuendused edastatakse:
  - Meili teel lepingujärgsetele halduritele.
  - Muudatused on dokumenteeritud Githubis
  - API veateadete päistes (kui rakendatav).  
- Tagasiühildumatuid muudatusi **ei** tehta ilma aegumise ajakava etteteatamata.


## API versioonid ja ülemineku tähtajad

| Tüüp   | Otspunkt                                     | Versioon | Staatus  | Kasutusel alates | Aegumise kuupäev | Sulgemise kuupäev | Kommentaar                                                            |
|--------|----------------------------------------------|----------|----------|------------------|------------------|-------------------|-----------------------------------------------------------------------|
| POST   | /api/v1/agreement                            | v1       | aegunud  | 22.11.2024       | 17.09.2025       | 31.03.2026        | Palume võtta kasutusele V2 versioon.                                  |
| POST   | /api/v2/agreements                           | v2       | aktiivne | 17.09.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/agreement/search                     | v1       | aegunud  | 22.11.2024       | 17.09.2025       | 31.03.2026        | Palume võtta kasutusele V2 versioon.                                  |
| GET    | /api/v2/agreements                           | v2       | aktiivne | 17.09.2025       | -                | -                 |                                                                       |
| GET    | /api/v2/agreements/{id}                      | v2       | aktiivne | 17.09.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/agreement/search/meter               | v1       | aegunud  | 22.11.2024       | 17.09.2025       | 31.03.2026        | Palume võtta kasutusele V2 versioon.                                  |
| GET    | /api/v2/metering-points/{eic}/agreements     | v2       | aktiivne | 17.09.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/agreement/export                     | v1       | aegunud  | 22.11.2024       | 17.09.2025       | 31.03.2026        | Palume võtta kasutusele V2 versioon.                                  |
| GET    | /api/v2/agreements/export                    | v2       | aktiivne | 17.09.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/agreement/delete                     | v1       | aegunud  | 22.11.2024       | 17.09.2025       | 31.03.2026        | Palume võtta kasutusele V2 versioon.                                  |
| DELETE | /api/v2/agreements/{id}                      | v2       | aktiivne | 17.09.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/agreement-bulk                       | v1       | aegunud  | 22.11.2024       | 17.09.2025       | 31.03.2026        | Palume võtta kasutusele V2 versioon.                                  |
| POST   | /api/v2/agreements/bulk                      | v2       | aktiivne | 17.09.2025       | -                | -                 |                                                                       |
| PUT    | /api/v1/agreement                            | v1       | aegunud  | 22.11.2024       | 17.09.2025       | 31.03.2026        | Palume võtta kasutusele V2 versioon.                                  |
| PUT    | /api/v2/agreements/{id}                      | v2       | aktiivne | 17.09.2025       | -                | -                 |                                                                       |
| PUT    | /api/v2/agreements/{id}                      | v2       | aktiivne | 17.09.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/template/meter                       | v1       | aegunud  | 22.11.2024       | 10.11.2025       | 30.05.2026        | Palume võtta kasutusele V2 versioon.                                  |
| POST   | /api/v2/template/meter                       | v2       | aktiivne | 10.11.2025       | -                | -                 |                                                                       |
| PUT    | /api/v1/meter                                | v1       | aegunud  | 22.11.2024       | 10.11.2025       | 30.05.2026        | Palume võtta kasutusele V2 versioon.                                  |
| PUT    | /api/v2/meter                                | v2       | aktiivne | 10.11.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/meter                                | v1       | aegunud  | 22.11.2024       | 10.11.2025       | 30.05.2026        | Palume võtta kasutusele V2 versioon.                                  |
| POST   | /api/v2/meter                                | v2       | aktiivne | 10.11.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/meter/search                         | v1       | aegunud  | 22.11.2024       | 10.11.2025       | 30.05.2026        | Palume võtta kasutusele V2 versioon.                                  |
| POST   | /api/v2/meter/search                         | v2       | aktiivne | 10.11.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/meter/search/customer                | v1       | aegunud  | 22.11.2024       | 10.11.2025       | 30.05.2026        | Palume võtta kasutusele V2 versioon.                                  |
| POST   | /api/v2/meter/search/customer                | v2       | aktiivne | 10.11.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/meter/search/border                  | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/meter/import                         | v1       | aegunud  | 22.11.2024       | 10.11.2025       | 30.05.2026        | Palume võtta kasutusele V2 versioon.                                  |
| POST   | /api/v2/meter/import                         | v2       | aktiivne | 10.11.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/meter/export                         | v1       | aegunud  | 22.11.2024       | 10.11.2025       | 30.05.2026        | Palume võtta kasutusele V2 versioon.                                  |
| POST   | /api/v2/meter/export                         | v2       | aktiivne | 10.11.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/meter/eic/amount                     | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/meter/eic/range                      | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/meter-data                           | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/meter-data/status                    | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/meter-data/search                    | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/meter-data/import                    | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/meter-data/export                    | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/template/meter-data                  | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/authorization                        | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/user/rights/search                   | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| GET    | /api/v1/user-role-type                       | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| GET    | /api/v1/user/market-roles                    | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/network-bill                         | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/network-bill/search                  | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/joint-invoice                        | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/joint-invoice/search                 | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/joint-invoice/download               | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/customer-authorization/search        | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/connection-state/search              | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/connection-state/message             | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/connection-state/message-history     | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/connection-state/initiate            | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/authorization/search                 | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| PUT    | /api/v1/authorization/delete                 | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/customer                             | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/customer/search                      | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| PUT    | /api/v1/idr/technical-user                   | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/idr/technical-user/search            | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/idr/technical-user/role              | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/balance-settlement-point/search      | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/report/export/json                   | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/report/export/excel                  | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/report/search                        | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| PUT    | /api/v1/joint-invoice                        | v1       | aktiivne | 22.11.2024       | -                | -                 |                                                                       |
| POST   | /api/v1/data-distribution/search             | v1       | aktiivne | 22.11.2024       | -                | -                 | Alates 31.03.2026 ei saa seda kasutada lepingute sõnumite pärimiseks. |
| GET    | /api/v2/data-distributions/agreement         | v2       | aktiivne | 17.09.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/agreement-coordinations/bulk         | v1       | aktiivne | 13.10.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/agreement-coordinations/{id}/approve | v1       | aktiivne | 13.10.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/agreement-coordinations/{id}/deny    | v1       | aktiivne | 13.10.2025       | -                | -                 |                                                                       |
| POST   | /api/v1/agreement-coordinations/{id}/cancel  | v1       | aktiivne | 13.10.2025       | -                | -                 |                                                                       |
| GET    | /api/v1/agreement-coordinations              | v1       | aktiivne | 13.10.2025       | -                | -                 |                                                                       |
| GET    | /api/v1/agreement-coordinations/{id}         | v1       | aktiivne | 13.10.2025       | -                | -                 |                                                                       |




