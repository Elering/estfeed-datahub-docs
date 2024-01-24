# Ühisarve

## Sisukord

- [Ühisarve](#ühisarve)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Võrguarve edastamine](#võrguarve-edastamine)
    - [Veebiliides](#veebiliides)
    - [Masinliidese sõnumid](#masinliidese-sõnumid)
      - [Sõnumid](#sõnumid)
      - [Sõnumite reeglid](#sõnumite-reeglid)

## Sissejuhatus

Ühisarve saatmise eelduseks on ühisarve leping Andmelaos. Loe täpsemalt dokumendist [Lepingud](06-lepingud.md).

Põhimõtteskeem võrguarve liikumiseks on järgmine: Võrguettevõtja > Andmeladu > Müüja > Klient.

Vahendatava võrguarve rekvisiidid saadakse e-arve standardist ([Eesti e-arve kirjelduse juhend](https://media.voog.com/0000/0042/1620/files/Eesti_e-arve_kirjelduse_juhend_E_arve_saatmine%20ja%20presenteeerimine%20pangas_ver_1_0.pdf)).

## Võrguarve edastamine

Võrguarvet on võimalik edastada nii masinliidese kui ka veebiliidese vahendusel (vorm väikestele võrguettevõtjatele) ning allalaadimiseks (müüjatele).

Võrguteenuse arve edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Võrguettevõtja saadab uue ühisarve võrguteenuse arve sõnumi kasutades teenust `joint-invoice`.
- Andmeladu kontrollib, et:
  - määratud adressaadi ja saatja vahel on kehtiv ühisarve leping ning
  - määratud kliendil on selles mõõtepunktis kehtiv avatud tarne leping arve adressaadiga ning
  - määratud kliendil on selles mõõtepunktis kehtiv võrguleping arve saatjaga.
- Kui tingimused ei ole täidetud, siis Andmeladu vastab veateatega.
- Kui tingimused on täidetud, siis Andmeladu salvestab andmed andmebaasi.
- Avatud tarnija või võrguettevõtja otsib võrguteenuste arveid  kasutades teenust `search`.
- Avatud tarnija või võrguettevõtja laeb alla võrguteenuste arve kasutades teenust `download`.

### Veebiliides

> **Note**
> Veebiliides on loomisel.

### Masinliidese sõnumid

#### Sõnumid

| Sõnum                                        | Eesmärk                           |
|----------------------------------------------|-----------------------------------|
| `POST /api/{version}/joint-invoice`          | Ühisarve võrguarve lisamine       |
| `POST /api/{version}/joint-invoice/search`   | Ühisarve võrguarve otsing         |
| `POST /api/{version}/joint-invoice/download` | Ühisarve võrguarve alla laadimine |

Sõnumite struktuuride ja validatsioonide kirjelduste kohta loe dokumendist [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](01-avp-kirjeldus-ja-infovahetuse-yldpohimotted.md)

#### Sõnumite reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](03-autentimine-ja-autoriseerimine.md)
