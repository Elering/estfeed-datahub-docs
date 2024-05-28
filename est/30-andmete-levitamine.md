# Andmete levitamine

## Sisukord

<!-- TOC -->
* [Andmete levitamine](#andmete-levitamine)
  * [Sisukord](#sisukord)
  * [Sissejuhatus](#sissejuhatus)
  * [Andmeuuenduste skaneerimine](#andmeuuenduste-skaneerimine)
  * [Andmeuuenduste levitamine](#andmeuuenduste-levitamine)
  * [Sõnumi struktuur](#sõnumi-struktuur)
  * [Andmetüübid](#andmetüübid)
    * [Leping](#leping)
      * [Atribuudid](#atribuudid)
      * [Näited](#näited)
    * [Mõõtepunkt](#mõõtepunkt)
      * [Atribuudid](#atribuudid-1)
      * [Näited](#näited-1)
    * [Mõõteandmed](#mõõteandmed)
      * [Atribuudid](#atribuudid-2)
      * [Näited](#näited-2)
    * [Võrguteenuse arve](#võrguteenuse-arve)
      * [Atribuudid](#atribuudid-3)
      * [Näited](#näited-3)
    * [Kliendi metaandmed](#kliendi-metaandmed)
      * [Atribuudid](#atribuudid-4)
      * [Näited](#näited-4)
    * [Ligipääsuõigused](#ligipääsuõigused)
      * [Atribuudid](#atribuudid-5)
      * [Näited](#näited-5)
<!-- TOC -->

## Sissejuhatus

Äriprotsesside edukaks ja probleemidevabaks toimimiseks on vaja, et liidestunud turuosaliste süsteemid oleks teadlikud lisandunud ja muutunud informatsioonist.

Selleks on vaja uus info turuosaliste süsteemideni toimetada. Käesolev dokument kirjeldab tehnilist lahendust, kuidas masinate vahelise liidese abil andmete uuendusi levitatakse.

## Andmeuuenduste skaneerimine

Erinevalt vanast Andmelaost, uus Andmeladu sõnumeid liidestuvatatele osapooltele ei saada vaid eeldab, et liidestuv süsteem kontrollib kas talle on uus sõnumeid. Selleks on loodud spetsiaalne
uuenduste tõmbamise API liides `/data-distribution/search `, mis toimib standardsel moel:

- liidestunud turuosalise süsteem saadab päringu defineerides ajavahemiku ja andmeobjekti tüübi.
- Andmeladu leiab eelnevalt genereeritud andmete levitamise sõnumid, mille adressaat on sõnumi saatnud turuosaline ning mis vastavad päringu tingimustele.
- Andmeladu tagastab uued või muutunud andmeobjektide andmed koos muudatuse põhjendusega.

Liidestunud turuosalise süsteem skaneerib muudatuste API-t endale sobiva intervalliga võttes arvesse andmeobjektide tekkimise ja muutumise tavapärast sagedust:

- aeglaselt lisanduvaid ja muutuvaid andmeid (nt mõõtepunktid) on sobilik skaneerida näiteks 1-4 korda ööpäevas.
- kiiresti lisanduvaid ja muutuvaid andmeid (nt mõõteandmed) on sobilik skaneerida sama tihendusega, nagu on ette nähtud andmete lisandumine - näiteks iga tund või tihedamalt. See aitab Andmelaol
  koormuste tippudega paremini toime tulla.

Andmeobjekti tüübid on:

- METERING_POINT - mõõtepunkt
- METERING_DATA - mõõteandmed
- NETWORK_BILL - võrguteenuse arve
- CUSTOMER_DATA - kliendi metaandmed (arveldamise andmete edastuseks nimetatud müüjale)
- AGREEMENT - leping ja üldteenuse teavitus, mis on realiseeritud lepinguna
- PERMISSION - ligipääsuõigused (antud Kliendiportaali kaudu)

Maksimaalne päritava perioodi pikkus on:

- mõõteandmed: 1 tund
- muud andmed: 1 päev

> **Note**
> Pikema ajaperioodi sõnumite pärimiseks on võimalik saata mitu erinevat päringut erinevate perioodide kohta. Nt esimene sõnum 02.01.2024-03.01.2024 perioodi ja teine 01.01.2024-02.01.2024 perioodi kohta.

## Andmeuuenduste levitamine

Eleringi meeskond arutab erinevaid tehnilisi lahendusi, kuidas võimaldada võimekamatel liidestunud süsteemidel saada andmeuuendusi kiiremini ja ilma skaneerimiseta. Konkreetne tehniline lahendus on
alles välja töötamisel. Selle tekkimisel teavitatakse turuosalisi aegsasti ja põhjalikult.

## Sõnumi struktuur

Iga andmete levitamise vastussõnum koosneb ühis- ja andmetüübi spetsiifilistest atribuutidest:

| Atribuut     | Tüüp     | Alati sõnumis? | Märkused                                                                                     |
|--------------|----------|----------------|----------------------------------------------------------------------------------------------|
| id           | int      | jah            | Unikaalne sõnumi ID, mis on ajas kasvav                                                      |
| createdTime  | datetime | jah            | Andmete levitamise sõnumi (mitte selle sõnumi, mis andmete levitamise põhjustas) loomise aeg |
| resourceType | string   | jah            | Andmeobjekti tüüp                                                                            |
| reason       | string   | ei             | Võimalikud väärtused: CREATE, UPDATE, DELETE. Võib olla ka tühi.                             |
| content      | string   | jah            | Sõnumi sisu vastavalt andmetüübile (vt kirjeldus allpool)                                    |
| pagination   | object   | jah            | Standardsed pagineerimise elemendid                                                          |

> **Note**
> "reason" atribuudi käitumise muutmine on arenduses (et seda paremaks muuta)

Näide vastussõnumist:

```json
{
  "dataDistributions": [
    {
      "id": 4656,
      "createdTime": "2024-05-23T10:08:44.320005900Z",
      "resourceType": "AGREEMENT",
      "content": "[{\"meterEic\":\"38ZGO-1000001U-D\",\"agreementType\":\"GENERAL_SERVICE\",\"preliminaryTerminationFee\":false,\"commodityType\":\"ELECTRICITY\",\"validFrom\":\"2024-05-22T21:00Z\",\"validTo\":\"2024-05-31T21:00Z\"}]"
    },
    {
      "id": 4660,
      "createdTime": "2024-05-23T10:10:13.682197100Z",
      "resourceType": "AGREEMENT",
      "reason": "CREATE",
      "content": "[{\"agreementId\":\"einar-2024-05-23T13:08:42.936268+03:00-EST\",\"meterEic\":\"38ZGO-1000001U-D\",\"agreementType\":\"SUPPLY\",\"preliminaryTerminationFee\":true,\"commodityType\":\"ELECTRICITY\",\"validFrom\":\"2024-05-22T21:00Z\",\"validTo\":\"2024-06-30T21:00Z\",\"serviceProviderEic\":\"38X-EIN-OS-----J\",\"customerEic\":\"38X-AVP-ZW6700C6\"}]"
    },
    {
      "id": 4661,
      "createdTime": "2024-05-23T10:10:13.682552100Z",
      "resourceType": "AGREEMENT",
      "reason": "CREATE",
      "content": "[{\"agreementId\":\"einar-2024-05-23T13:10:12.799579+03:00-EST\",\"meterEic\":\"38ZGO-1000001U-D\",\"agreementType\":\"SUPPLY\",\"preliminaryTerminationFee\":false,\"commodityType\":\"ELECTRICITY\",\"validFrom\":\"2024-06-30T21:00Z\"}]"
    }
  ],
  "pagination": {
    "page": 0,
    "totalPages": 1
  }
}

```

## Andmetüübid

### Leping

#### Atribuudid

Süsteem kasutab sama struktuuri ja atribuute, nagu `POST /api/{version}/agreement` teenuse vastussõnumis, kuid esinevad järgmised erisused:

- `agreementId`, `meterEic` ja `validTo` võivad puududa, kui need puuduvad algses lepingu sõnumis.
- `serviceProviderEic` ja `customerEic` puuduvad, kui see informatsioon ei kuulu vastavalt ärireeglitele avalikustamisele.

#### Näited

```json
[
    {
        "agreementId": "einar-2024-04-03T16:25:08.569885+03:00-EST",
        "meterEic": "38ZGO-1000001B-X",
        "agreementType": "SUPPLY",
        "preliminaryTerminationFee": false,
        "commodityType": "ELECTRICITY",
        "validFrom": "2024-04-03T21:00:00Z",
        "validTo": "2024-04-17T21:00:00Z"
    }
]
```

```json
[
  {
    "agreementType": "JOINT_INVOICE",
    "preliminaryTerminationFee": false,
    "commodityType": "ELECTRICITY",
    "validFrom": "2024-05-31T21:00Z",
    "serviceProviderEic": "38X-EIN-NS-----R",
    "customerEic": "38X-EIN-ALL----B"
  }
]
```

### Mõõtepunkt

Süsteem kasutab sama struktuuri ja atribuute, nagu `PUT /api/{version}/meter` teenuses.

#### Atribuudid

#### Näited

```json
{
    "meteringPoint": {
        "meterEic": "38ZGO-10000018-5",
        "meteringType": "NON_REMOTE_READING"
    },
    "meterLocation": {
        "adrId": 3182855,
        "comment": "Maja taga",
        "county": "Rapla maakond",
        "municipality": "Kehtna vald",
        "locality": "Järvakandi alev",
        "streetAddress": ", Uus tn, 20-3",
        "postcode": "79101",
        "coordinates": {
            "coordinateSystem": "LEST97",
            "latitude": 6515113.24,
            "longitude": 546858.53
        }
    },
    "electricityCharacteristics": {
        "consumptionScale": "SMALL",
        "connectionState": "DISCONNECTED",
        "resolution": "PT15M",
        "customerType": "MICRO",
        "production": true,
        "productionSource": "SOLAR",
        "transmissionNetworkEic": "38A-EE-98-4634-U",
        "apartmentAssociation": true,
        "isolatedMeteringPoint": false,
        "electricalHeating": true,
        "chargingPoint": false,
        "storageCapacity": 603.4,
        "storageEnergy": 636.83,
        "productionCapacity": 580.39,
        "transmissionCapacity": 440.17
    }
}
```

### Mõõteandmed

#### Atribuudid

Mõõteandmete levitamise sõnumi struktuur on täpselt sama, nagu `POST /meter-data` sõnumil.

#### Näited

```json
[
    {
        "meterEic": "38ZGO-1000000C-Y",
        "periods": [
            {
                "r": "PT15M",
                "aI": [
                    {
                        "pS": "2024-03-21T00:00:00+02:00",
                        "inQty": {
                            "rTime": "2024-03-21T09:45:58.146109Z",
                            "rType": "E",
                            "kwh": 12.803
                        },
                        "outQty": {
                            "rTime": "2024-03-21T09:45:58.146118Z",
                            "rType": "E",
                            "kwh": 1.417
                        }
                    },
                    {
                        "pS": "2024-03-21T00:15:00+02:00",
                        "inQty": {
                            "rTime": "2024-03-21T09:45:58.146123Z",
                            "rType": "E",
                            "kwh": 49.497
                        },
                        "outQty": {
                            "rTime": "2024-03-21T09:45:58.146126Z",
                            "rType": "E",
                            "kwh": 27.454
                        }
                    }
                ]
            }
        ]
    }
]
```

### Võrguteenuse arve

#### Atribuudid

Võrguteenuse arve levitamise sõnumi struktuur on täpselt sama, nagu `POST /network-bill` sõnumil.

#### Näited

```json
[
    {
        "commodityType": "ELECTRICITY",
        "meterEic": "38ZGO-10000013-K",
        "networkBillPeriod": {
            "calculationTimestamp": "2024-05-02T17:23:07.648663+03:00",
            "containsCalculatedValues": true,
            "measurements": [
                {
                    "day": 10,
                    "direction": "IN",
                    "measurementUnit": "KWH",
                    "night": 10,
                    "total": 20
                },
                {
                    "day": 20,
                    "direction": "OUT",
                    "measurementUnit": "KWH",
                    "night": 20,
                    "total": 40
                }
            ],
            "periodEnd": "2024-03-25T00:00+02:00",
            "periodStart": "2024-03-24T00:00+02:00"
        }
    }
]
```

### Kliendi metaandmed

#### Atribuudid

Kliendi metaandmete levitamise sõnum koosneb järgmistest sektsioonidest:

- `customerType` - sama nagu teenuse `api/{version}/customer/search` vastussõnumis
- `customerMetadata` - sama nagu teenuse `api/{version}/customer/search` vastussõnumis
- `customerEic` - kliendi EIC kood

#### Näited

```json
{
  "customerType": "PHYSICAL_PERSON",
  "customerMetadata": [
    {
      "metadataType": "BILLING_METHOD",
      "metadataValue": "BANK,POST,EMAIL",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "FIRST_NAME",
      "metadataValue": "Einars",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "LAST_NAME",
      "metadataValue": "Arros",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "PHONE",
      "metadataValue": "6128888",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "BILLING_ADDRESS",
      "metadataValue": "A.H.Tammsaare tee 55, Mustamäe linnaosa, Tallinn",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "BILLING_BANK_NAME",
      "metadataValue": "SEB Pank Eesti",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "EMAIL",
      "metadataValue": "einar@srini.ee",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "MOBILE_PHONE",
      "metadataValue": "+37258092567",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "BILLING_BANK_ACCOUNT",
      "metadataValue": "EE1234567890",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    }
  ],
  "customerEic": "38X-AVP-ZW6700C6"
}
```

```json
{
  "customerType": "PHYSICAL_PERSON",
  "customerMetadata": [
    {
      "metadataType": "FIRST_NAME",
      "metadataValue": "Einars",
      "validFrom": "2024-05-27T12:58:18.648130Z"
    },
    {
      "metadataType": "LAST_NAME",
      "metadataValue": "Arros",
      "validFrom": "2024-05-27T12:58:18.648130Z"
    }
  ],
  "customerEic": "38X-AVP-ZW6700C6"
}
```

### Ligipääsuõigused

#### Atribuudid

| Atribuut            | Tüüp     | Alati väljundis? | Kirjeldus                                                                                                                                                                                                                                                                                                                             |
|---------------------|----------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| mandateCustomerEic  | string   | JAH              | 16-kohaline turuosalise EIC kood                                                                                                                                                                                                                                                                                                      |
| mandateCustomerType | string   | JAH              | Üks järgnevatest: PRIVATE, LEGAL                                                                                                                                                                                                                                                                                                      |
| meteringPointEic    | string   | JAH              | 16-kohaline mõõtepunkti EIC kood                                                                                                                                                                                                                                                                                                      |
| ownerCustomerEic    | string   | JAH              | 16-kohaline kliendi EIC kood                                                                                                                                                                                                                                                                                                          |
| ownerCustomerType   | string   | JAH              | Üks järgnevatest: PRIVATE, LEGAL                                                                                                                                                                                                                                                                                                      |
| participantRoleType | string   | JAH              | Avatud tarnija puhul alati OPEN_SUPPLIER; agregaatori puhul alati AGGREGATOR, energiateenuse puhul alati ENERGY_SERVICE_PROVIDER                                                                                                                                                                                                      |
| permissionType      | string   | JAH              | Alati ACCESS                                                                                                                                                                                                                                                                                                                          |
| purpose             | string   | JAH              | Avatud tarnija puhul alati ENERGY_SUPPLY_OFFER; agregaatori puhul alati AGGREGATION_OFFER; energiateenuse puhul üks järgmistest: METERING_DATA_ANALYSIS_AND_MONITORING, MEASUREWAY_ANALYSIS_AND_ENERGY_SAVING, TELIA_IOT_SERVICE, INFORMANT_CALCULATIONS_AND_ANALYSIS, TARKVENT_CONSUMPTION_MONITORING, R8TECH_CONSUMPTION_MONITORING |
| status              | string   | JAH              | Alati APPROVED                                                                                                                                                                                                                                                                                                                        |
| subjectPeriodFrom   | datetime | JAH              | Ajaperioodi algus, mille andmetele ligipääsuõigus ligipääsu annab                                                                                                                                                                                                                                                                     |
| subjectPeriodTo     | datetime | JAH              | Ajaperioodi algus, mille andmetele ligipääsuõigus ligipääsu annab                                                                                                                                                                                                                                                                     |
| validFrom           | datetime | JAH              | Ligipääsuõiguse kehtivuse algus                                                                                                                                                                                                                                                                                                       |
| validTo             | datetime | EI               | Ligipääsuõiguse kehtivuse lõpp                                                                                                                                                                                                                                                                                                        |

#### Näited

```json
{
    "mandateCustomerEic": "38XVK-08600000-Q",
    "mandateCustomerType": "LEGAL",
    "meteringPointEic": "38Z-EE-DL-00N39F",
    "ownerCustomerEic": "38X-AVP-ILS600CI",
    "ownerCustomerType": "PRIVATE",
    "participantRoleType": "OPEN_SUPPLIER",
    "permissionType": "ACCESS",
    "purpose": "ENERGY_SUPPLY_OFFER",
    "status": "APPROVED",
    "subjectPeriodFrom": "2023-05-20T00:00Z",
    "subjectPeriodTo": "2024-05-20T00:00Z",
    "validFrom": "2024-05-20T21:37:54.499Z",
    "validTo": "2024-05-22T21:37:54.499Z"
}
```
