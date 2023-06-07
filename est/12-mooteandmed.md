# Mõõteandmed

## Sisukord

- [Mõõteandmed](#mõõteandmed)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Mõõteandmete edastamine](#mõõteandmete-edastamine)
    - [Mõõteandmete edastamine veebiliidese kaudu](#mõõteandmete-edastamine-veebiliidese-kaudu)
    - [Masinliidese sõnumid](#masinliidese-sõnumid)
      - [Sõnumid](#sõnumid)
      - [Sõnumite reeglid](#sõnumite-reeglid)
  - [Mõõteandmete päringud](#mõõteandmete-päringud)
    - [Masinliidese sõnumid](#masinliidese-sõnumid-1)
      - [Sõnumid](#sõnumid-1)
      - [Sõnumite reeglid](#sõnumite-reeglid-1)

## Sissejuhatus

Mõõteandmed on konkreetse mõõtepunktiga seotud prognoositud või mõõdetud aktiivenergia tarbimise andmed teatud ajaperioodi kohta. Mõõteandmed on arveldamise aluseks ja neid esitavad mõõtepunkti haldurid ning tarbivad teised turuosalised (peamiselt avatud tarnijad).

## Mõõteandmete edastamine

Mõõtepunkti haldur tagab tema mõõtepunktide aktiivenergia koguse kindlaksmääramise ning esitab Andmelattu kahesuunalised tunnipõhised aktiivenergia koguste mõõteandmed.

Agregaator edastab vähendatud tarbimise energia kogused.

Mõõtepunkti haldurid edastavad mõõtepunktide lõikes mõõteandmed järgmistel tingimustel:

1. nende mõõtepunktide kohta, kus mõõtmine toimub kauglugemise teel, edastatakse Andmelattu esialgsed mõõteandmed igal tööpäeval kella 10.00-ks;
2. kalendrikuu lõplikud mõõteandmed mõõtepunktides, kus mõõtmine toimub kauglugemise teel, edastatakse  Andmelattu iga järgneva kuu 5. kuupäevaks;

Võrgu- ja liinikao koguseid arvutab Andmeladu.

Võrguettevõtja on tüüpkoormusgraafikute haldaja ja vastutab tunnipõhiste koguste edastamise eest Andmelattu.

Võrguettevõtja ja liinivaldaja saab mõõteandmed edastada Andmelattu nii veebiliidese kaudu masslaadimisega kui ka automaatse andmevahetuse sõnumiga.

Mõõteandmete edastamiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Mõõtepunkti haldur saadab uue või muutunud mõõteandmete sõnumi kasutades teenust `meter-data`
- Kuivõrd mõõteandmete töötlemine toimub Andmelaos asünkroonselt, siis esmalt annab Andmeladu kiire vastuse, kas sõnum õnnestus kätte saada või mitte
- Seejärel paneb Andmeladu sõnumi töötluse järjekorda
- Soovi korral kontrollib mõõtepunkti haldur asünkroonse töötluse olekut kasutades teenust `meter-data/status`
- Kui sõnumi töötlemine õnnestub vigadeta, siis rohkem teavitusi Andmeladu mõõtepunkti haldurile ei edasta. Andmed lisatakse või muudetakse andmebaasis ning Andmeladu teeb mõõteandmete lisandumise või muutumise kättesaadavaks avatud tarnijatele läbi `changes` teenuse. Loe täpsemalt peatükist [Andmete levitamine](30-andmete-levitamine.md).
- Kui sõnumi töötlemisel tekivad vead, siis Andmeladu koostab vearaporti ja teeb selle kättesaadavaks mõõtepunkti haldurile läbi `changes` teenuse. Loe täpsemalt peatükist [Andmete levitamine](30-andmete-levitamine.md).
- Mõõtepunkti haldur loeb talle adresseeritud vearaportit ning lahendab selle vastavalt oma sisemisele äriloogikale

> **Warning**
>
> **NB! Andmeladu edastab võrguettevõtjate poolt sisestatud mõõteandmed muutmata kujul. Andmeladu ei kontrolli mõõteandmete sisu**

### Mõõteandmete edastamine veebiliidese kaudu

> **Note**
> Dokumentatsioon on loomisel

### Masinliidese sõnumid

Mõõteandmete edastamise puhul on oluline aru saada perioodi, resolutsiooni ja positsiooni tähendustest ja omavahelistest seostest:

- **Resolutsioon** määrab mõõteandmete tiheduse: 1 päev, 1 tund või 15 minutit
- **Periood** defineerib ajavahemiku, mille kohta mõõteandmeid edastatakse
- **Positsioon** defineerib pesa ehk sloti, mille kohta mõõteandmed käivad

Näiteks kui periood on 3 tundi ja resolutsioon 1 tund, siis tähendab see seda, et andmete edastaja soovib meile saata kolme pesa andmed. Seega eeldab süsteem sõnumis kolme sektsiooni, kus igas sektsioonis on mõõteandmed ja sektsioonide positsioonide väärtused on vastavalt 1, 2 ja 3.

Tehniliselt on küll lubatud ka sellised sõnumid, kus edastatud pesad ei kata ära kogu esitatud perioodi. Näiteks periood on 3 tundi, resolutsioon 1 tund, aga positsioone on kõigest 2. Sellisel juhul määrab süsteem edastatud positsioonide mõõteandmed perioodi algusesse - positsioon 1 andmed esimesse tundi ja positsioon 2 andmed teise tundi. Kolmas tund jääb täitmata.

#### Sõnumid

|Sõnum|Eesmärk|
|-----|-------|
|`POST /api/{version}/meter-data`|Võimaldab lisada mõõteandmeid|
|`PUT /api/{version}/meter-data`|Võimaldab muuta mõõteandmeid|
|`POST /api/{version}/meter-data/status`|Võimaldab kontrollida asünkroonse töötluse olekut|
|`POST /api/{version}/meter-data/changes`|Võimaldab skaneerida mõõteandmete töötluse vearaporteid|

Sõnumite struktuuride ja validatsioonide kirjeldused on leitavad [Swagger](https://test-datahub.elering.ee/swagger-ui/index.html) keskkonnast.

> **Note**
> Sõnumite näidiste kogumik on loomisel

#### Sõnumite reeglid

- Mõõteandmete ja mõõtepunkti resolutsiooni seose kohta loe täpsemalt dokumendist [Mõõtepunktid](04-mootepunktid.md#sõnumite-reeglid)
- Perioodi ajaperioodi väärtus peab olema vastavuses resolutsiooniga. Näiteks:
  - kui resolutsioon on 1 tund, siis perioodi alguse kellaaeg peab olema täistund (hh:00)
  - kui resolutsioon on 15 minutit, siis perioodi alguse kellaaeg peab olema veerandtund (hh:00, hh:15, hh:30, hh:45)
- perioodi algus esitatakse vasakjoondusega ja perioodi lõpp paremjoondusega. Näiteks 1 tunni mõõteandmete periood esitatakse kujul hh:00 - hh+1:00 (03:00-04:00)
- Mõõtekogused esitatakse alati kWh-des täpsusega 3 kohta peale koma.
- Mõõteandmete suund esitatakse alati mõõtva mõõtepunkti halduri poolt vaadatuna:
  - in – võrku sisenev energia (tootmine);
  - out – võrgust väljuv energia (tarbimine).
- Siseneva ja väljuva energia koguseid võib edastada ka eraldi sõnumitega.
- Mõõteandmeid korrigeeritakse tagasiulatuvalt kuni 12 kuud.

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)

## Mõõteandmete päringud

Mõõteandmete edastamiseks on loodud vastavad Andmelao teenused. Andmetele ligipääs on piiratud. Reeglid on  kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)

Mõõteandmete päringute teostamiseks on järgmised võimalused:

- Avatud tarnija skaneerib mõõteandmete muudatusi kasutades teenust `changes`
- Õigustatud kasutaja pärib mõõteandmed kasutades teenust `search`

### Masinliidese sõnumid

#### Sõnumid

|Sõnum|Eesmärk|
|-----|-------|
|`POST /api/{version}/meter-data/search`|Võimaldab otsida mõõteandmeid|
|`POST /api/{version}/meter-data/changes`|Võimaldab skaneerida mõõteandmete muudatusi|

Sõnumite struktuuride ja validatsioonide kirjeldused on leitavad [Swagger](https://test-datahub.elering.ee/swagger-ui/index.html) keskkonnast.

> **Note**
> Sõnumite näidiste kogumik on loomisel

#### Sõnumite reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)
