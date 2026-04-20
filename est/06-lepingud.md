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

| Leping                                         | Kood               |Turg         |
|------------------------------------------------|--------------------|-------------|
| võrguleping                                    | GRID               |Elekter, Gaas|
| piirimõõtepunkti võrguleping                   | BORDER_GRID        |Elekter, Gaas|
| avatud tarne leping                            | SUPPLY             |Elekter, Gaas|
| agregeerimisleping                             | AGGREGATION        |Elekter      |
| portfellileping (siia kuulub ka bilansileping) | PORTFOLIO_SUPPLIER |Elekter, Gaas|
| nimetatud tarnija leping                       | NAMED_SUPPLIER     |Elekter, Gaas|
| ühisarve leping                                | JOINT_INVOICE      |Elekter, Gaas|

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

- Vastav turuosaline saadab uue või muutunud lepingu sõnumi kasutades teenust vastavat teenust.
- Sõltuvalt lepingu tüübist, osalistest ja muudest andmetest võib Andmeladu teha lisandunud või muutunud lepingu andmed kättesaadavaks andmete levitamise teenuse vahendusel.
- Õigustatud kasutaja pärib lepingu andmed lepingute otsingu teenusest ning vajadusel ekspordib lepinguid kasutades lepingute eksportimise teenust.

### Veebiliidese abil

> [!NOTE]
> Lepingute loomine veebiliidese abil on kirjeldatud alamlehtedel.

### Masinliidese sõnumid

Andmelaos on erinevate lepingute edastamise liides ühtlustatud ja seega on kasutusel samad sõnumid ja andmestruktuurid. Küll aga tasub tähele panna, et erinevatel lepingutel on erinevad reeglid ja seega ka erinev nõutud ja lubatud andmekoosseis.

| V2 sõnum                         | Eesmärk                       |
|----------------------------------|-------------------------------|
| `POST /api/v2/agreements`        | Lepingu loomine               |
| `POST /api/v2/agreements/bulk`   | Mitme lepingu loomine korraga |
| `PUT /api/v2/agreements/{id}`    | Lepingu uuendamine            |
| `DELETE /api/v2/agreements/{id}` | Lepingu kustutamine           |




#### Sõnumite reeglid

Lepingute omavahelised sõltuvused ja reeglid:

- Portfelli, ühisarve või nimetatud tarnija lepingu kehtivusajad samade osapoolte vahel ei tohi kattuda
- (Piirmõõtepunkti) võrgulepingu, (piirmõõtepunkti) avatud tarne lepingu, agregeerimislepingu või üldteenuse lepingute kehtivusajad samade osapoolte vahel ja samas mõõtepunktis ei tohi kattuda
- Avatud tarnija saab avatud tarne lepinguid lisada alles siis, kui tal on kehtiv portfellileping (ehk avatud tarnija on kellegi portfellis). Kehtivuse aega arvesse ei võeta.
- Võrguettevõtja saab võrgulepinguid lisada alles siis, kui tal on kehtiv portfellileping (ehk  võrguettevõtja on kellegi portfellis). Kehtivuse aega arvesse ei võeta.
- Agregaator saab agregeerimislepinguid lisada alles siis, kui tal on kehtiv portfellileping (ehk  agregaator on kellegi portfellis). Kehtivuse aega arvesse ei võeta (ainult elektriturg).
- Avatud tarne lepingu sõlmimise aluseks on kehtiv võrguleping mõõtepunktis. Avatud tarne lepingu kehtivus ei tohi kummastki otspunktist ületada võrgulepingu kehtivust.
- Agregeerimislepingu sõlmimise aluseks on kehtiv võrguleping võrgu ülemmõõtepunktis. Agregeerimislepingu kehtivus ei tohi kummastki otspunktist ületada ülemmõõtepunkti võrgulepingu kehtivust (ainult elektriturg).

Muud reeglid:

- Lepingu alguse ja lõpu aeg esitatakse kasutajaliideses päeva või kuu täpsusega:
  - vaata allpool olev tabel: kasutajaliides — kuu täpsus
- Lepingu alguse ja lõpu aeg esitatakse andmevahtusliideses kellaaja täpsusega:
  - vaata allpool olev tabel: kasutajaliides — päeva täpsus ja andmevahetusliides algus/lõpp
- Lepingu lõpu kuupäev peab olema võrdne või hilisem alguskuupäevast (ühepäevasel lepingul on alguse ja lõpu kuupäevad samad, kuid kellaajad erinevad).
- Kehtivat ega kehtivuse kaotanud lepingut kustutada (*delete*) ei ole lubatud. Kehtivat lepingut on võimalik sulgeda, uuendades lepingu lõppemise kuupäeva väärtust.
- Kehtivuse kaotanud lepingut muuta ei ole lubatud.
- Lepingus märgitud energia liik peab olema sama lepingus märgitud mõõtepunkti energia liigiga (juhul, kui lepingu tüüp neid andmeid ette näeb).
- Lepingute puhul on lubatud muuta ainult operaatoripoolset lepingu ID-d ja lepingu lõpu kuupäeva. Ülejäänud andmete muutmine ei ole lubatud.

Elektrituru ja gaasituru lepingite alguse ja lõpu erisused 

| **Valdkond** | **Reegel / kirjeldus** | **Elektriturg (südaöö – südaöö)** | **Gaasiturg (gaasipäev 07:00 – 07:00)** |
|--------------|-------------------------|------------------------------------|-------------------------------------------|
| **Kasutajaliides — kuu täpsus** | Leping algab | Kuu 1. päev 00:00 | Kuu 1. päev 07:00 |
| | Leping lõpeb | kuu viimase päeva südaööl | Järgnev kuu 1. päev 07:00 |
| **Kasutajaliides — päeva täpsus** | Leping algab | Valitud päev 00:00 (näiteks: 01.01.2024 00:00) | Valitud päev 07:00 (näiteks: 01.01.2024 07:00)|
| | Leping lõpeb | valitud päeva südaööl (näiteks: 30.04.2024 südaöö) | Järgnev päev 07:00 (näiteks: 01.05.2024 07:00) |
| **Andmevahetusliides — algus** | Algusaeg EE aja järgi | 01.01.2024 00:00:00 | 01.01.2024 07:00:00 |
| Sõnumis tuleb edastada | Alguse näide (talveaeg) | 2024-01-01T00:00:00+02:00 või 2023-12-31T22:00:00Z | 2024-01-01T07:00:00+02:00 või 2024-01-01T05:00:00Z |
| **Andmevahetusliides — lõpp** | Lõppaeg EE aja järgi | 30.04.2024 südaööl | 01.05.2024 07:00:00 |
| Sõnumis tuleb edastada | Lõpu näide (suveaeg) | 2024-05-01T00:00:00+03:00 või 2024-04-30T21:00:00Z | 2024-05-01T07:00:00+03:00 või 2024-05-01T04:00:00Z |
| **Tulemuseks kehtib kuni** | Andmelao tõlgenduse järgi | 30.04.2024 23:59:59 | 01.05.2024 06:59:59 |


## Lepingute otsimine ja eksport

Lepinguid otsitakse kahes äriprotsessis:

- Kui turuosaline soovib leida (ja soovi korral eksportida) lepinguid, kus ta on teenusepakkuja või klient.
- Kui turuosaline soovib lisada uut võrgu, avatud tarne või agregeerimise lepingut ja soovib näha mõõtepunkti teisi lepinguid

### Masinliidese sõnumid

Andmelaos on erinevate lepingute edastamise liides ühtlustatud ja seega on kasutusel samad sõnumid ja andmestruktuurid. Küll aga tasub tähele panna, et erinevatel lepingutel on erinevad reeglid ja seega ka erinev nõutud ja lubatud andmekoosseis.

| V2 sõnum                                       | Eesmärk                                                            |
|------------------------------------------------|--------------------------------------------------------------------|
| `GET /api/v2/agreements`                       | Lepingute otsing, kus turuosaline on kas teenusepakkuja või klient |
| `GET /api/v2/agreements/{id}`                  | Lepingu otsing ID alusel                                           |
| `GET /api/v2/metering-points/{eic}/agreements` | Mõõtepunkti lepingute otsing uue lepingu lisamisel                 |
| `GET /api/v2/agreements/export`                | Lepingute eksport                                                  |                                                 |

#### Sõnumite reeglid

> [!CAUTION] 
> Teenuse `/agreement/search/meter` või `/metering-points/{eic}/agreements` kasutamine on lubatud ainult uue lepingu loomise protsessis. Teenuse kasutamist ja kasutamise õiguspärastust monitooritakse.

### Veebiliidese abil

> [!NOTE]
> Lepingute loomine veebiliidese abil on kirjeldatud alamlehtedel.
