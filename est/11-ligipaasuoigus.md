# Ligipääsuõigus

## Sisukord

- [Ligipääsuõigus](#ligipääsuõigus)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Ligipääsuõiguse andmete edastamine ja pärimine](#ligipääsuõiguse-andmete-edastamine-ja-pärimine)
  - [Masinliidese sõnumid](#masinliidese-sõnumid)
    - [Sõnumid](#sõnumid)
    - [Sõnumi reeglid](#sõnumi-reeglid)

## Sissejuhatus

Kliendiportaal asub aadressil [https://estfeed.elering.ee](https://estfeed.elering.ee)

Turuosalised saavad kliendiportaali kaudu anda ligipääsuõigusi avatud tarnijatele mõõtepunktide detailide ja eelmiste perioodide mõõteandmete nägemiseks. Seda eelkõige eesmärgiga saada avatud tarnijatelt personaalseid pakkumisi.

Andmetele ligipääsu õigus võib tuleneda ka seadusest.

## Ligipääsuõiguse andmete edastamine ja pärimine

Ligipääsuõiguse andmete edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

1. Turuosaline lisab uue ligipääsuõiguse kasutades Kliendiportaali funktsionaalsust
2. Andmeladu salvestab uue ligipääsuõiguse oma andmebaasi ja määrab avatud tarnija, kellele see kättesaadavaks tehakse
3. Avatud tarnija skaneerib `changes` teenust ning tuvastab, et talle on adresseeritud uus ligipääsuõigus
4. Pärast ligipääsuõiguse andmist võib avatud tarnija kasutada sõnumeid andmete pärimiseks:
   - kliendi andmed - kirjeldatud dokumendis [Kliendid](03-kliendi-eic.md)
   - mõõtepunkti andmed - kirjeldatud dokumendis [Mõõtepunktid](04-mootepunktid.md)
   - mõõteandmed - kirjeldatud dokumendis [Mõõteandmed](07-mooteandmed.md)

## Masinliidese sõnumid

### Sõnumid

| Sõnum | Eesmärk |
|-------|---------|
| `POST /api/{version}/customer-authorization/search` | Võimaldab otsida ligipääsuõigusi |
| `POST /api/{version}/customer-authorization/changes` | Võimaldab skaneerida ligipääsuõiguste uuendusi |

### Sõnumi reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)

- Igal ligipääsuõigusel on algus- ja lõppaeg. Etteantuna on kehtivusaeg 48h, mida ligipääsuõiguse andja saab vähendada.
- Iga ligipääsuõigus sisaldab konkreetset andmete töötlemise eesmärki ja kes on andmete vastutav töötleja
- Avatud tarnija ei näe kliendi ligipääsuõigusi teistele avatud tarnijatele.
