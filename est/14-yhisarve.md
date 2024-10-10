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

Ühisarve sõnum koosneb kahest osast:

- `jointInvoiceHeader`
- `invoice`

Header ehk päis sisaldab ühisarve metaandmeid ja invoice ehk arve fail sisaldab ühisarvet ennast base64 kujul.

Ühisarve muutmine ei ole võimalik. Muudatuste edastamiseks saadab võrguettevõtja või suletud jaotusvõrgu operaator uue kreedit ühisarve XML-i ja vajadusel täiendava ühisarve

#### Sõnumi atribuutide reeglid

- Päise andmed on:

| Atribuut teenuses | Selgitus                                     | Kohustuslik? | Muud reeglid                                                                         |
|-------------------|----------------------------------------------|--------------|--------------------------------------------------------------------------------------|
| senderEic         | Ühisarve saatja EIC kood                     | jah          |                                                                                      |
| receiverEic       | Ühisarve adressaadi EIC kood                 | jah          |                                                                                      |
| commodityType     | Energiakandja liik                           | jah          | Üks neist: ELECTRICITY, NATURAL_GAS                                                  |
| customerEic       | Mõõtepunkti kliendi EIC kood                 | jah          |                                                                                      |
| meterEics         | Mõõtepunkti(de) EIC koodid                   | jah          |                                                                                      |
| dataPeriodStart   | Ühisarve arveldusperioodi algus              | jah          |                                                                                      |
| dataPeriodEnd     | Ühisarve arveldusperioodi lõpp               | jah          |                                                                                      |
| fileName          | positsioonil "invoice" edastatava faili nimi | jah          | Peab ühe sõnumi piires olema unikaalne ja vastama failinimele positsioonil `invoice` |

#### Täiendavad reeglid

- Saatja ja adressaadi vahel peab olema kehtiv ühisarve leping, mille kehtivus katab ühisarve kehtivuse.
- Saatja ja kliendi vahel peab olema kehtiv võrguleping, mille kehtivus katab ühisarve kehtivuse.
- Adressaadi ja kliendi vahel peab olema kehtiv avatud tarne leping, mille kehtivus katab ühisarve kehtivuse.
- Päiseid ja faile peab sõnumis olema täpsel samas koguses

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
