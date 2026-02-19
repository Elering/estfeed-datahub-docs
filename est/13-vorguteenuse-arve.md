# Võrguteenuse arve

## Sisukord

- [Võrguteenuse arve](#võrguteenuse-arve)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Võrguteenuse arve edastamine ja pärimine](#võrguteenuse-arve-edastamine-ja-pärimine)
  - [Masinliidese sõnumid](#masinliidese-sõnumid)
    - [Sõnumid](#sõnumid)
    - [Sõnumite reeglid](#sõnumite-reeglid)
  - [Neto mõõdetud mõõteandmete lisandumine võrguarvele](#neto-mõõdetud-mõõteandmete-lisandumine-võrguarvele)

## Sissejuhatus

Võrguteenuse koostamise sõnum abil edastab võrguettevõtja info selle kohta, millisel hetkel ja milliste andmete alusel koostas võrguettevõtja kliendile võrguteenuse arve. Antud sõnumis olev info võimaldab müüjatel esitada klientidele müügiarve samade energiakoguste eest nagu võrguteenuse arve. Andmeladu edastab võrguettevõtja saadetud sõnumi mõõtepunkti avatud tarnijale.

> [!WARNING] 
> Andmeladu ei vastuta sõnumis toodud energiakoguste andmete kvaliteedi eest

## Võrguteenuse arve edastamine ja pärimine

Võrguteenuse arve edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Võrguettevõtja saadab uue või muutunud võrguteenuse arve sõnumi kasutades teenust `network-bill`.
- Andmeladu salvestab võrguteenuse arve andmebaasi
- Avatud tarnija otsib uusi võrguarveid kasutades teenust `search`

Võrguteenuse arve andmete muutmiseks, tuleb saata uus `network-bill` sõnum parandatud andmetega sama perioodi kohta ning väärtustada atribuut `calculationTimestamp` uuema väärtusega.

## Masinliidese sõnumid

### Sõnumid

| Sõnum                                     | Eesmärk                    |
|-------------------------------------------|----------------------------|
| `POST /api/{version}/network-bill`        | Võrguteenuse arve lisamine |
| `POST /api/{version}/network-bill/search` | Võrguteenuse arve otsing   |



### Sõnumite reeglid

- Võrguarve edastamise reeglid:
  - Võrguarvet saab lisada võrguettevõtja (GO) või suletud jaotusvõrgu ettevõtja (CDN)
  - Võrguarve `periodStart` ei tohi olla väiksem, kui võrgulepingu kehtivuse algus
  - Võrguarve `periodEnd` ei tohi olla suurem, kui võrgulepingu kehtivuse lõpp
  - Maksimaalne võrguarve koostamise periood on üks kuu.
  - Perioodi alguse ja lõpu kuu väärtus peab olema võrdne (juhul, kui avatud tarnija ei vahetu kuu vahetusel, siis võrguettevõtja peab edastama 2 eraldi võrguteenuse arvet).
- Juhul kui turuosaline kasutab üldteenust, on võrguteenuste arve edastamine Andmelattu vabatahtlik.
- Võrguarvete otsimise reeglid:
  - võrguettevõtja (GO) ja suletud jaotusvõrgu ettevõtja (CDN) saavad otsida ainult neid võrguarveid, mida nad ise lisasid
  - avatud tarnija saab otsida neid võrguarveid, kus `periodStart` ja `periodEnd` on kaetud sellise avatud tarne lepinguga, kus avatud tarnija on teenusepakkuja.
  - nimetatud tarnija saab otsida neid võrguarveid, kus `periodStart` ja `periodEnd` on kaetud sellise üldteenuse lepinguga, kus nimetatud tarnija on teenusepakkuja.

## Neto mõõdetud mõõteandmete lisandumine võrguarvele

Alates **01.08.2026** on võrguettevõtted kohustatud edastama Estfeed Datahubi kahesuunaliste mõõtepunktide kohta neto mõõdetud mõõteandmed. Andmed tuleb võrguettevõtjal ise arvutada lahutades tootmise kogusest tarbimine. Seetõttu tuleb võrguettevõtjal esitada septembri algusest võrguarve koos neto mõõdetud kogustega. Selleks tuleb võtta kasutusele uus API versioon. Testimine on testkeskkonnas võimalik alates 01.05.2026, testkeskkonna ligipääsu puudumisel tuleb sõlmida turuosalisel testkeskkonna kasutamise leping kirjutades datahub@elering.ee. Esialgu jäävad kaks API versiooni paralleelselt kasutusele, kuid V1 versioonis ei ole neto mõõdetud koguseid.

Uued API sõnumid:

| Sõnum                             | Eesmärk                    |
|-----------------------------------|----------------------------|
| `POST /api/v2/network-bills/bulk` | Võrguteenuse arve lisamine |
| `GET /api/v2/network-bills`       | Võrguteenuse arve otsing   |

> [!WARNING]
> Kuna tegu on alles arenduses oleva funktsionaalsusega ei ole uued API-d veel kirjeldatud Swaggeris.

> [!WARNING]
> Erinevate andmestruktuuride tõttu ei ole saadetud sõnum saadaval mõlemast andmete levitamise versioonist (data distribution). V1 versioonis saadetud võrguarve on saadaval V1 andmete levitamise kaudu. V2 versioonis saadetud võrguarve on saadaval V2 andmete levitamise kaudu.

### Sõnumid

**Võrguteenuse arve lisamine**

Näidis päring:
```json
[
  {
    "meteringPointEic": "34Z6B80RJXDW7UPQ",
    "calculationTimestamp": "2023-10-17T07:13:11.076Z",
    "periodStart": "2023-10-17T07:13:11.076Z",
    "periodEnd": "2023-10-17T07:13:11.076Z",
    "containsCalculatedValues": true,
    "quantities": [
      {
        "direction": "IN",
        "day": 1.234,
        "night": 0.000,
        "total": 1.234
      },
      {
        "direction": "OUT",
        "day": 1.234,
        "night": 0.000,
        "total": 1.234
      }
    ],
    "netQuantities": [
      {
        "direction": "IN",
        "day": 1.234,
        "night": 0.000,
        "total": 1.234
      },
      {
        "direction": "OUT",
        "day": 1.234,
        "night": 0.000,
        "total": 1.234
      }
    ]
  },
  {
    "meteringPointEic": "34Z6B80RJXDW7UPQ",
    "calculationTimestamp": "2023-10-17T07:13:11.076Z",
    "periodStart": "2023-10-17T07:13:11.076Z",
    "periodEnd": "2023-10-17T07:13:11.076Z",
    "containsCalculatedValues": true,
    "quantities": [
      {
        "direction": "IN",
        "day": 1.234,
        "night": 0.000,
        "total": 1.234
      },
      {
        "direction": "OUT",
        "day": 1.234,
        "night": 0.000,
        "total": 1.234
      }
    ],
    "netQuantities": [
      {
        "direction": "IN",
        "day": 1.234,
        "night": 0.000,
        "total": 1.234
      },
      {
        "direction": "OUT",
        "day": 1.234,
        "night": 0.000,
        "total": 1.234
      }
    ]
  }
]
```
Näidis vastus:
```json
{
  "successful": [
    {
      "meteringPointEic": "34Z6B80RJXDW7UPQ",
      "calculationTimestamp": "2023-10-17T07:13:11.076Z",
      "periodStart": "2023-10-17T07:13:11.076Z",
      "periodEnd": "2023-10-17T07:13:11.076Z",
      "containsCalculatedValues": true,
      "quantities": [
        {
          "direction": "IN",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        },
        {
          "direction": "OUT",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        }
      ],
      "netQuantities": [
        {
          "direction": "IN",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        },
        {
          "direction": "OUT",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        }
      ]
    }
  ],
  "unsuccessful": [
    {
      "request": {
        "meteringPointEic": "34Z6B80RJXDW7UPQ",
        "calculationTimestamp": "2023-10-17T07:13:11.076Z",
        "periodStart": "2023-10-17T07:13:11.076Z",
        "periodEnd": "2023-10-17T07:13:11.076Z",
        "containsCalculatedValues": true,
        "quantities": [
          {
            "direction": "IN",
            "day": 0.123,
            "night": 1.1,
            "total": 1.223
          },
          {
            "direction": "OUT",
            "day": 0.123,
            "night": 1.1,
            "total": 1.223
          }
        ],
        "netQuantities": [
          {
            "direction": "IN",
            "day": 0.123,
            "night": 1.1,
            "total": 1.223
          },
          {
            "day": 0.123,
            "night": 1.1,
            "total": 1.223
          }
        ]
      },
      "error": {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "message": "Quantities must be up to 3 positions after comma",
        "code": "opp.validation.3-positions-after-comma",
        "traceId": "3fa85f6457174562b3fc2c963f66afa6",
        "args": [
          "string"
        ]
      }
    }
  ]
}
```
**Võrguteenuse arve otsing**

Näidis päring:
```json
GET /api/v2/network-bills?meteringPointEics=34Z6B80RJXDW7UPQ&meteringPointEics=38Z9A12BCDEF3456&periodStart=2023-10-01T00:00:00Z&periodEnd=2023-11-01T00:00:00Z&direction=IN
```

Näidis vastus:

```json
{
  "successful": [
    {
      "meteringPointEic": "34Z6B80RJXDW7UPQ",
      "calculationTimestamp": "2023-10-17T07:13:11.076Z",
      "periodStart": "2023-10-17T07:13:11.076Z",
      "periodEnd": "2023-10-17T07:13:11.076Z",
      "containsCalculatedValues": true,
      "quantities": [
        {
          "direction": "IN",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        },
        {
          "direction": "OUT",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        }
      ],
      "netQuantities": [
        {
          "direction": "IN",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        },
        {
          "direction": "OUT",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        }
      ]
    },
    {
      "meteringPointEic": "34Z6B80RJXDW7UPQ",
      "calculationTimestamp": "2023-10-17T07:13:11.076Z",
      "periodStart": "2023-10-17T07:13:11.076Z",
      "periodEnd": "2023-10-17T07:13:11.076Z",
      "containsCalculatedValues": true,
      "quantities": [
        {
          "direction": "IN",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        },
        {
          "direction": "OUT",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        }
      ],
      "netQuantities": [
        {
          "direction": "IN",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        },
        {
          "direction": "OUT",
          "day": 0.123,
          "night": 1.1,
          "total": 1.223
        }
      ]
    }
  ],
  "unsuccessful": [
    {
      "meteringPointEic": "38ZGO-10000012-N",
      "error": {
        "id": "346ce43c-1d39-4df6-abd3-9834cc604c25",
        "message": "No SUPPLY agreement for requested period",
        "code": "opp.error.business.no-supply-agreement-for-period",
        "args": [],
        "traceId": "346ce43c1d394df6abd39834cc604c25"
      }
    }
  ]
}
```