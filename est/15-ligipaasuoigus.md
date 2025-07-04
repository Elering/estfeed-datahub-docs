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

Ligipääsuõigus laiendab turuosalise ligipääsu andmetele ja võimaldab pärida selliseid andmeid, mida muidu ei õnnestuks pärida.

## Ligipääsuõiguste loomine ja pärimine

Ligipääsuõiguse edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Klient siseneb kliendiportaali ja loob uue ligipääsuõiguse.
- Volitatud turuosaline skanneerib uusi ligipääsuõigusi kasutades andmete levitamise teenust või otsib spetsiifilisi ligipääsuõigusi kasutades teenust `customer-authorization/search`.
- Volitatud turuosaline pärib järgmisi andmeid:
  - kliendi andmed - kirjeldatud dokumendis [Kliendid](04-kliendi-eic.md);
  - mõõtepunkti andmed - kirjeldatud dokumendis [Mõõtepunktid](05-mootepunktid.md);
  - mõõteandmed - kirjeldatud dokumendis [Mõõteandmed](12-mooteandmed.md).

### Veebiliides

> [!NOTE]
> Veebiliides on loomisel.

### Masinliidese sõnumid

#### Sõnumid

| Sõnum                                               | Eesmärk                                        |
|-----------------------------------------------------|------------------------------------------------|
| `POST /api/{version}/customer-authorization/search` | Kliendiportaalis antud ligipääsuõiguste otsing |
