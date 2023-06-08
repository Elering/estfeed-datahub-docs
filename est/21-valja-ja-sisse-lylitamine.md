# Võrguühenduse välja- ja sisselülitamine

## Sisukord

- [Võrguühenduse välja- ja sisselülitamine](#võrguühenduse-välja--ja-sisselülitamine)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Väljalülitamise ja sisselülitamise taotlus ja kinnitus](#väljalülitamise-ja-sisselülitamise-taotlus-ja-kinnitus)
    - [Masinliidese sõnumid](#masinliidese-sõnumid)
      - [Sõnumid](#sõnumid)
      - [Sõnumite reeglid](#sõnumite-reeglid)

## Sissejuhatus

Kui Võrguteenuse osutaja ja avatud tarnija on sõlminud ühisarve lepingu, siis saadetakse turuosalisele alati ühisarve (turuosaline ei saa seda valida) ja avatud tarnijal tekib õigus nõuda võrguühenduse väljalülitamist juhul, kui turuosaline ei ole oma ühisarvet tasunud.

> **Warning**
> 
> Kogu käesolevas dokumendis kirjeldatud funktsionaalsus on esialgsest skoobist välja arvatud.

## Väljalülitamise ja sisselülitamise taotlus ja kinnitus

Väljalülitamise ja sisselülitamise taotluse ja kinnituse edastamiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

1. Avatud tarnija saadab välja- või sisselülitamise taotluse.
2. Andmeladu kontrollib, et määratud adressaadi ja saatja vahel on kehtiv (või on viimase 6 kuu jooksul olnud) ühisarve leping ning kas määratud kliendil selles mõõtepunktis on kehtiv avatud tarne leping saatjaga (või on olnud kehtiv viimase 12 kuu jooksul) ja kas määratud kliendi ja mõõtepunkti kombinatsioonil on kehtiv (või on olnud kehtiv viimase 12 kuu jooksul) võrguleping adresaadiga:
   - kui ei ole, siis Andmeladu vastab veateatega;
   - kui on, siis Andmeladu salvestab andmed andmebaasi ja teeb andmed kättesaadavaks võrguettevõtjale `changes` teenuse vahendusel.
3. Avatud tarnija vajadusel uuendab taotluse andmeid kasutades `PUT` teenust (selle teenusega saab ka tellimust tühistada).
4. Võrguettevõtja skaneerib välja- või sisselülitamise taotlusi kasutades teenust `changes`.
5. Võrguettevõtja lisab taotluse olekut kasutades teenust `connection-state/response`. Võimalikud variandid on:
   - mõõtepunkti välja- või sisselülitamise plaani võtmine;
   - mõõtepunkti välja- või sisselülitamisest keeldumine;
   - mõõtepunkti välja- või sisselülitamine.
6. Avatud tarnija skaneerib võrguettevõtja vastuseid kasutades teenust `changes`.
7. Võrguettevõtja uuendab taotluse olekut kasutades teenust `connection-state/response`. Võimalikud variandid on:
   - mõõtepunkti välja- või sisselülitamise plaani muutumine;
   - mõõtepunkti välja- või sisselülitamisest keeldumine;
   - mõõtepunkti välja- või sisselülitamine.
8. Avatud tarnija skaneerib võrguettevõtja vastuseid kasutades teenust `changes`.

### Masinliidese sõnumid

#### Sõnumid

| Sõnum                                           | Eesmärk                                                                      |
|-------------------------------------------------|------------------------------------------------------------------------------|
| `POST /api/{version}/connection-state`          | Võimaldab luua uut välja- või sisselülitamise taotlust                       |
| `PUT /api/{version}/connection-state`           | Võimaldab muuta või tühistada välja- või sisselülitamise taotlust            |
| `POST /api/{version}/connection-state/search`   | Võimaldab otsida välja- või sisselülitamise taotluse vastust                 |
| `POST /api/{version}/connection-state/response` | Võimaldab luua uut välja- või sisselülitamise taotluse vastust               |
| `PUT /api/{version}/connection-state/response`  | Võimaldab muuta välja- või sisselülitamise taotluse vastust                  |
| `POST /api/{version}/connection-state/changes`  | Võimaldab skaneerida välja- või sisselülitamise taotlusi või nende vastuseid |

#### Sõnumite reeglid

- Ühel välja- või sisselülitamise taotlusel saab olla ainult üks vastus. Vastuse muutumist tuleb väljendada vastuse muutmisega.
- Välja- või sisselülitamise taotlust on lubatud muuta seniks, kuni võrguettevõtja pole saatnud vastus lõppolekuga (CONNECTED, DISCONNECTED).

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)
