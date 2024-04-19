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
    * [Masinliidese sõnumid](#masinliidese-sõnumid-1)
      * [Sõnumid](#sõnumid-1)
      * [Sõnumite reeglid](#sõnumite-reeglid-1)
<!-- TOC -->

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

- Mõõtepunkti haldur saadab uue või muutunud mõõteandmete sõnumi kasutades teenust `meter-data`.
- Kuivõrd mõõteandmete töötlemine toimub Andmelaos asünkroonselt, siis esmalt annab Andmeladu kiire vastuse, kas sõnum õnnestus kätte saada või mitte.
- Seejärel paneb Andmeladu sõnumi töötluse järjekorda.
- Mõõtepunkti haldur kontrollib andmete töötluse tulemust, kasutades teenust `meter-data/status`. Võimalikud tulemused on:
  - `PROCESSING` - töötlus ei ole veel lõppenud
  - `SUCCESSFUL` - töötlus lõppes vigadeta
  - `ÈRROR` - töötlus lõppes vigadega
- Kui sõnumi töötlemine õnnestub vigadeta, siis andmed lisatakse või muudetakse andmebaasis ning Andmeladu teeb mõõteandmete lisandumise või muutumise kättesaadavaks avatud tarnijatele läbi `data-distribution/search` teenuse. Loe täpsemalt peatükist [Andmete levitamine](30-andmete-levitamine.md).
- Kui sõnumi töötlemisel tekivad vead, siis Andmeladu koostab vearaporti ja teeb selle kättesaadavaks mõõtepunkti haldurile teenuse `meter-data/status` vastuses.
- Mõõtepunkti haldur loeb talle adresseeritud vearaportit ning lahendab selle vastavalt oma sisemisele äriloogikale.

> **Warning**
>
> **NB! Andmeladu edastab võrguettevõtjate poolt sisestatud mõõteandmed muutmata kujul. Andmeladu ei kontrolli mõõteandmete sisu**

### Mõõteandmete edastamine veebiliidese kaudu

> **Note**
> Dokumentatsioon on loomisel

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

> **Warning**
> 
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

Sõnumite struktuuride ja validatsioonide kirjelduste kohta loe dokumendist [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](01-avp-kirjeldus-ja-infovahetuse-yldpohimotted.md)

> **Note**
> Sõnumite näidiste kogumik on loomisel

#### Sõnumite reeglid

- Mõõteandmete ja mõõtepunkti resolutsiooni seose kohta loe täpsemalt dokumendist [Mõõtepunktid](05-mootepunktid.md#sõnumite-reeglid).
- Perioodi ajaperioodi väärtus peab olema vastavuses resolutsiooniga. Näiteks:
  - kui resolutsioon on 1 tund, siis perioodi alguse kellaaeg peab olema täistund (hh:00);
  - kui resolutsioon on 15 minutit, siis perioodi alguse kellaaeg peab olema veerandtund (hh:00, hh:15, hh:30, hh:45).
- Elektri mõõtekogused esitatakse alati kWh-des täpsusega 3 kohta peale koma.
- Gaasi mõõtekogused esitatakse nii kWh-des kui ka kuupmeetrites täpsusega 3 kohta peale koma.
- Mõõteandmete suund esitatakse alati mõõtva mõõtepunkti halduri poolt vaadatuna:
  - in – võrku sisenev energia (tootmine);
  - out – võrgust väljuv energia (tarbimine).
- Siseneva ja väljuva energia koguseid võib edastada ka eraldi sõnumitega.
- Mõõteandmeid on lubatud korrigeerida tagasiulatuvalt kuni 12 kuud.
- Teenuses `import` tuleb kasutada sama templiiti, mida väljastab teenus `export`

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](03-autentimine-ja-autoriseerimine.md)

## Mõõteandmete päringud

Mõõteandmete edastamiseks on loodud vastavad Andmelao teenused. Andmetele ligipääs on piiratud. Reeglid on  kirjeldatud dokumendis [Autentimine ja autoriseerimine](03-autentimine-ja-autoriseerimine.md)

Mõõteandmete päringute teostamiseks on järgmised võimalused:

- Avatud tarnija skaneerib mõõteandmete muudatusi kasutades teenust `data-distribution/search`
- Õigustatud kasutaja pärib mõõteandmed kasutades teenust `search`

### Masinliidese sõnumid

#### Sõnumid

| Sõnum                                   | Eesmärk                   |
|-----------------------------------------|---------------------------|
| `POST /api/{version}/meter-data/search` | Mõõteandmete otsing       |
| `POST /api/{version}/meter-data/export` | Mõõteandmete eksportimine |

Sõnumite struktuuride ja validatsioonide kirjelduste kohta loe dokumendist [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](01-avp-kirjeldus-ja-infovahetuse-yldpohimotted.md)

> **Note**
> Sõnumite näidiste kogumik on loomisel

#### Sõnumite reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](03-autentimine-ja-autoriseerimine.md)
