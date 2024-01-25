# Lepingud

## Sisukord

- [Lepingud](#lepingud)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Katkematu avatud tarne](#katkematu-avatud-tarne)
  - [Lepingute edastamine](#lepingute-edastamine)
    - [Lepingute edastamine veebiliidese abil](#lepingute-edastamine-veebiliidese-abil)
    - [Masinliidese sõnumid](#masinliidese-sõnumid)
      - [Sõnumid](#sõnumid)
      - [Sõnumite reeglid](#sõnumite-reeglid)

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

### Lepingute edastamine veebiliidese abil

> **Note**
> Veebiliides on valmimisel

### Masinliidese sõnumid

Andmelaos on erinevate lepingute edastamise liides ühtlustatud ja seega on kasutusel samad sõnumid ja andmestruktuurid. Küll aga tasub tähele panna, et erinevatel lepingutel on erinevad reeglid ja seega ka erinev nõutud ja lubatud andmekoosseis.

#### Sõnumid

| Sõnum                                        | Eesmärk                      |
|----------------------------------------------|------------------------------|
| `POST /api/{version}/agreement`              | Lepingu loomine              |
| `PUT /api/{version}/agreement`               | Lepingu uuendamine           |
| `POST /api/{version}/agreement/delete`       | Lepingu kustutamine          |
| `POST /api/{version}/agreement/search`       | Lepingute otsing             |
| `POST /api/{version}/agreement/search/meter` | Mõõtepunkti lepingute otsing |
| `POST /api/{version}/agreement/export`       | Lepingute eksport            |

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
- Avatud tarne ja agregeerimislepingu klient peab olema sama isik, kes on ka võrgulepingu klient.

Muud reeglid:

- Lepingu alguse aeg esitatakse päeva täpsusega, leping hakkab kehtima esitatud päeval kell 00:00.
- Lepingu lõpu aeg esitatakse päeva täpsusega, leping lõpeb esitatud päeva südaööl.
- Lepingu lõpu kuupäev peab olema hilisem alguskuupäevast.
- Kehtivat ega kehtivuse kaotanud lepingut kustutada (*delete*) ei ole lubatud. Kehtivat lepingut on võimalik sulgeda, uuendades lepingu lõppemise kuupäeva väärtust.
- Lepingus märgitud energia liik peab olema sama lepingus märgitud mõõtepunkti energia liigiga (juhul, kui lepingu tüüp neid andmeid ette näeb).
- Lepingute puhul on lubatud muuta ainult operaatoripoolset ID-d ja lepingu lõpu kuupäeva. Ülejäänud andmete muutmine ei ole lubatud.

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](03-autentimine-ja-autoriseerimine.md)