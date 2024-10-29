# Ühisarve

## Sisukord

- [Ühisarve](#ühisarve)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Ühisarve edastamine ja pärimine](#ühisarve-edastamine-ja-pärimine)
  - [Veebiliides](#veebiliides)
  - [Masinliidese sõnumid](#masinliidese-sõnumid)
  - [Sõnumite reeglid](#sõnumite-reeglid)
    - [Ühisarve lisamine ja muutmine](#ühisarve-lisamine-ja-muutmine)
      - [Sõnumi atribuutide reeglid](#sõnumi-atribuutide-reeglid)
      - [Täiendavad reeglid](#täiendavad-reeglid)
    - [Ühisarvete otsing ja alla laadimine](#ühisarvete-otsing-ja-alla-laadimine)
      - [Sõnumi atribuutide reeglid](#sõnumi-atribuutide-reeglid-1)
      - [Täiendavad reeglid](#täiendavad-reeglid-1)

## Sissejuhatus

Ühisarve võrguarve (lühidalt ühisarve) saatmise eelduseks on ühisarve leping Andmelaos. Loe täpsemalt dokumendist [Ühisarve leping](06.7-yhisarve-leping.md).

Vahendatava ühisarve rekvisiidid saadakse e-arve standardist ([Eesti e-arve kirjelduse juhend](https://media.voog.com/0000/0042/1620/files/Eesti_e-arve_kirjelduse_juhend_E_arve_saatmine%20ja%20presenteeerimine%20pangas_ver_1_0.pdf)).

## Ühisarve edastamine ja pärimine

Ühisarvet on võimalik edastada masinliidese vahendusel. Tulevikus tekib võimalus selleks ka veebiliidese vahendusel (vorm väikestele võrguettevõtjatele) ning allalaadimiseks (müüjatele).

Ühisarvete edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on leitav lehelt [Äriprotsessid](02-äriprotsessid.md#ühisarve-haldus)

## Veebiliides

> [!NOTE]
> Veebiliides on loomisel.

## Masinliidese sõnumid

| Sõnum                                        | Eesmärk                    | Kirjeldus ja reeglid                                                        |
|----------------------------------------------|----------------------------|-----------------------------------------------------------------------------|
| `POST /api/{version}/joint-invoice`          | Ühisarve lisamine/muutmine | [Ühisarve lisamine ja muutmine](#ühisarve-lisamine-ja-muutmine)             |
| `POST /api/{version}/joint-invoice/search`   | Ühisarve otsing            | [Ühisarvete otsing ja alla laadimine](#ühisarvete-otsing-ja-alla-laadimine) |
| `POST /api/{version}/joint-invoice/download` | Ühisarve alla laadimine    | [Ühisarvete otsing ja alla laadimine](#ühisarvete-otsing-ja-alla-laadimine) |

## Sõnumite reeglid

### Ühisarve lisamine ja muutmine

Ühisarve sõnum koosneb järgmistest osadest:

- `marketParticipantContext` sektsioon nagu igal sõnumil
- `jointInvoiceHeadersList` - nimekiri `jointInvoiceHeaders` ehk päise andmetest. Sisaldab ühisarve metaandmeid
- `invoiceList` - nimekiri `invoice` ehk arve failidest base64 kujul

Ühisarve muutmine ei ole võimalik. Muudatuste edastamiseks saadab võrguettevõtja või suletud jaotusvõrgu operaator uue kreedit ühisarve XML-i ja vajadusel täiendava ühisarve

#### Sõnumi atribuutide reeglid

- `jointInvoiceHeaders` ehk päise andmed on:

| Atribuut teenuses | Selgitus                                     | Kohustuslik? | Muud reeglid                                                                         |
|-------------------|----------------------------------------------|--------------|--------------------------------------------------------------------------------------|
| senderEic         | Ühisarve saatja EIC kood                     | jah          |                                                                                      |
| receiverEic       | Ühisarve adressaadi EIC kood                 | jah          |                                                                                      |
| commodityType     | Energiakandja liik                           | jah          | Üks neist: ELECTRICITY, NATURAL_GAS                                                  |
| customerEic       | Mõõtepunkti kliendi EIC kood                 | jah          |                                                                                      |
| meterEics         | Mõõtepunkti(de) EIC koodid                   | jah          | Arvel olevate mõõtepunktide EIC koodid                                               |
| dataPeriodStart   | Ühisarve arveldusperioodi algus              | jah          |                                                                                      |
| dataPeriodEnd     | Ühisarve arveldusperioodi lõpp               | jah          |                                                                                      |
| fileName          | positsioonil "invoice" edastatava faili nimi | jah          | Peab ühe sõnumi piires olema unikaalne ja vastama failinimele positsioonil `invoice` |

- `invoice` - ehk faili andmed on:
  - faili nimi - peab vastama positsioonil `jointInvoiceHeadersList.object.fileName` väärtusele, et süsteem saaks faili ja tema päise omavahel kokku viia. Nt "joint_invoice.xml"
  - faili sisu - base64 formaadis kodeeritud e-arve XML

#### Täiendavad reeglid

- Saatja ja adressaadi vahel peab olema kehtiv ühisarve leping, mille kehtivus katab ühisarve kehtivuse.
- Saatja ja kliendi vahel peab olema kehtiv võrguleping, mille kehtivus katab ühisarve kehtivuse.
- Adressaadi ja kliendi vahel peab olema kehtiv avatud tarne leping, mille kehtivus katab ühisarve kehtivuse.
- Päiseid ja faile peab sõnumis olema täpsel samas koguses

#### Näidissõnumid

Kuivõrd `joint-invoice` sõnum on `multipart/form-data` formaadis, siis alljärgnevad näidissõnumid pole täpses vaid pseudo struktuuris, et edasi anda sõnumi edastamise reegleid ja loogikat.

<details>

<summary>Näide "Üks mõõtepunkt, üks arve"</summary>

```json
"marketParticipantContext": {
    "marketParticipantIdentification": "38X-EIN-GO-----0",
    "marketParticipantRole": "GRID_OPERATOR",
    "commodityType": "ELECTRICITY"
},
"jointInvoiceHeadersList": [
    {
        "senderEic": "38X-EIN-GO-----0",
        "receiverEic": "38X-EIN-OS-----J",
        "customerEic": "38X-AVP-ZW6700C6",
        "commodityType": "ELECTRICITY",
        "meterEics": [
            "38ZGO-1000006K-N",
        ],
        "dataPeriodStart": "2024-10-23T00:00:00+03:00",
        "dataPeriodEnd": "2024-10-24T00:00:00+03:00",
        "fileName": "joint_invoice_1.xml"
    }
],
"invoiceList": [
    {
        filename="joint_invoice_1.xml"

        PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPEVfSW52b2ljZSB4bWxuczp4c2k9Imh0dHA6Ly93d3cudzMub3JnLzIwMDEvWE1MU2NoZW1hLWluc3RhbmNlIiB4c2k6bm9OY
        W1lc3BhY2VTY2hlbWFMb2NhdGlvbj0iZS0KaW52b2ljZV92ZXIxLjExLnhzZCI+CjwvRV9JbnZvaWNlPg==
    }
]
```

</details>

<details>

<summary>Näide "Mitu mõõtepunkti ühel arvel"</summary>

```json
"marketParticipantContext": {
    "marketParticipantIdentification": "38X-EIN-GO-----0",
    "marketParticipantRole": "GRID_OPERATOR",
    "commodityType": "ELECTRICITY"
},
"jointInvoiceHeadersList": [
    {
        "senderEic": "38X-EIN-GO-----0",
        "receiverEic": "38X-EIN-OS-----J",
        "customerEic": "38X-AVP-ZW6700C6",
        "commodityType": "ELECTRICITY",
        "meterEics": [
            "38ZGO-1000006K-N",
            "38ZGO-1000006P-8"
        ],
        "dataPeriodStart": "2024-10-23T00:00:00+03:00",
        "dataPeriodEnd": "2024-10-24T00:00:00+03:00",
        "fileName": "joint_invoice_1.xml"
    }
],
"invoiceList": [
    {
        filename="joint_invoice_1.xml"

        PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPEVfSW52b2ljZSB4bWxuczp4c2k9Imh0dHA6Ly93d3cudzMub3JnLzIwMDEvWE1MU2NoZW1hLWluc3RhbmNlIiB4c2k6bm9OY
        W1lc3BhY2VTY2hlbWFMb2NhdGlvbj0iZS0KaW52b2ljZV92ZXIxLjExLnhzZCI+CjwvRV9JbnZvaWNlPg==
    }
]
```

</details>

<details>

<summary>Näide "Mitu arvet"</summary>

```json
"marketParticipantContext": {
    "marketParticipantIdentification": "38X-EIN-GO-----0",
    "marketParticipantRole": "GRID_OPERATOR",
    "commodityType": "ELECTRICITY"
},
"jointInvoiceHeadersList": [
    {
        "senderEic": "38X-EIN-GO-----0",
        "receiverEic": "38X-EIN-OS-----J",
        "customerEic": "38X-AVP-ZW6700C6",
        "commodityType": "ELECTRICITY",
        "meterEics": [
            "38ZGO-1000006K-N"
        ],
        "dataPeriodStart": "2024-10-23T00:00:00+03:00",
        "dataPeriodEnd": "2024-10-24T00:00:00+03:00",
        "fileName": "joint_invoice_1.xml"
    },
    {
        "senderEic": "38X-EIN-GO-----0",
        "receiverEic": "38X-EIN-OS-----J",
        "customerEic": "38X-AVP-V8JG00C9",
        "commodityType": "ELECTRICITY",
        "meterEics": [
            "38ZGO-10000030-L",
            "38ZGO-10000031-I",
            "38ZGO-10000032-F"
        ],
        "dataPeriodStart": "2024-10-01T00:00:00+03:00",
        "dataPeriodEnd": "2024-11-01T00:00:00+03:00",
        "fileName": "joint_invoice_2.xml"
    }
],
"invoiceList": [
    {
        filename="joint_invoice_1.xml"

        PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPEVfSW52b2ljZSB4bWxuczp4c2k9Imh0dHA6Ly93d3cudzMub3JnLzIwMDEvWE1MU2NoZW1hLWluc3RhbmNlIiB4c2k6bm9OY
        W1lc3BhY2VTY2hlbWFMb2NhdGlvbj0iZS0KaW52b2ljZV92ZXIxLjExLnhzZCI+CjwvRV9JbnZvaWNlPg==
    },
    {
        filename="joint_invoice_2.xml"

        PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPEVfSW52b2ljZSB4bWxuczp4c2k9Imh0dHA6Ly93d3cudzMub3JnLzIwMDEvWE1MU2NoZW1hLWluc3RhbmNlIiB4c2k6bm9OY
        W1lc3BhY2VTY2hlbWFMb2NhdGlvbj0iZS0KaW52b2ljZV92ZXIxLjExLnhzZCI+CjwvRV9JbnZvaWNlPg==
    },
]
```

</details>


### Ühisarvete otsing ja alla laadimine

Ühisarve otsimiseks ja arve allalaadimiseks on loodud eraldi teenused. Otsingu teenus tagastab arvete ID-d, mida saab kasutada allalaadimise teenuses.

Ühisarveid on võimalik otsida ja alla laadida ka veebiliidese vahendusel.

#### Sõnumi atribuutide reeglid

Ühisarveid on võimalik otsida erinevate tunnuste alusel:

| Atribuut teenuses | Selgitus                                                                    | Kohustuslik? | Muud reeglid                                            |
|-------------------|-----------------------------------------------------------------------------|--------------|---------------------------------------------------------|
| invoiceId         | Ühisarve faili ID, mis saadi vastuseks ühisarve lisamise käigus             | ei           | Võimaldab otsida konkreetset ühisarvet                  |
| commodityType     | Energiakandja liik                                                          | jah          | Üks neist: ELECTRICITY, NATURAL_GAS                     |
| createdTimeFrom   | Ühisarve lisamise aeg alates                                                | jah          |                                                         |
| createdTimeTo     | Ühisarve lisamise aeg kuni                                                  | jah          | Peab olema suurem kui `createdTimeFrom`                 |
| senderEic         | Ühisarve saatja EIC kood                                                    | ei           |                                                         |
| receiverEic       | Ühisarve adressaadi EIC kood                                                | ei           |                                                         |
| customerEic       | Mõõtepunkti kliendi EIC kood                                                | ei           |                                                         |
| meterEics         | Mõõtepunkti(de) EIC koodid                                                  | ei           |                                                         |
| dataPeriodStart   | Ühisarve arveldusperioodi algus                                             | ei           |                                                         |
| dataPeriodEnd     | Ühisarve arveldusperioodi lõpp                                              | ei           | Kui antud, siis peab olema suurem kui `dataPeriodStart` |
| unread            | Kas ühisarve on varasemalt **adressaadi** poolt korra alla laetud või mitte | ei           |                                                         |

Näidissõnum:

```bash
curl -X POST -H "Content-Type: multipart/form-data" \
  -F "invoiceList=@file1.xml" \
  -F "invoiceList=@file2.xml" \
  -F "jointInvoiceHeadersList=[{\"senderEic\":\"38X-AVP-8T8D00EC\",\"receiverEic\":\"38X-AVP-1G0G00E7\",\"customerEic\":\"38X-PP-03712673A\",\"commodityType\":\"ELECTRICITY\",\"meterEics\":[\"38Z-EE-CS-0041-X\",\"38Z-EE-CS-004Z-5\"],\"dataPeriodStart\":\"2023-10-03T22:00:00Z\",\"dataPeriodEnd\":\"2023-11-06T23:00:00Z\",\"fileName\":\"file1\"},{\"senderEic\":\"38X-AVP-8T8D00EC\",\"receiverEic\":\"38X-AVP-1G0G00E7\",\"customerEic\":\"38X-PP-03712673A\",\"commodityType\":\"ELECTRICITY\",\"meterEics\":[\"38Z-EE-CS-0041-X\",\"38Z-EE-CS-004Z-5\"],\"dataPeriodStart\":\"2023-10-03T22:00:00Z\",\"dataPeriodEnd\":\"2023-11-06T23:00:00Z\",\"fileName\":\"file2\"}]" \
  -F "marketParticipantContext={\"marketParticipantIdentification\":\"38X-AVP-UQLB00EB\",\"marketParticipantRole\":\"GRID_OPERATOR\",\"commodityType\":\"ELECTRICITY\"}" \
  {{restHost}}/api/v1/joint-invoice
```

Otsingu sõnumi vastuses on ühisarve faili ID (`invoiceId`), mida saab kasutada sisendina teenuses `POST /api/{version}/joint-invoice/download`

#### Täiendavad reeglid

- Kui ühisarvete otsijaks on võrguettevõtja või suletud jaotusvõrgu operaator, siis tagastatakse ainult need võrguarved, kus päringu saatja on ühisarve saatja (võimaldab otsida enda saadetud ühisarveid)
- Kui ühisarvete otsijaks on avatud tarnija, siis tagastatakse ainult need võrguarved, kus päringu saatja on ühisarve adressaat.
- Kui ühisarve laeb alla adressaat, siis märgitakse arve kättesaaduks (`unread = false`)
