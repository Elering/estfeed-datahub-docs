# Bilansipiirkond

## Sisukord

- [Bilansipiirkond](#bilansipiirkond)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Bilansipiirkonna sõnum](#bilansipiirkonna-sõnum)
  - [Masinliidese sõnumid](#masinliidese-sõnumid)
  - [Sõnumi reeglid](#sõnumi-reeglid)
  - [Sõnumi atribuutide reeglid](#sõnumi-atribuutide-reeglid)

## Sissejuhatus

Bilansipiirkond on teisisõnu portfell, mis koosneb mõõtepunktidest. Iga mõõtepunkt peab kuuluma mingisse bilansipiirkonda. Bilansipiirkonda kuulumise määrab see, kes on antud ajahetkel energia müüja sellele mõõtepunktile.

Bilansipiirkonna moodustamise reegel on järgmine: bilansihalduri bilansipiirkond on määratud bilansihalduri bilansipiirkonnas olevate turuosaliste bilansiselgituse mõõtepunktidega – see on mõõtepunkt, kus turuosalise bilansihaldur ja võrguettevõtja bilansihaldur selles mõõtepunktis on erinevad.

Bilansihaldurile kohanduvad Andmelaos avatud tarnija õigused ja kohustused. Bilansihalduri tarneahela moodustavad turuosalised, kellel on bilansihalduriga sõlmitud avatud tarne leping, ning bilansihalduri poolt portfellilepingutega sisestatud teised avatud tarnijad ja/või võrguettevõtjad.

Bilansihalduri bilansipiirkond on Andmelaos bilansihaldurile nähtav järgmiselt:

1. Mõõtepunkti EIC kood.
2. Kliendi EIC kood.
3. Mõõtepunkti võrguoperaatori EIC kood.
4. Võrguoperaatori bilansihalduri EIC kood.
5. Kui mõõtepunkt on bilansihalduri tarneahelas: mõõtepunktis avatud tarnija EIC kood ja bilansihalduri EIC kood.
6. Kui mõõtepunkt ei ole bilansihalduri tarneahelas: mõõtepunktis avatud tarnija ja bilansihaldur ei ole nähtavad.
7. Periood (avatud tarne lepingu algus- ja lõpuaeg).

Bilansihaldur saab Andmelaost mõõteandmed järgmiselt:

1. Mõõteandmed nendest mõõtepunktidest, mis on lepingute alusel bilansihalduri avatud tarne ahelas.
2. Kui võrguettevõtja piirimõõtepunktid on selle bilansihalduri bilansipiirkonna piirimõõtepunktid, saadakse mõõteandmed samuti nendest piirimõõtepunktidest.

## Bilansipiirkonna sõnum

Kasutatakse bilansihaldurile ja süsteemihaldurile bilansihalduri piirkonnas toimunud bilansiselgituse mõõtepunktide muudatuste edastamiseks. Bilansipiirkonna muudatussõnumi genereerimise ja edastamise protsess on järgmine:

- Andmelaos aktiveerub uus võrgu- või avatud tarne või portfellileping VÕI olemasolev võrgu- või avatud tarne või portfellileping lõppeb (ööpäeva vahetusel).
- Bilansihaldur pärib endale sobival ajal bilansipiirkonna muudatused kasutades teenust `balance-settlement-point/change` ja määrates ära kuupäeva, mille muudatusi soovib.
- Andmeladu arvutab ja tagastab muudatused koheselt. Sõnum sisaldab uusi bilansiselgituse mõõtepunkte bilansipiirkonnas *(ADDED)* või bilansipiirkonnast välja arvatud bilansiselgituse mõõtepunkte *(REMOVED)*.

## Masinliidese sõnumid

| Sõnum                                                 | Eesmärk                                                             |
|-------------------------------------------------------|---------------------------------------------------------------------|
| `POST /api/{version}/balance-settlement-point/change` | Võimaldab otsida bilansiselgituse mõõtepunktide muudatusi           |
| `POST /api/{version}/balance-settlement-point/search` | Võimaldab otsida bilansiselgituse mõõtepunkte soovitud ajaperioodil |

Sõnumite struktuuride ja validatsioonide kirjelduste kohta loe dokumendist [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](01-avp-kirjeldus-ja-infovahetuse-yldpohimotted.md)

## Sõnumite reeglid

- Teenus annab vastuse ainult bilansihalduritele (kellel on portfellileping TSO-ga). Teistele bilansipuu portfelliteenuse pakkujatele andmeid ei väljastata.
- `change` sõnumiga saab pärida ainult ühe kuupäeva muudatusi. Pikema perioodi muudatuste pärimiseks tuleb sõnumit saata mitu korda soovitud perioodi kuupäevadega.

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](03-autentimine-ja-autoriseerimine.md)

## Sõnumite atribuutide reeglid

### Teenus `change`

| Atribuut teenuses    | Selgitus                                 | Kohustuslik? | Muud reeglid                                                                                                                                 |
| -------------------- | ---------------------------------------- | ------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| updatePeriodStart    | Muudatuse alguse kuupäev                 | ei           | Võimaldab otsida vabalt valitud kuupäeva muudatusi. Kellaja väärtust ignoreeritakse. Kui täitmata, siis süsteem väärtustab tänase kuupäevaga |
| meteringPointActions | Muudatuse tüüp                           | ei           | ADDED - lisatud; REMOVED - eemaldatud                                                                                                        |
| includeParticipants  | Kas vastusesse kaasata lepingu osapooled | ei           | Väärtuse "true" puhul on vastuses täidetud positsioon `serviceProviders`                                                                     |

### Teenus `search`

| Atribuut teenuses  | Selgitus                                 | Kohustuslik? | Muud reeglid                                                                                    |
|--------------------|------------------------------------------|--------------|-------------------------------------------------------------------------------------------------|
| periodStart        | Soovitud perioodi alguse kuupäev         | jah          | periodStart ja periodEnd määravad perioodi, mille kohta soovitakse bilansiselgituse mõõtepunkte |
| periodEnd          | Soovitud perioodi lõpu kuupäev           | jah          |                                                                                                 |
| meteringPointTypes | Kas vastusesse kaasata lepingu osapooled | ei           | REGULAR - tavamõõtepunkt; BORDER - piirimõõtepunkt                                              |