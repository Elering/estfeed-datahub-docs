# Andmete levitamine

## Sisukord

<!-- TOC -->
* [Andmete levitamine](#andmete-levitamine)
  * [Sisukord](#sisukord)
  * [Andmeuuenduste levitamine](#andmeuuenduste-levitamine)
    * [Üldreeglid](#üldreeglid)
    * [Mõõtepunkti reeglid](#mõõtepunkti-reeglid)
    * [Lepingute reeglid](#lepingute-reeglid)
    * [Mõõteandmete reeglid](#mõõteandmete-reeglid)
    * [Võrguteenuse arve reeglid](#võrguteenuse-arve-reeglid)
    * [Kliendi metaandmete reeglid](#kliendi-metaandmete-reeglid)
    * [Ligipääsuõiguste reeglid](#ligipääsuõiguste-reeglid)
    * [Kooskõlastusega lepingute muudatuste reeglid](#kooskõlastusega-lepingute-muudatuste-reeglid)
  * [Andmeuuenduste skaneerimine](#andmeuuenduste-skaneerimine)
    * [Muudatuse põhjus (reason)](#muudatuse-põhjus-reason)
      * [Lihtväärtused](#lihtväärtused)
      * [Liitväärtused](#liitväärtused)
  * [Sõnumid](#sõnumid)
    * [Versioonid](#versioonid)
    * [Uued teenused](#uued-teenused)
    * [Vanad teenused](#vanad-teenused)
      * [Päring](#päring)
      * [Vastus](#vastus)
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

## Andmeuuenduste levitamine

Andmelaos on realiseeritud erinevad ärireeglid, millal ja kellele andmeuuendusi levitatakse. Käesolevas dokumendis kõiki reegleid ei kirjeldata, kuid selleks, et aimu anda, mismoodi andmed peamiselt
liiguvad, siis siin on üldistatul kujul loetelu tähtsamatest reeglitest.

### Üldreeglid

- Andmeladu tuvastab teavitatavad osapooled vastavalt lepingutes olevatele andmetele.
- Teavitatavad osapooled jagunevad kaheks:
  - Otsesed osapooled - nende õigus teavitustele tuleneb otsesest lõppkasutaja lepingust
  - Portfellipakkujad - nende õigus teavitustele tuleneb portfelli lepingutest.
- Andmete saatjatele/muutjatele muudatust andmelevituse kaudu tagasi ei peegeldata
- Kõiki portfellipakkujaid erinevates tasemetes teavitatakse ühelaadselt
- Üldiselt on portfellipakkujad erinevate muudatuste teavituste adressaadid. Ainult mõnel üksikul juhul teavitatakse ainult otsest osapoolt. **Alljärgnevates sektsioonides portfellipakkujaid eraldi välja ei tooda**

### Mõõtepunkti reeglid

- Mõõtepunkti, millel puuduvad kehtivad või tulevikus kehtima hakkavad lepingud, muudatusi ei levitata

| Tingimus                                     | Levitamine                                                            |
|----------------------------------------------|-----------------------------------------------------------------------|
| Piirimõõtepunkti andmeid muudetakse          | Klient                                                                |
| Mõõtepunkti andmeid muudetakse               | Avatud tarnija, nimetatud müüja, agregeerimise mõõtepunkti agregaator |


### Lepingute reeglid

- Teenusepakkuja portfellihaldur on alati andmete levitamise subjekt.
- Süsteem otsustab vastavalt ärireeglitele, kas levitatakse lepingu täis- või osaline andmestik.
- Agregeerimise lepingu lisamisel/muutmisel/kustutamisel kontrollitakse, kas on ajalist kattuvust ülemmõõtepunkti GENERAL_SERVICE või SUPPLY või BORDER_SUPPLY lepingutega.
  - Kui ei ole, siis mingit andmete levitamist agregeerimise lepingu lisamisele/muutmisele/kustutamisele ei järgne
  - Kui on, siis järgneb
- GENERAL_SERVICE lepingud levitatakse alles peale nende aktiveerumist

| Tingimus                                                                                          | Levitamine                                                                                              |
|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| Süsteem loob või kustutab GENERAL_SERVICE lepingu, kus teenusepakkujaks on nimetatud müüja        | Nimetatud müüja, võrguoperaator                                                                         |
| Süsteem loob või kustutab GENERAL_SERVICE lepingu, kus teenusepakkujaks on võrguoperaator         | Võrguoperaator                                                                                          |
| GRID või BORDER_GRID lepingu muutmine/kustutamine                                                 | Aktiivne või tuleviku avatud tarnija, agregeerimise mõõtepunkti agregaator                              |
| GRID lepingu muutmine selliselt, et see mõjutab SUPPLY lepingut(uid)                              | Avatud tarnija(d), Mõõtepunkti haldur                                                                   |
| SUPPLY lepingu lisamine/muutmine/kustutamine                                                      | Mõõtepunkti haldur                                                                                      |
| SUPPLY lepingu lisamine/muutmine/kustutamine selliselt, et see mõjutab teist SUPPLY lepingut(uid) | Mõõtepunkti haldur, teine avatud tarnija                                                                |
| AGGREGATION lepingu lisamine/muutmine/kustutamine                                                 | Vastavalt ülemmõõtepunktis kattuvatele lepingutele: avatud tarnija, nimetatud müüja, mõõtepunkti haldur |

### Mõõteandmete reeglid

- Mõõteandmete laekumisel kontrollib Andmeladu, kas kõik edastatud andmed (ühes sõnumis võib olla mitme mõõtepunkti mitme perioodi andmed) on võimalik üks-ühele vastavatele adressaatidele edasi saata või mitte. Kui mitte, siis tükeldab Andmeladu andmed selliselt, et adressaatideni jõuaks ainult neile mõeldud andmed.
- Andmete levitamine sõltub otselt mõõtepunkti SUPPLY, BORDER_SUPPLY, GENERAL_SERVICE, AGGREGATION, lepingutest ja lepingute kehtivusaegade kattuvusest saadetud andmete perioodidega. Kui mõõteandmete sõnumis edastatud periood kattub mõne sellise lepinguga, siis lepingu teenusepakkujale levitatakse mõõteandmeid

### Võrguteenuse arve reeglid

- Võrguteenuse arve laekumisel kontrollib Andmeladu, kas kõik edastatud andmed on võimalik üks-ühele vastavatele adressaatidele edasi saata või mitte. Kui mitte, siis tükeldab Andmeladu andmed selliselt, et adressaatideni jõuaks ainult neile mõeldud andmed.
- Andmete levitamise adressaat saab olla vastavalt SUPPLY või GENERAL_SERVICE lepingule kas avatud tarnija või nimetatud müüja või mõlemad.

### Kliendi metaandmete reeglid

- Kliendi BILLING metaandmete uuendusi levitatakse nimetatud müüjale, kellel on hetkel kehtiv või oli viimase 12 kuu jooksul kehtinud GENERAL_SERVICE leping kliendiga (eeldusel, et andmeid ei muutnud nimetatud müüja ise)
- Kliendi nime uuendusi levitatakse aktiivsetele teenusepakkujatele

### Ligipääsuõiguste reeglid

- Ligipääsuõiguse subjektile toimub alati uue ligipääsuõiguse levitamine

### Kooskõlastusega lepingute muudatuste reeglid

> [!IMPORTANT]
> Lepingute kooskõlastuste levitamise funktsionaalsus on arenduses

- Kõik kooskõlastajad saavad kooskõlastuse teavitusi, kui:
  - Loodi uus kooskõlastus
  - Kooskõlastus tühistati
  - Kooskõlastus sai mõnelt kooskõlastajalt heakskiitva või tagasilükkava vastuse

## Andmeuuenduste skaneerimine

Erinevalt vanast Andmelaost, uus Andmeladu sõnumeid liidestuvatatele osapooltele ei saada vaid eeldab, et liidestuv süsteem kontrollib kas talle on uus sõnumeid. Selleks on loodud spetsiaalsed
uuenduste tõmbamise API liidesed.

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
- AGREEMENT_COORDINATION - kooskõlastusega lepingute muudatuste taotlused

> [!IMPORTANT]
> Lepingute kooskõlastuste funktsionaalsus on arenduses

Maksimaalne päritava perioodi pikkus on:

- mõõteandmed: 1 tund
- muud andmed: 24 tundi (sügisese kellakeeramise ajal on see erisus oluline, kuna lokaalne (mitte UTC) päev on 25h pikk)

Maksimaalne lubatud sõnumi ID-de vahemik (`idTo` miinus `idFrom`) on 10000

> [!TIP]
> Pikema ajaperioodi sõnumite pärimiseks on võimalik saata mitu erinevat päringut erinevate perioodide kohta. Nt esimene sõnum 02.01.2024-03.01.2024 perioodi ja teine 01.01.2024-02.01.2024 perioodi kohta.

> [!WARNING]
> Vanemaid kui 7 päeva andmeid pole võimalik tagantjärele lugeda.

### Muudatuse põhjus (reason)

Vastussõnumis on alati atribuut `reason`, mis kirjeldab muudatuse olemust. Muudatuse põhjused jagunevad kahte suurde gruppi: lihtväärtused ja liitväärtused.

#### Lihtväärtused

Lihtväärtused on olemas kõigil andmeobjekti tüüpidel, millel esineb elustükkel. Osadel andmeobjektidel võivad osad väärtused puududa. Nt pole võimalik mõõtepunkti kustutada või võrguarvet uuendada.

Lihtväärtused on:

- `CREATE` - andmeobjekt loodi
- `UPDATE` - andmeobjekt uuendati
- `DELETE` - andmeobjekt kustutati

#### Liitväärtused

Liitväärtused on kasutusel ainult lepingutega seotud andmete levitamise sõnumites, kuna ühe lepingu muudatus võib kaasa tuua mõne teise lepingu või lausa mitme lepingu muudatuse. Näiteks, kui SUPPLY lepingut muudetakse GRID lepingu muutmise tõttu.

Liitväärtused koosnevad alati järgmistest osadest: 

| Mis juhtus sõnumis oleva lepinguga | Sest | Muudatuse põhjustanud lepingu tüüp                               | Muudatuse põhjustanud lepingu tegevus |
|------------------------------------|------|------------------------------------------------------------------|---------------------------------------|
| CREATE, UPDATE või DELETE          | BC   | GRID, BORDER_GRID, SUPPLY, PORTFOLIO_SUPPLIER või NAMED_SUPPLIER | CREATE, UPDATE või DELETE             |

Täpne nimekiri kasutusel olevatest väärtustest on leitav Swagger teenuste kirjeldustest, kuid allpool on nimekiri mõnedest väärtustest

| Kategooria                | Kood                                | Kirjeldus                                                                                                                         |
|---------------------------|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| GRID impact               | CREATE_BC_GRID_CREATE               | Leping loodi, kuna loodi GRID leping                                                                                              |
|                           | UPDATE_BC_GRID_CREATE               | Lepingut muudeti, kuna loodi GRID leping                                                                                          |
|                           | DELETE_BC_GRID_CREATE               | Leping kustutati, kuna loodi GRID leping                                                                                          |
|                           | CREATE_BC_GRID_UPDATE               | Leping loodi, kuna GRID lepingut muudeti                                                                                          |
|                           | UPDATE_BC_GRID_UPDATE               | Lepingut muudeti, kuna GRID lepingut muudeti                                                                                      |
|                           | DELETE_BC_GRID_UPDATE               | Leping kustutati, kuna GRID lepingut muudeti                                                                                      |
|                           | DELETE_BC_GRID_DELETE               | Leping kustutati, kuna GRID leping kustutati                                                                                      |
| BORDER_GRID impact        | CREATE_BC_BORDER_GRID_CREATE        | Leping loodi, kuna BORDER_GRID                                                                                                    |
|                           | UPDATE_BC_BORDER_GRID_CREATE        | Lepingut muudeti, kuna BORDER_GRID                                                                                                |
|                           | DELETE_BC_BORDER_GRID_CREATE        | Leping kustutati, kuna BORDER_GRID                                                                                                |
|                           | CREATE_BC_BORDER_GRID_UPDATE        | Leping loodi, kuna BORDER_GRID lepingut muudeti                                                                                   |
|                           | UPDATE_BC_BORDER_GRID_UPDATE        | Lepingut muudeti, kuna BORDER_GRID lepingut muudeti                                                                               |
|                           | DELETE_BC_BORDER_GRID_UPDATE        | Leping kustutati, kuna BORDER_GRID lepingut muudeti                                                                               |
|                           | CREATE_BC_BORDER_GRID_DELETE        | Leping loodi, kuna BORDER_GRID leping kustutati                                                                                   |
|                           | UPDATE_BC_BORDER_GRID_DELETE        | Lepingut muudeti, kuna BORDER_GRID leping kustutati                                                                               |
|                           | DELETE_BC_BORDER_GRID_DELETE        | Leping kustutati, kuna BORDER_GRID leping kustutati                                                                               |
| SUPPLY impact             | CREATE_BC_SUPPLY_CREATE             | Leping loodi, kuna loodi SUPPLY leping                                                                                            |
|                           | UPDATE_BC_SUPPLY_CREATE             | Lepingut muudeti, kuna loodi SUPPLY leping                                                                                        |
|                           | DELETE_BC_SUPPLY_CREATE             | Leping kustutati, kuna loodi SUPPLY leping                                                                                        |
|                           | CREATE_BC_SUPPLY_UPDATE             | Leping loodi, kuna SUPPLY lepingut muudeti                                                                                        |
|                           | UPDATE_BC_SUPPLY_UPDATE             | Lepingut muudeti, kuna SUPPLY lepingut muudeti                                                                                    |
|                           | DELETE_BC_SUPPLY_UPDATE             | Leping kustutati, kuna SUPPLY lepingut muudeti                                                                                    |
|                           | CREATE_BC_SUPPLY_DELETE             | Leping loodi, kuna SUPPLY leping kustutati                                                                                        |
|                           | UPDATE_BC_SUPPLY_DELETE             | Lepingut muudeti, kuna SUPPLY leping kustutati                                                                                    |
|                           | DELETE_BC_SUPPLY_DELETE             | Leping kustutati, kuna SUPPLY leping kustutati                                                                                    |
|                           | CREATE_BC_AGREEMENT_COORDINATION    | Leping lisati, kuna mõni teine SUPPLY leping lisati või muudeti kooskõlastuse kaudu. Kasutatakse GENERAL_SERVICE lepingute puhul. |
|                           | UPDATE_BC_AGREEMENT_COORDINATION    | Lepingut muudeti, kuna mõni teine SUPPLY leping lisati või muudeti kooskõlastuse kaudu                                            |
|                           | DELETE_BC_AGREEMENT_COORDINATION    | Leping kustutati, kuna mõni teine SUPPLY leping lisati või muudeti kooskõlastuse kaudu                                            |
| PORTFOLIO_SUPPLIER impact | CREATE_BC_PORTFOLIO_SUPPLIER_CREATE | Leping loodi, kuna loodi PORTFOLIO_SUPPLIER leping                                                                                |
|                           | UPDATE_BC_PORTFOLIO_SUPPLIER_CREATE | Lepingut muudeti, kuna loodi PORTFOLIO_SUPPLIER leping                                                                            |
|                           | DELETE_BC_PORTFOLIO_SUPPLIER_CREATE | Leping kustutati, kuna loodi PORTFOLIO_SUPPLIER leping                                                                            |
|                           | CREATE_BC_PORTFOLIO_SUPPLIER_UPDATE | Leping loodi, kuna PORTFOLIO_SUPPLIER lepingut muudeti                                                                            |
|                           | UPDATE_BC_PORTFOLIO_SUPPLIER_UPDATE | Lepingut muudeti, kuna PORTFOLIO_SUPPLIER lepingut muudeti                                                                        |
|                           | DELETE_BC_PORTFOLIO_SUPPLIER_UPDATE | Leping kustutati, kuna PORTFOLIO_SUPPLIER lepingut muudeti                                                                        |
|                           | CREATE_BC_PORTFOLIO_SUPPLIER_DELETE | Leping loodi, kuna PORTFOLIO_SUPPLIER leping kustutati                                                                            |
|                           | UPDATE_BC_PORTFOLIO_SUPPLIER_DELETE | Lepingut muudeti, kuna PORTFOLIO_SUPPLIER leping kustutati                                                                        |
|                           | DELETE_BC_PORTFOLIO_SUPPLIER_DELETE | Leping kustutati, kuna PORTFOLIO_SUPPLIER leping kustutati                                                                        |
| NAMED_SUPPLIER impact     | CREATE_BC_NAMED_SUPPLIER_CREATE     | Leping loodi, kuna loodi NAMED_SUPPLIER leping                                                                                    |
|                           | UPDATE_BC_NAMED_SUPPLIER_CREATE     | Lepingut muudeti, kuna loodi NAMED_SUPPLIER leping                                                                                |
|                           | DELETE_BC_NAMED_SUPPLIER_CREATE     | Leping kustutati, kuna loodi NAMED_SUPPLIER leping                                                                                |
|                           | CREATE_BC_NAMED_SUPPLIER_UPDATE     | Leping loodi, kuna NAMED_SUPPLIER lepingut muudeti                                                                                |
|                           | UPDATE_BC_NAMED_SUPPLIER_UPDATE     | Lepingut muudeti, kuna NAMED_SUPPLIER lepingut muudeti                                                                            |
|                           | DELETE_BC_NAMED_SUPPLIER_UPDATE     | Leping kustutati, kuna NAMED_SUPPLIER lepingut muudeti                                                                            |
|                           | CREATE_BC_NAMED_SUPPLIER_DELETE     | Leping loodi, kuna NAMED_SUPPLIER leping kustutati                                                                                |
|                           | UPDATE_BC_NAMED_SUPPLIER_DELETE     | Lepingut muudeti, kuna NAMED_SUPPLIER leping kustutati                                                                            |
|                           | DELETE_BC_NAMED_SUPPLIER_DELETE     | Leping kustutati, kuna NAMED_SUPPLIER leping kustutati                                                                            |

## Sõnumid

### Versioonid

Andmete levitamise teenuseid versioonitakse. Kui päringu või vastuse struktuuri muudetakse, muutub teenuse uus versioon kättesaadavaks.

Oluline on mõista, et andmeobjekti peamise teenuse versioon võib erineda andmete levitamise teenuse versioonist. Näiteks kui lepingu otsingu teenuse päringu struktuuri uuendatakse, kuid vastus jääb samaks, siis pole andmete levitamise teenuse värskendamist vaja. Kuid kui näiteks lepingu andmeolemi struktuuri muudetakse, põhjustab see ka andmete levitamise teenuse versioonimuutuse.

Uurige Swaggeris peamiste teenuste ja andmete levitamise teenuste struktuure, et leida sobivad vasted.

### Uued teenused

> [!IMPORTANT]
> Lepingute kooskõlastuste levitamise teenused on arenduses

Mõiste "uus" viitab asjaolule, et need teenused loodi pärast "vana" teenust. Need teenused on andmeobjekti spetsiifilised ja tagastavad andmeobjekti uue versiooni (V2 ja uuem).

| Sõnum                                                   | Eesmärk                                                     |
|---------------------------------------------------------|-------------------------------------------------------------|
| `GET /api/v1/data-distributions/agreement`              | Leia lepingute muudatuste teateid                           |
| `GET /api/v1/data-distributions/agreement-coordination` | Leia kooskõlastusega lepingute muudatuste taotluste teateid |

Uued teenused on andmeobjekti tüübi spetsiifilised. Seega on sõnumite andmestruktuurid eksplitsiitselt kirjeldatud Swaggeris

### Vanad teenused

Mõiste "vana" viitab asjaolule, et see teenus loodi koos Andmelao esmase tarnimisega. See on ühine teenus kõigi andmeolemite tüüpide (välja arvatud kooskõlastusega lepingute muudatuste taotlused) jaoks.

See teenus tagastab andmeobjektide V1 versiooni.

| Sõnum                                   | Eesmärk                                            |
|-----------------------------------------|----------------------------------------------------|
| `POST /api/v1/data-distribution/search` | Leia kõigi andmeolemite tüüpide muudatuste teateid |

#### Päring

Atribuudid:

| Atribuut        | Tüüp              | Kohustuslik?                         | Märkused                                                                                            |
|-----------------|-------------------|--------------------------------------|-----------------------------------------------------------------------------------------------------|
| createdTimeFrom | string($datetime) | jah, kui idFrom/idTo puuduvad        | Sõnumi loomisaja algus                                                                              |
| createdTimeTo   | string($datetime) | jah, if idFrom/idTo  puuduvad        | Sõnumi loomisajal lõpp                                                                              |
| idFrom          | int               | jah, kui createdTimeFrom/To puuduvad | Sõnumi ID algus                                                                                     |
| idTo            | int               | jah, kui createdTimeFrom/To puuduvad | Sõnumi ID lõpp                                                                                      |
| resourceType    | int               | jah                                  | Üks järgnevatest: METERING_POINT, METERING_DATA, NETWORK_BILL, CUSTOMER_DATA, AGREEMENT, PERMISSION |
| pagination      | int               | jah                                  | Standardne pagineerimise sektsioon                                                                  |

#### Vastus

Iga andmete levitamise vastussõnum koosneb ühis- ja andmetüübi spetsiifilistest atribuutidest:

| Atribuut             | Tüüp     | Alati sõnumis? | Märkused                                                                                             |
|----------------------|----------|----------------|------------------------------------------------------------------------------------------------------|
| id                   | int      | jah            | Unikaalne sõnumi ID, mis on ajas kasvav                                                              |
| createdTime          | datetime | jah            | Andmete levitamise sõnumi (mitte selle sõnumi, mis andmete levitamise põhjustas) loomise aeg         |
| resourceType         | string   | jah            | Andmeobjekti tüüp                                                                                    |
| reason               | string   | jah            | Väärtused on kirjeldatud peatükis [Muudatuse põhjus (reason)](#muudatuse-põhjus-reason)              |
| hasContent           | bool     | jah            | Kui "true", siis on positsioonil "content" sisu. Kui "false", siis sisu puudub (tehnilisel põhjusel) |
| content              | string   | jah            | Sõnumi sisu vastavalt andmetüübile (vt kirjeldus allpool)                                            |
| contentMissingReason | string   | ei             | Inimloetav põhjendus, miks atribuut "content" on tühi.                                               |
| pagination           | object   | jah            | Standardsed pagineerimise elemendid                                                                  |

Võimalikud `contentMissingReason` väärtused:

* "File not found at the specified path"
* "Unexpected error while getting file from MinIO"
* "The path value is null"

Näide vastussõnumist:

```json
{
  "dataDistributions": [
    {
      "id": 4656,
      "createdTime": "2024-05-23T10:08:44.320005900Z",
      "resourceType": "AGREEMENT",
      "reason": "CREATE",
      "hasContent": true,
      "content": "[{\"meterEic\":\"38ZGO-1000001U-D\",\"agreementType\":\"GENERAL_SERVICE\",\"preliminaryTerminationFee\":false,\"commodityType\":\"ELECTRICITY\",\"validFrom\":\"2024-05-22T21:00Z\",\"validTo\":\"2024-05-31T21:00Z\"}]"
    },
    {
      "id": 4660,
      "createdTime": "2024-05-23T10:10:13.682197100Z",
      "resourceType": "AGREEMENT",
      "reason": "CREATE",
      "hasContent": true,
      "content": "[{\"agreementId\":\"einar-2024-05-23T13:08:42.936268+03:00-EST\",\"meterEic\":\"38ZGO-1000001U-D\",\"agreementType\":\"SUPPLY\",\"preliminaryTerminationFee\":true,\"commodityType\":\"ELECTRICITY\",\"validFrom\":\"2024-05-22T21:00Z\",\"validTo\":\"2024-06-30T21:00Z\",\"serviceProviderEic\":\"38X-EIN-OS-----J\",\"customerEic\":\"38X-AVP-ZW6700C6\"}]"
    },
    {
      "id": 4661,
      "createdTime": "2024-05-23T10:10:13.682552100Z",
      "resourceType": "METERING_POINT",
      "reason": "",
      "content": "",
      "hasContent": false,
      "contentMissingReason": "File not found at the specified path"
    }
  ],
  "pagination": {
    "page": 0,
    "totalPages": 1
  }
}

```

#### Andmetüübid

##### Leping

###### Atribuudid

Süsteem kasutab sama struktuuri ja atribuute, nagu `POST /api/{version}/agreement` teenuse vastussõnumis, kuid esinevad järgmised erisused:

- `agreementId`, `meterEic` ja `validTo` võivad puududa, kui need puuduvad algses lepingu sõnumis.
- `serviceProviderEic` ja `customerEic` puuduvad, kui see informatsioon ei kuulu vastavalt ärireeglitele avalikustamisele.

###### Näited

```json
{
  "meterEic": "38ZGO-10000074-U",
  "agreementType": "GENERAL_SERVICE",
  "preliminaryTerminationFee": false,
  "commodityType": "ELECTRICITY",
  "validFrom": "2024-11-12T22:00Z",
  "validTo": "2024-11-30T22:00Z",
  "serviceProviderEic": "38X-EIN-GO-----0",
  "customerEic": "38X-AVP-ZW6700C6"
}
```

```json
{
  "agreementType": "JOINT_INVOICE",
  "preliminaryTerminationFee": false,
  "commodityType": "ELECTRICITY",
  "validFrom": "2024-05-31T21:00Z",
  "serviceProviderEic": "38X-EIN-NS-----R",
  "customerEic": "38X-EIN-ALL----B"
}
```

##### Mõõtepunkt

Süsteem kasutab sama struktuuri ja atribuute, nagu `PUT /api/{version}/meter` teenuses.

###### Atribuudid

###### Näited

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

##### Mõõteandmed

###### Atribuudid

Mõõteandmete levitamise sõnumi struktuur on täpselt sama, nagu `POST /meter-data` sõnumil.

###### Näited

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

##### Võrguteenuse arve

###### Atribuudid

Võrguteenuse arve levitamise sõnumi struktuur on täpselt sama, nagu `POST /network-bill` sõnumil.

###### Näited

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

##### Kliendi metaandmed

###### Atribuudid

Kliendi metaandmete levitamise sõnum koosneb järgmistest sektsioonidest:

- `customerType` - sama nagu teenuse `api/{version}/customer/search` vastussõnumis
- `customerMetadata` - sama nagu teenuse `api/{version}/customer/search` vastussõnumis
- `customerEic` - kliendi EIC kood

###### Näited

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
      "metadataValue": "Mari",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "LAST_NAME",
      "metadataValue": "Maasikas",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "PHONE",
      "metadataValue": "55667788",
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
      "metadataValue": "mari.maasikas@gmail.com",
      "validFrom": "2024-05-27T12:40:14.657518Z"
    },
    {
      "metadataType": "MOBILE_PHONE",
      "metadataValue": "+37255667788",
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

##### Ligipääsuõigused

###### Atribuudid

| Atribuut            | Tüüp     | Alati väljundis? | Kirjeldus                                                                                                                           |
|---------------------|----------|------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| mandateCustomerEic  | string   | JAH              | 16-kohaline turuosalise EIC kood                                                                                                    |
| mandateCustomerType | string   | JAH              | Üks järgnevatest: PRIVATE, LEGAL                                                                                                    |
| meteringPointEic    | string   | JAH              | 16-kohaline mõõtepunkti EIC kood                                                                                                    |
| ownerCustomerEic    | string   | JAH              | 16-kohaline kliendi EIC kood                                                                                                        |
| ownerCustomerType   | string   | JAH              | Üks järgnevatest: PRIVATE, LEGAL                                                                                                    |
| participantRoleType | string   | JAH              | Avatud tarnija puhul alati OPEN_SUPPLIER; agregaatori puhul alati AGGREGATOR, energiateenuse puhul alati ENERGY_SERVICE_PROVIDER    |
| permissionType      | string   | JAH              | Alati ACCESS                                                                                                                        |
| purpose             | string   | JAH              | Avatud tarnija puhul alati ENERGY_SUPPLY_OFFER; agregaatori puhul alati AGGREGATION_OFFER; energiateenuse puhul erinevad väärtused  |
| status              | string   | JAH              | Alati APPROVED                                                                                                                      |
| subjectPeriodFrom   | datetime | JAH              | Ajaperioodi algus, mille andmetele ligipääsuõigus ligipääsu annab                                                                   |
| subjectPeriodTo     | datetime | JAH              | Ajaperioodi algus, mille andmetele ligipääsuõigus ligipääsu annab                                                                   |
| validFrom           | datetime | JAH              | Ligipääsuõiguse kehtivuse algus                                                                                                     |
| validTo             | datetime | EI               | Ligipääsuõiguse kehtivuse lõpp                                                                                                      |

###### Näited

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
