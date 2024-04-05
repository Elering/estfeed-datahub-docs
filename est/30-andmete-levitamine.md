# Andmete levitamine

## Sisukord

<!-- TOC -->
* [Andmete levitamine](#andmete-levitamine)
  * [Sisukord](#sisukord)
  * [Sissejuhatus](#sissejuhatus)
  * [Andmeuuenduste skaneerimine](#andmeuuenduste-skaneerimine)
  * [Andmeuuenduste levitamine](#andmeuuenduste-levitamine)
  * [Näidised](#näidised)
    * [Leping](#leping)
    * [Mõõtepunkt](#mõõtepunkt)
    * [Mõõteandmed](#mõõteandmed)
    * [Võrguteenuse arve](#võrguteenuse-arve)
    * [Kliendi metaandmed](#kliendi-metaandmed)
    * [Raportid](#raportid)
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
- CUSTOMER - kliendi metaandmed (arveldamise andmete edastuseks nimetatud müüjale)
- AGREEMENT - leping ja üldteenuse teavitus, mis on realiseeritud lepinguna
- REPORT - raportid

Maksimaalne päritava perioodi pikkus on:

- mõõteandmed: 1 tund
- muud andmed: 1 päev

## Andmeuuenduste levitamine

Eleringi meeskond arutab erinevaid tehnilisi lahendusi, kuidas võimaldada võimekamatel liidestunud süsteemidel saada andmeuuendusi kiiremini ja ilma skaneerimiseta. Konkreetne tehniline lahendus on
alles välja töötamisel. Selle tekkimisel teavitatakse turuosalisi aegsasti ja põhjalikult.

## Näidised

### Leping

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

### Mõõtepunkt

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

> **Note**
> Näidised on loomisel

### Kliendi metaandmed

> **Note**
> Näidised on loomisel

### Raportid

> **Note**
> Näidised on loomisel
