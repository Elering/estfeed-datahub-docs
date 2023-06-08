# Bilansipiirkond

## Sisukord

- [Bilansipiirkond](#bilansipiirkond)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Bilansipiirkonna sõnum](#bilansipiirkonna-sõnum)
    - [Masinliidese sõnumid](#masinliidese-sõnumid)
    - [Sõnumid](#sõnumid)
    - [Sõnumi reeglid](#sõnumi-reeglid)
  - [Summeeritud mõõteandmete sõnum](#summeeritud-mõõteandmete-sõnum)
    - [Masinliidese sõnumid](#masinliidese-sõnumid-1)

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

1. Mõõteandmed nendest mõõtepunktidest, mis on elektrilepingute alusel bilansihalduri avatud tarne ahelas.
2. Kui võrguettevõtja piirimõõtepunktid on selle bilansihalduri bilansipiirkonna piirimõõtepunktid, saadakse mõõteandmed samuti nendest piirimõõtepunktidest.
3. Summeeritult mõõteandmed võrguettevõtja piirkonnas olevate mõõtepunktide kohta, mis on teiste bilansihaldurite portfellides. Raport edastatakse eelmise perioodi andmetega kell 10.30 bilansihalduri poolt Andmelaos märgitud aadressile.

## Bilansipiirkonna sõnum

Kasutatakse bilansihaldurile ja süsteemihaldurile bilansihalduri piirkonnas toimunud muudatuste edastamiseks. Bilansipiirkonna muudatussõnumi genereerimise ja edastamise protsess on järgmine:

- Andmelaos registreeritakse uus võrgu- või avatud tarne või portfellileping VÕI olemasolev võrgu- või avatud tarne või portfellileping lõppeb.
- Andmeladu arvutab kord ööpäevas viimase ööpäeva bilansimuudatused (mõõtepunkti sisenemine või väljumine bilansipiirkonnast).
- Andmeladu koostab kell 00:05 bilansimuudatuste sõnumi ja teeb selle kättesaadavaks selle vastava(te)le bilansihalduri(te)le, kelle bilansipiirkonnas muudatused toimusid `changes` teenuse kaudu. Loe täpsemalt peatükist [Andmete levitamine](30-andmete-levitamine.md). Sõnum sisaldab uusi mõõtepunkte bilansipiirkonnas *(ADDED)* või bilansipiirkonnast välja arvatud mõõtepunkte *(REMOVED)*.

### Masinliidese sõnumid

### Sõnumid

| Sõnum                                       | Eesmärk                                                   |
|---------------------------------------------|-----------------------------------------------------------|
| `POST /api/{version}/balance-state/changes` | Võimaldab skaneerida bilansipiirkonna muudatusi           |
| `POST /api/{version}/balance-state/search`  | Võimaldab otsida soovitud perioodi bilansipiirkonna seisu |

### Sõnumi reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)

## Summeeritud mõõteandmete sõnum

Bilansihalduritele edastatakse summeeritud mõõteandmeid, et bilansihaldurid saaksid prognoosida tuleviku tarbimist ja tootmist. Sõnumi genereerimise ja edastamise protsess on järgmine:

- Peale mõõteandmete lisamise või muutmise sõnumi töötlemist summeerib Andmeladu mõõteandmed selle võrguettevõtja piirkonnas olevate mõõteandmete (Pin ja Pout) kohta, mis on teiste bilansihaldurite portfellides.
- Kord ööpäevas (kell 14:00) koostab Andmeladu summeeritud mõõteandmete sõnumi ja teeb selle kättesaavaks bilansihaldurile(tele) `changes` teenuse kaudu. Loe täpsemalt peatükist [Andmete levitamine](30-andmete-levitamine.md). Sõnum sisaldab mõõteandmeid kehtiva kalendrikuu algusest alates (esimesel kuupäeval terve eelmise kuupäeva andmed), kusjuures iga päev lisanduvad andmed eelmise päeva kohta võrguettevõtja poolt Andmelattu saadetud andmetest.

### Masinliidese sõnumid

> **Note**
> Teenused on väljatöötamisel
