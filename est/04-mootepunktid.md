# Mõõtepunktid

## Sisukord

- [Mõõtepunktid](#mõõtepunktid)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Mõõtepunkti andmete edastamine](#mõõtepunkti-andmete-edastamine)
    - [Veebiliides](#veebiliides)
    - [Masinliidese sõnumid](#masinliidese-sõnumid)
      - [Sõnumid](#sõnumid)
      - [Sõnumite reeglid](#sõnumite-reeglid)
  - [Mõõtepunkti andmete küsimine](#mõõtepunkti-andmete-küsimine)
    - [Masinliidese sõnumid](#masinliidese-sõnumid-1)
      - [Sõnumid](#sõnumid-1)
      - [Sõnumite reeglid](#sõnumite-reeglid-1)

## Sissejuhatus

Mõõtepunkt on seade, mis mõõdab energia tarbimise ja tootmise koguseid teatud asukohas.

Mõõtepunkte haldavad järgmised turuosalised:

- võrguettevõtja;
- liinivaldaja;
- suletud jaotusvõrgu ettevõtja;
- agregaator;
- tootja;
- laadimispunkti operaator;
- salvestusjaama operaator;
- gaasitankla operaator.

Käesolevas dokumendis nimetatakse neid ühisnimetajaga **Mõõtepunkti haldur**.

Mõõtepunkti haldur vastutab Andmelaos tema piirkonnas olevate mõõtepunktid kohta mõõtepunkti andmete lisamise ja uuendamise eest.

Mõõtepunkti andmestik sisaldab järgmist teavet:

1. mõõtepunkti EIC kood;
2. mõõtepunkti tüüp:
   1. REGULAR - regulaarne ehk tavaline mõõtepunkt;
   2. BORDER - piirimõõtepunkt ehk mõõtepunkt, kus võrguettevõtja on võrguteenuse klient;
   3. AGGREGATION - agregeerimise mõõtepunkt;
   4. INTERNAL - sisemine mõõtepunkt, millel puudub seos mõne lepinguga;
3. mõõteviis:
   1. REMOTE_READING - kaugloetav;
   2. NON_REMOTE_READING - kohtloetav;
   3. VIRTUAL - virtuaalne;
4. energia tüüp:
   1. ELECTRICITY - elekter;
   2. NATURAL_GAS - gaas;
5. mõõtepunkti asukoha aadress;
6. elektrimõõtepunkti metaandmestik;
7. gaasimõõtepunkti metaandmestik;
8. agregeerimismõõtepunkti metaandmestik.

> **Warning**
> 
> NB! Mõõtepunkti haldur on kohustatud mõõtepunkti andmeid uuendama esimesel võimalusel.

## Mõõtepunkti andmete edastamine

Mõõtepunkti haldur saab mõõtepunktide tehnilised andmed edastada Andmelattu nii veebiliidese kaudu masslaadimisega kui ka automaatse andmevahetuse sõnumiga.

Mõõtepunkti andmete edastamiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Võrguettevõtja saadab uue või muutunud mõõtepunkti sõnumi kasutades teenust `meter`.

### Veebiliides

> **Note**
> Dokumentatsioon on loomisel

### Masinliidese sõnumid

#### Sõnumid

| Sõnum                                            | Eesmärk                                                         |
|--------------------------------------------------|-----------------------------------------------------------------|
| `POST /api/{version}/meter`                      | Võimaldab registreerida uue mõõtepunkti                         |
| `PUT /api/{version}/meter`                       | Võimaldab uuendada mõõtepunkti andmeid                          |
| `GET /api/{version}/template/`                   | Võimaldab alla laadida mõõtepunkti masslisamise Excel templiidi |
| `POST /api/{version}/meter/import`               | Võimaldab lisada mitu mõõtepunkti täidetud Excel templiidi abil |

Sõnumite struktuuride ja validatsioonide kirjelduste kohta loe dokumendist [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](01-avp-kirjeldus-ja-infovahetuse-yldpohimotted.md)

> **Note**
> Sõnumite näidiste kogumik on loomisel

#### Sõnumite reeglid

- Mõõtepunkti EIC kood peab jääma võrguettevõtja EIC koodide vahemikku.
- Mõõtepunkti tüüp defineerib lubatud metaandmestiku:
  - regulaarne, piirimõõtepunkt, sisemine - lubatud on gaasi või elektri metaandmestik;
  - agregeerimise - lubatud on agregeerimise metaandmestik;
- Mõõtepunkti resolutsioon on täiendav info ja ei mõjuta mõõteandmete edastamist tulevikus vaid iseloomustab, kas mõõtepunkt suudab  reaalsuses tarbimist mõõta 15 minuti, 1 tunni või päeva täpsusega.

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)

## Mõõtepunkti andmete küsimine

Üldiselt võivad kõik õigustatud kasutajad pärida mõõtepunktide andmeid kasutades `search` teenuseid, kuid avatud tarnija ja bilansihaldur saavad pärida ka uute ja muutunud mõõtepunktide andmete uuendusi kasutades teenust `change`.

### Masinliidese sõnumid

#### Sõnumid

| Sõnum                                       | Eesmärk                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| `POST /api/{version}/meter/search`          | Võimaldab otsida mõõtepunkte mõõtepunkti andmete alusel                                          |
| `POST /api/{version}/meter/search/customer` | Võimaldab otsida mõõtepunkte, kus sisendis olev klient on mõõtepunktiga seotud läbi mõne lepingu |
| `POST /api/{version}/meter/search/border`   | Võimaldab otsida piirimõõtepunkte, kus sisendis olev klient on mõõtepunktiga seotud läbi võrgulepingu |
| `POST /api/{version}/meter/export`          | Võimaldab eksportida tingimustele vastavad mõõtepunktid                                          |
| `POST /api/{version}/meter/change`          | Võimaldab skaneerida mõõtepunktide andmete uuendusi.                                             |

Sõnumite struktuuride ja validatsioonide kirjelduste kohta loe dokumendist [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](01-avp-kirjeldus-ja-infovahetuse-yldpohimotted.md)

> **Note**
> Sõnumite näidiste kogumik on loomisel

#### Sõnumite reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)

- Kui andmete pärijal puudub vajalik kliendi andmete nägemise õigus, siis otsingu teenus tagastab ainult EIC koodi.
- Andmeladu väljastab mõõtepunkti andmed ilma aadressita, kui teostatakse võrgueeskirja §8 lg 5 järgset kontrolli.
- Ligipääsuõiguste olemasolul väljastab Andmeladu kogu mõõtepunkti andmestiku.
