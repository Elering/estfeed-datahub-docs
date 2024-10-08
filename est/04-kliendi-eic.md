# Kliendid

## Sisukord

<!-- TOC -->
* [Kliendid](#kliendid)
  * [Sisukord](#sisukord)
  * [Sissejuhatus](#sissejuhatus)
  * [Kliendi andmete edastamine ja pärimine](#kliendi-andmete-edastamine-ja-pärimine)
  * [Masinliidese sõnumid](#masinliidese-sõnumid)
  * [Sõnumite reeglid](#sõnumite-reeglid)
    * [Kliendi ja tema metaandmete lisamine ja muutmine](#kliendi-ja-tema-metaandmete-lisamine-ja-muutmine)
      * [Sõnumi atribuutide reeglid](#sõnumi-atribuutide-reeglid)
      * [Täiendavad reeglid](#täiendavad-reeglid)
    * [Kliendi ja tema metaandmete otsing](#kliendi-ja-tema-metaandmete-otsing)
      * [Sõnumi atribuutide reeglid](#sõnumi-atribuutide-reeglid-1)
    * [Äriregistri esindusõiguste otsing](#äriregistri-esindusõiguste-otsing)
    * [Kliendi lepingute otsing](#kliendi-lepingute-otsing)
    * [Kliendi mõõtepunktide otsing](#kliendi-mõõtepunktide-otsing)
<!-- TOC -->

## Sissejuhatus

Elektrituruseaduses nimetatud turuosalistest võimaldab Andmeladu lisada ja muuta ainult tarbija ehk kliendi (*Customer*) andmeid. Ülejäänud turuosalised hallatakse Andmelao süsteemihalduri poolt.

Igale kliendile omistatakse Andmelao poolt **EIC kood**, mis on peamine kliendi identifikaator süsteemis.

Andmeladu võimaldab registreerida nii Eesti kui ka välismaiseid füüsilisi ja juriidilisi isikuid. Lisaks on lisatud tugi selliste mittefüüsiliste isikutele, kellel puudub Eesti või mõne muu riigi Äriregistri (või samaväärse registri) kood. Näiteks saatkonnad.

## Kliendi andmete edastamine ja pärimine

Kliendi andmete edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on leitav lehelt [Äriprotsessid](02-äriprotsessid.md#klientide-haldus)

## Masinliidese sõnumid

| Sõnum                                                | Eesmärk                              | Kirjeldus ja reeglid                                                                                  |
|------------------------------------------------------|--------------------------------------|-------------------------------------------------------------------------------------------------------|
| `POST /api/{version}/customer`                       | Kliendi ja tema metaandmete lisamine | [Kliendi ja tema metaandmete lisamine ja muutmine](#kliendi-ja-tema-metaandmete-lisamine-ja-muutmine) |
| `PUT /api/{version}/customer`                        | Kliendi metaandmete muutmine         | [Kliendi ja tema metaandmete lisamine ja muutmine](#kliendi-ja-tema-metaandmete-lisamine-ja-muutmine) |
| `POST /api/{version}/customer/search`                | Kliendi ja tema metaandmete otsing   | [Kliendi ja tema metaandmete otsing](#kliendi-ja-tema-metaandmete-otsing)                             |

## Sõnumite reeglid

### Kliendi ja tema metaandmete lisamine ja muutmine

#### Sõnumi atribuutide reeglid

- Kliendi andmed on:

| Atribuut teenuses   | Selgitus                 | Kohustuslik? | Muud reeglid                                           |
|---------------------|--------------------------|--------------|--------------------------------------------------------|
| customerType        | Kliendi tüüp             | jah          | Üks neist: PHYSICAL_PERSON, LEGAL_PERSON, ORGANIZATION |
| customerMetadata    | Kliendi metaandmed       | jah          | Atribuutide selgitus on alljärgnevates jaotistes       |
| customerIdentifiers | Kliendi identifikaatorid | jah          | Atribuutide selgitus on alljärgnevates jaotistes       |

- customerMetadata:

Metaandmed on süsteemis modelleeritud võti-väärtus paaridena, kus "võti" on `metadataType` ja "väärtus" on `metadataValue`. Võti-väärtus paaridel saab olla kehtivusaeg. Ühel kliendil saab olla rohkem kui üks metaandmestik. Sellisel juhul on käesolevat sektsiooni sõnumis mitu korda.

| Atribuut teenuses | Selgitus                       | Kohustuslik? | Muud reeglid                                                                                                                                                                                                                       |
|-------------------|--------------------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| metadataType      | Metaandmestiku tüüp            | jah          | Üks neist: FIRST_NAME, LAST_NAME, COMPANY_NAME, PHONE, EMAIL, ORGANIZATION_NAME, MOBILE_PHONE, BILLING_ADDRESS, BILLING_BANK_NAME, BILLING_BANK_ACCOUNT, BILLING_METHOD                                                            |
| metadataValue     | Metaandmestiku väärtus         | jah          |                                                                                                                                                                                                                                    |
| validFrom         | Metaandmestiku kehtivuse algus | ei           | Ei tohi puududa, kui `validTo` on täidetud. Tavapärane väärtus on `now`, kuna täpse alguskuupäeva tuvastamine on võrguettevõtja jaoks keeruline. Aga kui see on teada, siis võib võrguettevõtja määrata täpse kuupäeva ja kellaaja |
| validTo           | Metaandmestiku kehtivuse lõpp  | ei           | Peab olema suurem, kui `validFrom`. Kasutatakse mõne metaandmestiku lõpetamiseks. Näiteks, kui `PHONE`ei ole enam kasutusel.                                                                                                       |

- customerIdentifiers:

Ühel kliendil võib olla rohkem kui üks identifikaator. Sellisel juhul on käesolevat sektsiooni sõnumis mitu korda.

| Atribuut teenuses | Selgitus                | Kohustuslik? | Muud reeglid                                                 |
|-------------------|-------------------------|--------------|--------------------------------------------------------------|
| identityType      | Identifikaatori tüüp    | jah          | Üks neist: PERSONAL_ID, DOCUMENT_ID, COMPANY_ID, EMBASSY_ID. |
| identityValue     | Identifikaatori väärtus | jah          |                                                              |

- identityExtension:

Ühel identifikaatoril võib olla rohkem kui üks laiendus. Näiteks kui identifikaatori `identityType` väärtus on `DOCUMENT_ID`, siis selle identifikaatori võib olla nii riigi kui ka väljaandja väärtused.

| Atribuut teenuses | Selgitus                  | Kohustuslik? | Muud reeglid                                                                                                                        |
|-------------------|---------------------------|--------------|-------------------------------------------------------------------------------------------------------------------------------------|
| extensionType     | Laienduse kehtivuse algus | ei           | Üks neist: COUNTRY, ISSUER                                                                                                          |
| extensionValue    | Laienduse kehtivuse lõpp  | ei           | Tüübi `COUNTRY` puhul tuleb kasutada [ISO standardi](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) 2-tähelisi koode |

#### Täiendavad reeglid

- Kliendi andmeid on lubatud lisada või muuta ainult võrguettevõtjal ja aktiivsel nimetatud müüjal.
- Füüsilise isiku lisamisel või muutmisel järgmised andmed kohustuslikud:
  - ees- ja perenimi;
  - riik;
  - isikukood, kui riigi väärtust on Eesti;
  - dokumendi number kui riigi väärtus ei ole Eesti ja isikukood puudub.
- Juriidilise isiku lisamisel või muutmisel järgmised andmed kohustuslikud:
  - nimetus;
  - riik;
  - Äriregistri kood;
- Organisatsiooni lisamisel või muutmisel on järgmised andmed kohustuslikud:
  - organisatsiooni nimi;
  - riik;
  - esinduse ID;
- Kliendi tüübi ja identiteedi tüübi lubatud kombinatsioonid on:

|             | ORGANIZATION | PHYSICAL_PERSON | LEGAL_PERSON |
|-------------|--------------|-----------------|--------------|
| PERSONAL_ID | -            | ✓               | -            |
| COMPANY_ID  | ✓            | -               | ✓            |
| DOCUMENT_ID | ✓            | ✓               | -            |
| EMBASSY_ID  | ✓            | -               | -            |

- Identitedi tüübi ja identiteedi laienduse tüübi lubatud kombinatsioonid on:

|             | COUNTRY | ISSUER |
|-------------|---------|--------|
| PERSONAL_ID | ✓       | ✓      |
| COMPANY_ID  | ✓       | ✓      |
| DOCUMENT_ID | ✓       | ✓      |
| EMBASSY_ID  | ✓       | -      |

- Kliendi tüübi ja tema metaandmestiku tüübi lubatud kombinatsioonid on:

|                      | ORGANIZATION | PHYSICAL_PERSON | LEGAL_PERSON |
|----------------------|--------------|-----------------|--------------|
| ORGANIZATION_NAME    | ✓            | -               | -            |
| FIRST_NAME           | -            | ✓               | -            |
| LAST_NAME            | -            | ✓               | -            |
| COMPANY_NAME         | -            | -               | ✓            |
| PHONE                | ✓            | ✓               | ✓            |
| MOBILE_PHONE         | ✓            | ✓               | ✓            |
| EMAIL                | ✓            | ✓               | ✓            |
| BILLING_METHOD       | ✓            | ✓               | ✓            |
| BILLING_BANK_NAME    | ✓            | ✓               | ✓            |
| BILLING_BANK_ACCOUNT | ✓            | ✓               | ✓            |
| BILLING_ADDRESS      | ✓            | ✓               | ✓            |


- Ühel ajahetkel saab kehtida ainult üks sama tüübiga metaandmestik. Andmete uuendamisel muudab Andmeladu eelmise väärtuse kehtetuks (vastavalt edastatud `validFrom` ja `validTo` väärtustele või nende puudumisel automaatselt).
- Metaandmestiku `BILLING_METHOD` reeglid:
  - Lubatud väärtused on: `EMAIL`, `POST`, `BANK` ja `SELF_SERVICE`
  - Mitme väärtuse lisamisel on lubatud komaga eraldatud andmed. Näiteks: `EMAIL,POST` (ilma tühikuteta)
  - Täiendavate metaandmete vajadus sõltuvalt väärtusest:
    - väärtuse `EMAIL` korral peab sõnumis või varasemas andmestikus eksisteerima metaandmestik `EMAIL`
    - väärtuse `POST` korral peab sõnumis või varasemas andmestikus eksisteerima metaandmestik `BILLING_ADDRESS`
    - väärtuse `BANK` korral peavad sõnumis või varasemas andmestikus eksisteerima metaandmestikud `BILLING_BANK_ACCOUNT` ja `BILLING_BANK_NAME`
    - väärtuse `SELF_SERVICE` või `B2B_BILL` korral täiendavad nõutavad andmed puuduvad
- Eesti isikukoodi ja äriregistri koodi puhul rakendub formaadi kontroll.
- Välismaiste ID-de puhul formaadi kontrolli ei rakendu.
- Uue kliendi registreerimisel peab `customerType + identityType + identityValue + extensionType(COUNTRY)` kombinatsioon peab olema unikaalne. Kui ei ole, siis on tegu olemasoleva kliendiga ning andmete uuendamiseks tuleb kasutada `PUT` teenust.

### Kliendi ja tema metaandmete otsing

#### Sõnumi atribuutide reeglid

| Atribuut teenuses     | Selgitus                            | Kohustuslik? | Muud reeglid                                                                                      |
|-----------------------|-------------------------------------|--------------|---------------------------------------------------------------------------------------------------|
| customerTypes         | Kliendi tüübid                      | jah          | One of: PHYSICAL_PERSON, LEGAL_PERSON, ORGANIZATION, MARKET_PARTICIPANT. Lubatud on mitu väärtust |
| marketParticipantRole | Otsitava turuosalise roll Andmelaos | ei           | Kasutatakse turuosalise otsingu puhul                                                             |
| searchCriteria        | Otsingu tingimused                  | jah          | Kasutab sama struktuuri nagu `customerIdentifiers`                                                |

- Kliendi otsingu teenus tagastab ainult kliendi EIC koodi juhul, kui andmete pärijal puudub vastav õigus.
- Nime järgi saab otsida juriidilisi isikuid ja organisatsioone. Füüsilisi isikuid nime järgi otsida ei saa.
- Metaandmeid `BILLING_*`, `PHONE`, `MOBILE_PHONE` ja `EMAIL` väljastatakse ainult juhul, kui:
  - pärijaks on on nimetatud müüja, kellel on hetkel aktiivne (või oli viimase 12 kuu jooksul aktiivne) üldteenuse leping antud kliendiga.
  - pärijaks on võrguoperaator või suletus jaotusvõrgu operaator kellel on või on olnud võrgu või piirimõõtepunkti võrgu leping antud kliendiga.

### Äriregistri esindusõiguste otsing

> [!NOTE]
> Dokumentatsioon on loomisel

### Kliendi lepingute otsing

Loe täpsemalt peatükist [Lepingud](06-lepingud.md)

### Kliendi mõõtepunktide otsing

Loe täpsemalt peatükist [Mõõtepunktid](05-mootepunktid.md)
