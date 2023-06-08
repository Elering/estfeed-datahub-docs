# Võrguteenuse arve

## Sisukord

- [Võrguteenuse arve](#võrguteenuse-arve)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Võrguteenuse arve edastamine ja pärimine](#võrguteenuse-arve-edastamine-ja-pärimine)
  - [Masinliidese sõnumid](#masinliidese-sõnumid)
    - [Sõnumid](#sõnumid)
    - [Sõnumite reeglid](#sõnumite-reeglid)

## Sissejuhatus

Võrguteenuse koostamise sõnum abil edastab võrguettevõtja info selle kohta, millisel hetkel ja milliste andmete alusel koostas võrguettevõtja kliendile võrguteenuse arve. Antud sõnumis olev info võimaldab müüjatel esitada klientidele müügiarve samade energiakoguste eest nagu võrguteenuse arve. Andmeladu edastab võrguettevõtja saadetud sõnumi mõõtepunkti avatud tarnijale.

> **Warning**
> 
> Andmeladu ei vastuta sõnumis toodud energiakoguste andmete kvaliteedi eest

## Võrguteenuse arve edastamine ja pärimine

Võrguteenuse arve edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Võrguettevõtja saadab uue või muutunud võrguteenuse arve sõnumi kasutades teenust `network-bill`.
- Võrguettevõtja kustutab vajadusel eksliku arve kasutades teenust `delete`.
- Avatud tarnija skaneerib võrguteenuste arvete muudatusi kasutades teenust `changes`.
- Avatud tarnija kustutab kättesaadud võrguteenuste arve kasutades teenust `delete`.

Võrguettevõtja või avatud tarnija võib kasutada `search` teenust Andmelattu salvestatud arvete otsimiseks.

## Masinliidese sõnumid

### Sõnumid

| Sõnum                                      | Eesmärk                                                        |
|--------------------------------------------|----------------------------------------------------------------|
| `POST /api/{version}/network-bill`         | Võimaldab registreerida uut võrguarvet.                        |
| `PUT /api/{version}/network-bill`          | Võimaldab uuendada olemasoleva võrguarve andmeid.              |
| `POST /api/{version}/network-bill/search`  | Võimaldab otsida registreeritud võrguarvet.                    |
| `POST /api/{version}/network-bill/changes` | Võimaldab skaneerida võrguarvete muudatusi                     |
| `POST /api/{version}/network-bill/delete`  | Võimaldab eemaldada eksliku või töödeldud võrguarve Andmelaost |

Sõnumite struktuuride ja validatsioonide kirjeldused on leitavad [Swagger](https://test-datahub.elering.ee/swagger-ui/index.html) keskkonnast.

> **Note**
> Sõnumite näidiste kogumik on loomisel

### Sõnumite reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)

- Maksimaalne võrguarve koostamise periood on üks kuu.
- Perioodi alguse ja lõpu kuu väärtus peab olema võrdne (juhul, kui avatud tarnija ei vahetu kuu vahetusel, siis võrguettevõtja peab edastama 2 eraldi võrguteenuse arvet).
- Juhul kui turuosaline kasutab üldteenust, on võrguteenuste arve edastamine Andmelattu vabatahtlik.
