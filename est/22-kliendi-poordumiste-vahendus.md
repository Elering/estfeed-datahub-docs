# Kliendi pöördumiste vahendus

> [!WARNING] 
> Konsultatsioonid turuosalistega selle teenuste paketi realiseerimise üle alles käivad. Allpool olev kirjeldus on kõigest esialgne nägemus.

## Sisukord

- [Kliendi pöördumiste vahendus](#kliendi-pöördumiste-vahendus)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Kliendi pöördumise edastamine ja vastamine](#kliendi-pöördumise-edastamine-ja-vastamine)
    - [Veebiliides](#veebiliides)
    - [Masinliidese sõnumid](#masinliidese-sõnumid)
      - [Sõnumid](#sõnumid)
      - [Sõnumite reeglid](#sõnumite-reeglid)

## Sissejuhatus

Kliendi pöördumiste vahenduse protsessi eesmärk on klientide võrguteenusega seotud pöördumiste vahendamine müüjalt võrguettevõtjale. Kliendi pöördumiste vahendus on kasutatav vaid müüja ja võrguettevõtja vaheliste sõnumitena. Kliendi pöördumiste funktsionaalsus sisaldab võrguettevõtjate ja müüjate omavahelist infovahetust standardiseeritud kujul.

> [!WARNING] 
> Kogu käesolevas dokumendis kirjeldatud funktsionaalsus on esialgsest skoobist välja arvatud.

## Kliendi pöördumise edastamine ja vastamine

Pöördumisi on võimalik edastada ja vaadata nii masin- kui ka veebiliidese vahendusel.

Pöördumiste edastamiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Avatud tarnija saadab kliendi pöördumise info kasutades teenust `direct-messages`.
- Andmeladu salvestab pöördumise ja teeb selle kättesaadavaks võrguettevõtjale `TODO` teenuse vahendusel.
- Võrguettevõtja skaneerib `TODO` teenust ja saab uued või muutunud pöördumised.
- Võrguettevõtja saadab pöördumisele vastuse kasutades teenust `response`.
- Andmeladu salvestab vastuse ja teeb selle kättesaadavaks avatud tarnijale `TODO` teenuse vahendusel.
- Avatud tarnija skaneerib `TODO` teenust ja saab uued või muutunud vastused.

Võrguettevõtja või avatud tarnija võib kasutada `search` teenust Andmelattu salvestatud pöördumiste ja vastuste otsimiseks.

### Veebiliides

> [!NOTE]
> Veebiliides on loomisel

### Masinliidese sõnumid

#### Sõnumid

| Sõnum                                          | Eesmärk                                                                                  |
|------------------------------------------------|------------------------------------------------------------------------------------------|
| `POST /api/{version}/direct-messages`          | Võimaldab registreerida uue kliendi pöördumise                                           |
| `PUT /api/{version}/direct-messages`           | Võimaldab muuta olemasoleva kliendi pöördumise andmeid. Või tühistada kliendi pöördumise |
| `POST /api/{version}/direct-messages/search`   | Võimaldab otsida kliendi pöördumisi ja tagasisidet                                       |
| `POST /api/{version}/direct-messages/response` | Võimaldab registreerida uue kliendi pöördumise tagasiside                                |
| `PUT /api/{version}/direct-messages/response`  | Võimaldab muuta olemasoleva kliendi pöördumise tagasiside andmeid                        |

#### Sõnumite reeglid

- Pöördumise adressaati Andmeladu ei valideeri. Õigete andmete väärtustamise eest vastutab avatud tarnija.
