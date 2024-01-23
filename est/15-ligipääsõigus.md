# Ligipääsuõigus

## Sisukord

- [Ligipääsuõigus](#ligipääsuõigus)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Ligipääsuõiguste loomine ja pärimine](#ligipääsuõiguste-loomine-ja-pärimine)
    - [Veebiliides](#veebiliides)
    - [Masinliidese sõnumid](#masinliidese-sõnumid)
      - [Sõnumid](#sõnumid)
      - [Sõnumite reeglid](#sõnumite-reeglid)

## Sissejuhatus

Ligipääsuõigus antakse kliendi poolt avatud tarnijale või mõnele muule turuosalisele kliendiportaali vahendusel. Igal ligipääsuõigusel on oma kehtivusaeg ja ligipääsu ulatus.

Ligipääsuõigus laiendab turuosalise ligipääsu andmetele ja võimaldab pärida sellise mõõtepunkti- ja mõõteandmeid, mida muidu ei õnnestuks pärida.

## Ligipääsuõiguste loomine ja pärimine

Ligipääsuõiguse edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Klient siseneb kliendiportaali ja loob uue ligipääsuõiguse.
- Volitatud turuosaline skanneerib uusi ligipääsuõigusi kasutades teenust `data-distribution/search` või otsib spetsiifilisi ligipääsuõigusi kasutades teenust `search`.
- Volitatud turuosaline pärib mõõtepunkti ja tema mõõteandmeid kasutades `meter` ja `meter-data` teenuseid ligipääsuõiguses määratud mõõtepunkti EIC koodi alusel (ligipääsuõigust ei arvestata automaatses andmete levitamise protsessis).

### Veebiliides

> **Note**
> Veebiliides on loomisel.

### Masinliidese sõnumid

#### Sõnumid

| Sõnum                                        | Eesmärk                                        |
|----------------------------------------------|------------------------------------------------|
| `POST /api/{version}/customer-authorization` | Kliendiportaalis antud ligipääsuõiguste otsing |

Sõnumite struktuuride ja validatsioonide kirjelduste kohta loe dokumendist [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](01-avp-kirjeldus-ja-infovahetuse-yldpohimotted.md)

#### Sõnumite reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)
