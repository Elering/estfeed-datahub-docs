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

Andmeladu võimaldab registreerida kolme tüüpi mõõtepunkte:
1. Elektri mõõtepunkt;
2. Gaasi mõõtepunkt;
3. Agregeerimise mõõtepunkt;

Mõõtepunkte haldavad järgmised turuosalised:

- võrguettevõtja
- liinioperaator
- suletud jaotusvõrgu ettevõtja
- agregaator
- tootja
- laadimispunkti operaator
- salvestusjaama operaator
- gaasitankla operaator

Käesolevas dokumendis nimetatakse neid ühisnimetajaga **Mõõtepunkti haldur**.

Mõõtepunkti haldur vastutab Andmelaos tema piirkonnas olevate mõõtepunktid kohta mõõtepunkti andmete lisamise ja uuendamise eest.

Mõõtepunkti andmestik sisaldab järgmist teavet:

1. mõõtepunkti EIC kood;
2. mõõtepunkti tüüp (virtuaalne, kaugloetav, kohtloetav);
3. energia tüüp (elekter või gaas)
4. mõõtepunkti asukoha aadress;
5. elektrimõõtepunkti metaandmestik
6. gaasimõõtepunkti metaandmestik
7. agregeerimismõõtepunkti metaandmestik

> **Warning**
> 
> NB! Mõõtepunkti haldur on kohustatud mõõtepunkti andmeid uuendama esimesel võimalusel.

## Mõõtepunkti andmete edastamine

Mõõtepunkti haldur saab mõõtepunktide tehnilised andmed edastada Andmelattu nii veebiliidese kaudu masslaadimisega kui ka automaatse andmevahetuse sõnumiga.

Mõõtepunkti andmete edastamiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Vajadusel kasutab võrguettevõtja eelnevalt teenust `range` et leida vaba EIC kood mõõtepunkti registreerimiseks
- Võrguettevõtja saadab uue või muutunud mõõtepunkti sõnumi kasutades teenust `meter` või `gridagreementmeteringpoint`


### Veebiliides

> **Note**
> Dokumentatsioon on loomisel

### Masinliidese sõnumid

#### Sõnumid

|Sõnum|Eesmärk|
|-----|-------|
|`POST /api/{version}/eic/range`|Võimaldab pärida vaba(d) EIC koodi(d) omale eraldatud vahemikust|
|`POST /api/{version}/meter`|Võimaldab registreerida uue mõõtepunkti|
|`PUT /api/{version}/meter`|Võimaldab uuendada mõõtepunkti andmeid|
|`POST /api/{version}/gridagreementmeteringpoint`|Võimaldab registreerida mõõtepunkti koos võrgulepinguga korraga|

Sõnumite struktuuride ja validatsioonide kirjeldused on leitavad [Swagger](https://test-datahub.elering.ee/swagger-ui/index.html) keskkonnast.

> **Note**
> Sõnumite näidiste kogumik on loomisel

#### Sõnumite reeglid

- Mõõtepunkti EIC kood peab jääma võrguettevõtja EIC koodide vahemikku
- Piirimõõtepunkt on mõõtepunkt, kus võrguettevõtja on võrguteenuse klient
- Mõõtepunkti resolutsiooni reeglid on energia tüübist sõltuvad:
  - Elektri puhul on resolutsioon täiendav info ja ei mõjuta mõõteandmete edastamist tulevikus vaid iseloomustab, kas mõõtepunkt suudab  reaalsuses tarbimist mõõta 15 minuti, 1 tunni või lausa päeva täpsusega
  - Gaasi puhul on resolutsioon rangelt seotud mõõteandmete resolutsiooniga. Näiteks kui mõõtepunkti resolutsioon on 1 päev, siis peavad ka edastatud mõõteandmed olema resolutsioonis 1 päev

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)

## Mõõtepunkti andmete küsimine

Üldiselt võivad kõik õigustatud kasutajad pärida mõõtepunktide andmeid kasutades `search` teenuseid, kuid avatud tarnija ja bilansihaldur saavad pärida ka uute ja muutunud mõõtepunktide andmete uuendusi kasutades teenust `changes`.

### Masinliidese sõnumid

#### Sõnumid

|Sõnum|Eesmärk|
|-----|-------|
|`POST /api/{version}/meter/search`|Võimaldab otsida mõõtepunkte mõõtepunkti andmete alusel|
|`POST /api/{version}/meter/search/customer`|Võimaldab otsida mõõtepunkte kliendi andmete alusel|
|`POST /api/{version}/meter/export`|Võimaldab eksportida tingimustele vastavad mõõtepunktid|
|`POST /api/{version}/meter/changes`|Võimaldab skaneerida mõõtepunktide andmete uuendusi.|

Sõnumite struktuuride ja validatsioonide kirjeldused on leitavad [Swagger](https://test-datahub.elering.ee/swagger-ui/index.html) keskkonnast.

> **Note**
> Sõnumite näidiste kogumik on loomisel

#### Sõnumite reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)

1. Kui andmete pärijal puudub vajalik kliendi andmete nägemise õigus, siis otsingu teenus tagastab ainult EIC koodi.
2. Andmeladu väljastab mõõtepunkti andmed ilma aadressita, kui teostatakse võrgueeskirja §8 lg 5 järgset kontrolli.
3. Ligipääsuõiguste olemasolul väljastab Andmeladu kogu mõõtepunkti andmestiku
