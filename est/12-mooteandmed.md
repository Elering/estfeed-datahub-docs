# Mõõteandmed

## Sisukord

<!-- TOC -->
* [Mõõteandmed](#mõõteandmed)
  * [Sisukord](#sisukord)
  * [Sissejuhatus](#sissejuhatus)
  * [Mõõteandmete edastamine](#mõõteandmete-edastamine)
    * [Mõõteandmete edastamine veebiliidese kaudu](#mõõteandmete-edastamine-veebiliidese-kaudu)
    * [Masinliidese sõnumid](#masinliidese-sõnumid)
      * [Sõnumid](#sõnumid)
      * [Sõnumite reeglid](#sõnumite-reeglid)
  * [Mõõteandmete päringud](#mõõteandmete-päringud)
    * [legalConsent](#legalconsent)
    * [Aja tüüp](#aja-tüüp)
    * [Mõõteandmete otsimine veebiliidese kaudu](#mõõteandmete-otsimine-veebiliidese-kaudu)
    * [Masinliidese sõnumid](#masinliidese-sõnumid-1)
      * [Sõnumid](#sõnumid-1)
<!-- TOC -->

## Sissejuhatus

Mõõteandmed on konkreetse mõõtepunktiga seotud prognoositud või mõõdetud aktiivenergia tarbimise andmed teatud ajaperioodi kohta. Mõõteandmed on arveldamise aluseks ja neid esitavad mõõtepunkti haldurid ning tarbivad teised turuosalised (peamiselt avatud tarnijad).

## Mõõteandmete edastamine

Mõõtepunkti haldur tagab tema mõõtepunktide aktiivenergia koguse kindlaksmääramise ning esitab Andmelattu kahesuunalised tunnipõhised aktiivenergia koguste mõõteandmed.

Agregaator edastab tarbimise juhtimise energia kogused.

Mõõtepunkti haldurid edastavad mõõtepunktide lõikes mõõteandmed järgmistel tingimustel:

1. nende mõõtepunktide kohta, kus mõõtmine toimub kauglugemise teel, edastatakse Andmelattu esialgsed mõõteandmed igal tööpäeval kella 10.00-ks;
2. kalendrikuu lõplikud mõõteandmed mõõtepunktides, kus mõõtmine toimub kauglugemise teel, edastatakse  Andmelattu iga järgneva kuu 5. kuupäevaks;

Võrgu- ja liinikao koguseid arvutab Andmeladu.

Võrguettevõtja on tüüpkoormusgraafikute haldaja ja vastutab tunnipõhiste koguste edastamise eest Andmelattu.

Võrguettevõtja ja liinivaldaja saab mõõteandmed edastada Andmelattu nii veebiliidese kaudu masslaadimisega kui ka automaatse andmevahetuse sõnumiga.

Mõõteandmete edastamiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Mõõtepunkti haldur saadab uue või muutunud mõõteandmete sõnumi kasutades teenust `meter-data`.
- Kuivõrd mõõteandmete töötlemine toimub Andmelaos asünkroonselt, siis esmalt annab Andmeladu kiire vastuse, kas sõnum õnnestus kätte saada või mitte.
- Seejärel paneb Andmeladu sõnumi töötluse järjekorda.
- Mõõtepunkti haldur kontrollib andmete töötluse tulemust, kasutades teenust `meter-data/status`(sõnumi positsioonil `originalDocumentIdentification` tuleb edastada eelnevalt edastatud mõõteandmete sõnumi `header`-is olnud samanimelise atribuudi väärtus. UUID väärtust ei tohi taaskasutada). Võimalikud tulemused on:
  - `PROCESSING` - töötlus ei ole veel lõppenud
  - `SUCCESSFUL` - töötlus lõppes vigadeta
  - `ERROR` - töötlus lõppes vigadega
  - `PARTIALLY_SUCCESSFUL` - töötlus lõppes osaliselt vigadega (nt sõnumis olid mitme mõõtepunkti mõõteandmed ja ühe mõõtepunkti andmete lisamine õnnestus, aga teise oma mitte)
- Kui sõnumi töötlemine õnnestub vigadeta, siis andmed lisatakse või muudetakse andmebaasis ning Andmeladu teeb mõõteandmete lisandumise või muutumise kättesaadavaks avatud tarnijatele läbi `data-distribution/search` teenuse. Loe täpsemalt peatükist [Andmete levitamine](30-andmete-levitamine.md).
- Kui sõnumi töötlemisel tekivad vead, siis Andmeladu koostab vearaporti ja teeb selle kättesaadavaks mõõtepunkti haldurile teenuse `meter-data/status` vastuses.
- Mõõtepunkti haldur loeb talle adresseeritud vearaportit ning lahendab selle vastavalt oma sisemisele äriloogikale.

> [!WARNING]
> **NB! Andmeladu edastab võrguettevõtjate poolt sisestatud mõõteandmed muutmata kujul. Andmeladu ei kontrolli mõõteandmete sisu**

> [!NOTE]
> Tasub teada, et eksisteerib üliväike, kuid teoorias siiski võimalik olukord, kus Andmeladu võtab mõõteandmete sõnumi vastu ja vastab "protsessimine alustatud" vastusega, kuid tegelikkuses jääb sõnum töötlemata ja selle kohta ei looda ka ´meter_data_status´ kirjet.
> Mõõtepunkti haldur peaks pidama järge, mis igast mõõteandmete sõnumist on saanud ja kas töötlus lõppes mingi tulemusega. Kui mõnele mõõteandmete sõnumile ei tekigi tõpptulemust, siis tuleb eeldada, et Andmelaos tekkis mõõteandmete töötlemisel ootamatu probleem (nt rakenduse ootamatu sulgumine) ja edastada mõõteandmed uuesti.
> Tulemuste jälgimiseks on erinevaid võimalusi. Nt pärida staatust ükshaaval `originalDocumentIdentification` alusel (juhul, kui andmemahud on väikesed) või skanneerida `SUCCESSFUL` ja `ERROR` staatuseid ja pidada sisemiselt järge, millised sõnumid on lõppolekusse jõudnud

### Mõõteandmete edastamine veebiliidese kaudu

Mõõteandmete edastamiseks veebiliidese kaudu tuleb navigeerida "Metering data" lehele.

Mõõteandmete mugavamaks edastamiseks on võimalik alla laadida template. Template koostamiseks tuleks valida mõõteandmete resolutsioon ning ajavahemik, selle põhjal koostatakse eeltäidetud template. Tähelepanu tuleks pöörata valitud ajavahemikule - valitud kellaajad peavad vastama mõõteandmete resolutsioonile.

![Mõõteandmete template genereerimine](../images/opp-ui/metering-data/metering-data-template1.png)

![Template seadistamine](../images/opp-ui/metering-data/metering-data-template2.png)

Mõõteandmete importimiseks tuleks vajutada "Metering data" lehel nuppu "Import". Seejärel on võimalik võimalik lisada mõõteandmete fail. 

![Mõõteandmete edastamine](../images/opp-ui/metering-data/metering-data-import.png)

Kui faili on juhtunud mõni viga annab süsteem sellest teada.
1. Mõõtepunktide andmed võivad olla lisatud ka mitmele MS Excel faili lehele, seetõttu annab süsteem kasutajatele teada, millisel lehel probleem on.
2. Lisaks on võimalik näha vigase rea numbrit.
3. Probleemi kirjeldus aitab mõista probleemi sisu.
4. Kui probleem on leitud ja fail parandatud peaks vajutama "Cancel" ning importimise protsessi kordama.

![Error mõõteandmete edastamisel](../images/opp-ui/metering-data/metering-data-error.png)

### Masinliidese sõnumid

Uues Andmelaos on "pos" ehk "positsiooni" atribuut eemaldatud. Mõõteandmete edastaja peab sõnumis defineerima perioodi alguse (pS) ja resolutsiooni (r) ehk andmete mõõtmise tiheduse:

```json
"periods": [
  {
    "r": "PT1H",
    "aI": [
      {
        "pS": "2023-09-04T12:00:00.000Z",
        "inQty": {
          "rTime": "2023-09-04T12:48:13.368Z",
          "rType": "E",
          "kwh": 0
        },
        "outQty": {
          "rTime": "2023-09-04T12:48:13.368Z",
          "rType": "M",
          "kwh": 5
        }
      }
    ]
  }
]
```

API teenuses kasutatavate lühendite selgitused:

* r - resolutsioon
* aI - Account Interval ehk ühe mõõtetulemuse intervall
* pS - Period Start ehk perioodi algus
* inQty - IN ehk siseneva energia mõõtetulemus
* outQty - OUT ehk väljuva energia mõõtetulemus
* rTime - Reading Time ehk mõõtmise aeg
* rType - Reading Type ehk mõõtmise tüüp (E - estimeeritud, M - mõõdetud)

Andmeladu ei valideeri, et iga 1 tunni või 15 minuti vahemik oleks mõõteandmetega täidetud. 

> [!NOTE] 
> Andmete resolutsioon on Andmelao poolt jäigalt fikseeritud - nii elektri kui gaasi puhul on resolutsiooniks 1 tund. 2024 aastal läheb elekter üle resolutsioonile 15 minutit.
> 
> Gaasi puhul on lubatud edastada ka päeva andmeid. Sellisel juhul tuleb päeva mõõteandmed lisada enda poolt sobivasse gaasipäeva tundi.

#### Sõnumid

| Sõnum                                     | Eesmärk                                                              |
|-------------------------------------------|----------------------------------------------------------------------|
| `POST /api/{version}/meter-data`          | Mõõteandmete lisamine                                                |
| `POST /api/{version}/meter-data/status`   | Mõõteandmete sõnumi töötlemise staatuse päring                       |
| `POST /api/{version}/meter-data/import`   | Mõõteandmete masslaadimine templiidi abil                            |
| `POST /api/{version}/template/meter-data` | Mõõteandmete masslaadimine templiidi genereerimine ja alla laadimine |

#### Sõnumite reeglid

- Resolutsiooni väärtus peab vastama antud ajaperioodil rakendatud globaalse resolutsiooniga. Nt, kui kogu turg läheb kuupäeval X üle 15min resolutsioonile, siis mõõteandmetele alates X kuupäevast peab sõnumis olema resolutsiooni väärtuseks 15min
- Perioodi ajaperioodi väärtus peab olema vastavuses resolutsiooniga. Näiteks:
  - kui resolutsioon on 1 tund, siis perioodi alguse kellaaeg peab olema täistund (hh:00);
  - kui resolutsioon on 15 minutit, siis perioodi alguse kellaaeg peab olema veerandtund (hh:00, hh:15, hh:30, hh:45).
- Elektri mõõtekogused esitatakse alati kWh-des täpsusega kuni 3 kohta peale koma.
- Gaasi mõõtekogused esitatakse nii kWh-des kui ka kuupmeetrites täpsusega 3 kohta peale koma.
- Mõõteandmete suund esitatakse alati mõõtva mõõtepunkti halduri poolt vaadatuna:
  - in – võrku sisenev energia (tootmine);
  - out – võrgust väljuv energia (tarbimine).
- Siseneva ja väljuva energia koguseid võib edastada ka eraldi sõnumitega.
- Mõõteandmeid on lubatud korrigeerida tagasiulatuvalt kuni 12 kuud.
- Teenuses `import` tuleb kasutada sama templiiti, mida väljastab teenus `export` või `template/meter-data`

## Mõõteandmete päringud

Mõõteandmete edastamiseks on loodud vastavad Andmelao teenused. Andmetele ligipääs on piiratud. Reeglid on  kirjeldatud dokumendis [Rollipõhised ligipääsuõigused](03.01-rollipohised-ligipaasuoigused.md)

Mõõteandmete päringute teostamiseks on järgmised võimalused:

- Avatud tarnija, nimetatud müüja ja portfelliteenuse pakkuja skaneerib mõõteandmete muudatusi kasutades teenust `data-distribution/search`
- Õigustatud kasutaja pärib mõõteandmed kasutades teenust `search`

### legalConsent

Nii füüsiline kui ka juriidiline isik saab läbi kliendiportaali anda andmetele ligipääsuõiguse, nagu kirjeldatud peatükis [Rollipõhised ligipääsuõigused](03.01-rollipohised-ligipaasuoigused.md)

Kui füüsiliste isikute ligipääsuõigus on oma olemuselt absoluutne, siis juriidiliste isikute puhul on võimalik ka alternatiivne töövoog, kus juriidiline isik on andnud ligipääsuõiguse Andmelao ja kliendiportaali väliselt, kuid kirjalikus taasesitamist võimaldavad vormis otse avatud tarnijale.

Sellise olukorra olemasolu saab avatud tarnija `search` teenuses kinnitada, lisades päringusse `"legalConsent": true`. Sellisel juhul on avatud tarnijal võimalik pärida mistahes mõõtepunkti mõõteandmeid eeldusel, et mõõtepunkti võrgulepingu kliendiks on juriidiline isik või organisatsioon.

> [!CAUTION] 
> `"legalConsent": true` kasutamine on lubatud vaid kliendi volituse olemasolul ja selle õiguspärast kasutamist monitooritakse

### Aja tüüp

Võrreldes vana süsteemiga on kadunud `billingSequence` kontseptsioon. Selle asemel edastab mõõtepunkti haldur koos mõõteandmetega mõõtmise aja (ing. **reading time**). 
Mõõteandmete vastuvõtmisel lisab Andmeladu andmetele salvestamise aja (ing. **snapshot time**).

Kuna mõlemad ajaväärtused on Andmelao süsteemis olemas, siis võimaldab Andmeladu mõõteandmeid otsida nende ajaväärtuste alusel. Näited:

1. Avatud tarnija on huvitatud viimasest teadaolevast mõõteandmete seisust mõõtepunktis X. Selleks on tal 2 võimalust:
  * Jätab atrbibuudid `observationTimeType` ja `observationTime` sõnumisse lisamata
  * väärtustab ta sõnumis atribuudid:
  * `observationTimeType` = `SNAPSHOT_TIME`.
  * `observationTime` = hetke kuupäev ja kellaaeg
2. Avatud tarnija on huvitatud mõõteandmete seisust mõõtepunktis X kuupäeva 01.01.2024 00:00 seisuga. Selleks väärtustab ta sõnumis atribuudid:
  * `observationTimeType` = `SNAPSHOT_TIME`
  * `observationTime` = `2024-01-01T00:00:00+02:00`
3. Avatud tarnija on huvitatud mõõteandmete seisust mõõtepunktis X, kus mõõtmise aeg ei ole suurem kui 31.12.2023 23:59. Selleks väärtustab ta sõnumis atribuudid:
  * `observationTimeType` = `READING_TIME`
  * `observationTime` = `2023-12-31T23:59:59+02:00`

> [!WARNING]
> Hetkel pole toetatud `observationTimeType` = `SNAPSHOT_TIME` ja `observationTime` koos kasutamine (näide nr 2). Vastav arendus on defineeritud ja hetkeseisuga planeeritud aastasse 2024.

### Mõõteandmete otsimine veebiliidese kaudu

Mõõteandmeid saab otsida navigeerides "Metering data" lehele. Selleks tuleb sisestada otsitava mõõtepunkti EIC kood ning otsinguperioodi algkuupäev. Soovi korral võib määrata ka lõppkuupäeva.

![Mõõteandmete otsimine](../images/opp-ui/metering-data/metering-data-search.png)

### Masinliidese sõnumid

#### Sõnumid

| Sõnum                                   | Eesmärk                   |
|-----------------------------------------|---------------------------|
| `POST /api/{version}/meter-data/search` | Mõõteandmete otsing       |
| `POST /api/{version}/meter-data/export` | Mõõteandmete eksportimine |
