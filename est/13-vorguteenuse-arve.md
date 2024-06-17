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
- Andmeladu salvestab võrguteenuse arve andmebaasi
- Avatud tarnija otsib uusi võrguarveid kasutades teenust `search`

Võrguteenuse arve andmete muutmiseks, tuleb saata uus `network-bill` sõnum parandatud andmetega sama perioodi kohta ning väärtustada atribuut `calculationTimestamp` uuema väärtusega.

## Masinliidese sõnumid

### Sõnumid

| Sõnum                                     | Eesmärk                    |
|-------------------------------------------|----------------------------|
| `POST /api/{version}/network-bill`        | Võrguteenuse arve lisamine |
| `POST /api/{version}/network-bill/search` | Võrguteenuse arve otsing   |

Sõnumite struktuuride ja validatsioonide kirjelduste kohta loe dokumendist [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](01-avp-kirjeldus-ja-infovahetuse-yldpohimotted.md)

> **Note**
> Sõnumite näidiste kogumik on loomisel

### Sõnumite reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](03-autentimine-ja-autoriseerimine.md)


- Võrguarve edastamise reeglid:
  - Võrguarvet saab lisada võrguettevõtja (GO) või suletud jaotusvõrgu ettevõtja (CDN)
  - Võrguarve `periodStart` ei tohi olla väiksem, kui võrgulepingu kehtivuse algus
  - Võrguarve `periodEnd` ei tohi olla suurem, kui võrgulepingu kehtivuse lõpp
  - Maksimaalne võrguarve koostamise periood on üks kuu.
  - Perioodi alguse ja lõpu kuu väärtus peab olema võrdne (juhul, kui avatud tarnija ei vahetu kuu vahetusel, siis võrguettevõtja peab edastama 2 eraldi võrguteenuse arvet).
- Juhul kui turuosaline kasutab üldteenust, on võrguteenuste arve edastamine Andmelattu vabatahtlik.
- Võrguarvete otsimise reeglid:
  - võrguettevõtja (GO) ja suletud jaotusvõrgu ettevõtja (CDN) saavad otsida ainult neid võrguarveid, mida nad ise lisasid
  - avatud tarnija saab otsida neid võrguarveid, kus `periodStart` ja `periodEnd` on kaetud sellise avatud tarne lepinguga, kus avatud tarnija on teenusepakkuja.
