# Lepingud

## Sisukord

<!-- TOC -->
* [Lepingud](#lepingud)
  * [Sisukord](#sisukord)
  * [Sissejuhatus](#sissejuhatus)
  * [Katkematu avatud tarne](#katkematu-avatud-tarne)
  * [Lepingute edastamine](#lepingute-edastamine)
    * [Veebiliidese abil](#veebiliidese-abil)
    * [Masinliidese sõnumid](#masinliidese-sõnumid)
      * [Sõnumite reeglid](#sõnumite-reeglid)
  * [Lepingute otsimine ja eksport](#lepingute-otsimine-ja-eksport)
    * [Masinliidese sõnumid](#masinliidese-sõnumid-1)
      * [Sõnumite reeglid](#sõnumite-reeglid-1)
    * [Veebiliidese abil](#veebiliidese-abil-1)
<!-- TOC -->

## Sissejuhatus

Süsteem võimaldab lisada järgmisi lepinguid:

| Leping                                         | Kood               |
|------------------------------------------------|--------------------|
| võrguleping                                    | GRID               |
| piirimõõtepunkti võrguleping                   | BORDER_GRID        |
| avatud tarne leping                            | SUPPLY             |
| agregeerimisleping                             | AGGREGATION        |
| portfellileping (siia kuulub ka bilansileping) | PORTFOLIO_SUPPLIER |
| nimetatud tarnija leping                       | NAMED_SUPPLIER     |
| ühisarve leping                                | JOINT_INVOICE      |

Erinevatel lepingutel on erinevad reeglid. Lisaks eksisteerivad lepingute omavahelised reeglid stiilis "avatud tarne lepingut ei saa lisada perioodi, kus puudub võrguleping".

## Katkematu avatud tarne

Bilansivastutus tagatakse katkematu avatud tarne ahela kaudu alljärgnevas hierarhias:

1. Süsteemihalduril on avatud tarne leping Eesti elektrisüsteemile. Süsteemihaldur selgitab Eesti elektrisüsteemi ja bilansihaldurite avatud tarned. Elering on oma võrgu võrgukadudele ise avatud tarnija.
2. Avatud tarnijat, kellel on bilansileping süsteemihalduriga, nimetatakse bilansihalduriks. Bilansihaldur kasutab bilansi selgitamiseks nende bilansipiirkonna piiripunktide mõõtmisi, kus tema vastutab bilansi eest.
3. Avatud tarnijal (v.a juhul, kui avatud tarnija on ise bilansihaldur) on avatud tarne leping ühe bilansihalduriga. Avatud tarnija selgitab oma piirkonnas nende turuosaliste bilansid, kelle avatud tarnijana ta tegutseb.
4. Jaotusvõrguettevõtjal on (võrgukadude katteks) oma teeninduspiirkonna kohta avatud tarne leping ühe avatud tarnijaga.
5. Tarbija ja tootja sõlmivad ühe avatud tarnijaga avatud tarne lepingu, sh ühe mõõtepunkti kohta saab olla igal ajaperioodil vaid üks avatud tarne leping.

## Lepingute edastamine

Lepinguid on võimalik Andmelattu edastada nii veebiliidese kui automaatse andmevahetuse sõnumi abil. Lepingu edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Vastav turuosaline saadab uue või muutunud lepingu sõnumi kasutades teenust `agreement`.
- Sõltuvalt lepingu tüübist, osalistest ja muudest andmetest võib Andmeladu teha lisandunud või muutunud lepingu andmed kättesaadavaks `data-distribution/search` teenuse vahendusel.
- Õigustatud kasutaja pärib lepingu andmed `agreement/search` teenusest ning vajadusel ekspordib lepinguid kasutades teenust `agreement/export`.

### Veebiliidese abil

> **Note**
> Lepingute loomine veebiliidese abil on kirjeldatud alamlehtedel.

### Masinliidese sõnumid

Andmelaos on erinevate lepingute edastamise liides ühtlustatud ja seega on kasutusel samad sõnumid ja andmestruktuurid. Küll aga tasub tähele panna, et erinevatel lepingutel on erinevad reeglid ja seega ka erinev nõutud ja lubatud andmekoosseis.

| Sõnum                                  | Eesmärk                       |
|----------------------------------------|-------------------------------|
| `POST /api/{version}/agreement`        | Lepingu loomine               |
| `PUT /api/{version}/agreement`         | Lepingu uuendamine            |
| `POST /api/{version}/agreement/delete` | Lepingu kustutamine           |
| `POST /api/{version}/agreement-bulk`   | Mitme lepingu loomine korraga |

Sõnumite struktuuride ja validatsioonide kirjelduste kohta loe dokumendist [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](01-avp-kirjeldus-ja-infovahetuse-yldpohimotted.md)

> **Note**
> Sõnumite näidiste kogumik on loomisel

#### Sõnumite reeglid

Lepingute omavahelised sõltuvused ja reeglid:

- Ühel ajahetkel saab samade osapoolte vahel olla ainult üks kehtiv sama tüüpi leping.
- Avatud tarnija saab avatud tarne lepinguid lisada alles siis, kui tal on kehtiv portfellileping (ehk avatud tarnija on kellegi portfellis). Kehtivuse aega arvesse ei võeta.
- Võrguettevõtja saab võrgulepinguid lisada alles siis, kui tal on kehtiv portfellileping (ehk  võrguettevõtja on kellegi portfellis). Kehtivuse aega arvesse ei võeta.
- Agregaator saab agregeerimislepinguid lisada alles siis, kui tal on kehtiv portfellileping (ehk  agregaator on kellegi portfellis). Kehtivuse aega arvesse ei võeta.
- Avatud tarne lepingu sõlmimise aluseks on kehtiv võrguleping mõõtepunktis. Avatud tarne lepingu kehtivus ei tohi kummastki otspunktist ületada võrgulepingu kehtivust.
- Agregeerimislepingu sõlmimise aluseks on kehtiv võrguleping võrgu mõõtepunktis (mida nimetatakse ka ülemmõõtepunktiks). Agregeerimislepingu kehtivus ei tohi kummastki otspunktist ületada võrgulepingu kehtivust.

Muud reeglid:

- Lepingu alguse ja lõpu aeg esitatakse kasutajaliideses päeva või kuu täpsusega:
  - Kui lepingu liik lubab kehtivusaegu määrata kuu kaupa:
    - leping hakkab kehtima valitud kuu esimesel päeval kell 00:00
    - leping lõpeb valitud kuu viimasel päeva südaööl.
  - Kui lepingu liik lubab kehtivusaeg määrata päeva kaupa:
    - leping hakkab kehtima valitud päeval kell 00:00
    - leping lõpeb valitud päeva südaööl.
- Lepingu alguse ja lõpu aeg esitatakse andmevahtusliideses kellaaja täpsusega:
  - Lepingu alguse kellaaeg peab olema lepingu kehtivuse esimese päeva 00:00:00 Eesti aja järgi. Andmeladu tõlgendab esitatud kuupäeva sissearvatuna (*inclusive*). Näiteks, kui leping peaks algama 01.01.2024 algusest, siis peab sõnumis olema märgitud `2024-01-01T:00:00+02:00` või `2023-12-31T22:00:00Z`.
  - Lepingu lõpu kellaaeg peab olema lepingu lõpule järgneva päeva 00:00:00 Eesti aja järgi. Andmelagu tõlgendab esitatud kuupäeva väljaarvatuna (*exclusive*). Näiteks kui leping peaks lõppema 30.04.2024 südaööl, siis peab sõnumis olema märgitud `2024-05-01T00:00:00+03:00` või `2024-04-30T21:00:00Z`, mis Andmelao loogika järgi tähendab, et leping kehtis 30.04.2024 23:59:59 lõpuni.
- Lepingu lõpu kuupäev peab olema hilisem alguskuupäevast.
- Kehtivat ega kehtivuse kaotanud lepingut kustutada (*delete*) ei ole lubatud. Kehtivat lepingut on võimalik sulgeda, uuendades lepingu lõppemise kuupäeva väärtust.
- Lepingus märgitud energia liik peab olema sama lepingus märgitud mõõtepunkti energia liigiga (juhul, kui lepingu tüüp neid andmeid ette näeb).
- Lepingute puhul on lubatud muuta ainult operaatoripoolset ID-d ja lepingu lõpu kuupäeva. Ülejäänud andmete muutmine ei ole lubatud.

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](03-autentimine-ja-autoriseerimine.md)

## Lepingute otsimine ja eksport

Lepinguid otsitakse kahes äriprotsessis:

- Kui turuosaline soovib leida (ja soovi korral eksportida) lepinguid, kus ta on teenusepakkuja või klient.
- Kui turuosaline soovib lisada uut võrgu, avatud tarne või agregeerimise lepingut ja soovib näha mõõtepunkti teisi lepinguid

### Masinliidese sõnumid

Andmelaos on erinevate lepingute edastamise liides ühtlustatud ja seega on kasutusel samad sõnumid ja andmestruktuurid. Küll aga tasub tähele panna, et erinevatel lepingutel on erinevad reeglid ja seega ka erinev nõutud ja lubatud andmekoosseis.

| Sõnum                                        | Eesmärk                                                            |
| -------------------------------------------- | ------------------------------------------------------------------ |
| `POST /api/{version}/agreement/search`       | Lepingute otsing, kus turuosaline on kas teenusepakkuja või klient |
| `POST /api/{version}/agreement/search/meter` | Mõõtepunkti teiste lepingute otsing uue lepingu lisamisel          |
| `POST /api/{version}/agreement/export`       | Lepingute eksport                                                  |

Sõnumite struktuuride ja validatsioonide kirjelduste kohta loe dokumendist [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](01-avp-kirjeldus-ja-infovahetuse-yldpohimotted.md)

> **Note**
> Sõnumite näidiste kogumik on loomisel

#### Sõnumite reeglid

> **Warning**
> 
> Teenuse `/agreement/search/meter` kasutamine on lubatud ainult uue lepingu loomise protsessis. Teenuse kasutamist ja kasutamise õiguspärastust monitooritakse.

- Mõõtepunkti lepingute otsingu teenus tagastab lepinguite täisandmestiku ainult juhul, kui otsingu teostaja on lepingu teenusepakkuja või kui mõõtepunkti klient on andnud turuosalisele esindusõiguse

### Veebiliidese abil

> **Note**
> Lepingute loomine veebiliidese abil on kirjeldatud alamlehtedel.
