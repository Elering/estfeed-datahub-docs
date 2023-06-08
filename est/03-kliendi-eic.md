# Kliendid

## Sisukord

- [Kliendid](#kliendid)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Kliendi andmete edastamine ja pärimine](#kliendi-andmete-edastamine-ja-pärimine)
  - [Masinliidese sõnumid](#masinliidese-sõnumid)
    - [Sõnumid](#sõnumid)
    - [Sõnumite reeglid](#sõnumite-reeglid)

## Sissejuhatus

Elektrituruseaduses nimetatud turuosalistest võimaldab Andmeladu lisada ja muuta ainult tarbija ehk kliendi (*Customer*) andmeid. Ülejäänud turuosalised hallatakse Andmelao süsteemihalduri poolt.

Igale kliendile omistatakse Andmelao poolt **EIC kood**, mis on peamine kliendi identifikaator süsteemis.

Andmeladu võimaldab registreerida nii Eesti kui ka välismaiseid füüsilisi ja juriidilisi isikuid. Lisaks on lisatud tugi selliste mittefüüsiliste isikutele, kellel puudub Eesti või mõne muu riigi Äriregistri (või samaväärse registri) kood. Näiteks saatkonnad.

## Kliendi andmete edastamine ja pärimine

Kliendi andmete edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Võrguettevõtja saadab uue või muutunud kliendi sõnumi kasutades teenust `customer`.
- Andmeladu salvestab kliendi andmed ning määrab kliendile EIC koodi.
- Õigustatud kasutaja pärib kliendi andmed `customer/search` teenusest..
- Õigustatud kasutaja pärib uute ja muutunud klientide andmete uuendusi kasutades teenust `customer/changes`.

## Masinliidese sõnumid

### Sõnumid

| Sõnum                                  | Eesmärk                                          |
|----------------------------------------|--------------------------------------------------|
| `POST /api/{version}/customer`         | Võimaldab registreerida uut klienti.             |
| `PUT /api/{version}/customer`          | Võimaldab uuendada olemasoleva kliendi andmeid.  |
| `POST /api/{version}/customer/search`  | Võimaldab otsida registreeritud klienti.         |
| `POST /api/{version}/customer/changes` | Võimaldab skaneerida klientide andmete uuendusi. |

Sõnumite struktuuride ja validatsioonide kirjeldused on leitavad [Swagger](https://test-datahub.elering.ee/swagger-ui/index.html) keskkonnast.

> **Note**
> Sõnumite näidiste kogumik on loomisel

### Sõnumite reeglid

- Kliendi andmeid on lubatud lisada või muuta ainult võrguettevõtjal.
- Kui uue kliendi registreerimisel tuvastab Andmeladu, kas antud isik juba eksisteerib süsteemis:
  - Kui eksisteerib, siis tagastab Andmeladu sõnumi saatjale olemasoleva isiku EIC koodi ja kui sõnumis oli uusi andmeid, siis uuendab need (nt nimi).
  - Kui isikut veel ei eksisteeri, siis loob uue isiku, omistab EIC koodi ja tagastab EIC koodi.
- Füüsilise isiku lisamisel või muutmisel järgmised andmed kohustuslikud:
  - ees- ja perenimi;
  - riik;
  - isikukood, kui riigi väärtust on Eesti;
  - dokumendi number kui riigi väärtus ei ole Eesti ja isikukood puudub.
- Juriidilise isiku lisamisel või muutmisel järgmised andmed kohustuslikud:
  - nimetus;
  - riik;
  - Äriregistri kood, kui riigi väärtus on Eesti ja tegu ei ole saatkonnaga;
  - Muu identifikaator, kui tegu on välismaise ettevõttega või saatkonnaga.
- Eesti isikukoodi puhul rakendub formaadi kontroll.
- Välismaiste isikukoodide puhul formaadi kontrolli ei rakendu.
- Riigi väärtuse edastamiseks kasutatakse [ISO standardi](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) 2-tähelisi koode.
- Uue kliendi registreerimisel peab `customerType + identityType + identityValue + extensionType(COUNTRY)` kombinatsioon peab olema unikaalne. Kui ei ole, siis on tegu olemasoleva kliendiga ning süsteem kohtleb lisamise päringut kui kliendi andmete uuendamise päringuna ning võimalusel uuendab kliendi andmed.
- Kliendi otsingu teenus tagastab ainult kliendi EIC koodi juhul, kui andmete pärijal puudub vastav õigus.

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)
