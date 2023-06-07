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

Ühisarve saatmise eelduseks on ühisarve leping Andmelaos. Loe täpsemalt dokumendist [Lepingud](05-lepingud.md).

Põhimõtteskeem võrguarve liikumiseks on järgmine: Võrguettevõtja > Andmeladu > Müüja > Klient

Vahendatava võrguarve rekvisiidid saadakse e-arve standardist ([Eesti e-arve kirjelduse juhend](https://media.voog.com/0000/0042/1620/files/Eesti_e-arve_kirjelduse_juhend_E_arve_saatmine%20ja%20presenteeerimine%20pangas_ver_1_0.pdf))

## Võrguarve edastamine

Võrguarvet on võimalik edastada nii masinliidese kui ka veebiliidese vahendusel (vorm väikestele võrguettevõtjatele) ning allalaadimiseks (müüjatele).

Võrguteenuse arve edastamiseks ja pärimiseks on loodud vastavad Andmelao teenused. Ettenähtud kasutamise protsess on järgmine:

- Võrguettevõtja saadab uue ühisarve võrguteenuse arve sõnumi kasutades teenust `forward-invoice`
- Andmeladu kontrollib, et määratud adressaadi ja saatja vahel on kehtiv ühisarve leping ning kas määratud kliendil selles mõõtepunktis on kehtiv avatud tarne leping arve adressaadiga.
  - Kui ei ole, siis Andmeladu vastab veateatega
  - Kui on, siis Andmeladu salvestab andmed andmebaasi ja teeb andmed kättesaadavaks avatud tarnijale `changes` teenuse vahendusel
- Avatud tarnija skaneerib võrguteenuste arvete muudatusi kasutades teenust `changes`
- Avatud tarnija laeb alla võrguteenuste arve kasutades teenust `download`
- Avatud tarnija kustutab kättesaadud võrguteenuste arve kasutades teenust `delete`

Võrguettevõtja või avatud tarnija võib kasutada `search` teenust Andmelattu salvestatud arvete otsimiseks

### Veebiliides

> **Note**
> Veebiliides on loomisel.

### Masinliidese sõnumid

#### Sõnumid

|Sõnum|Eesmärk|
|-----|-------|
|`POST /api/{version}/forward-invoice`|Võimaldab edastada ühisarve võrguarvet|
|`POST /api/{version}/forward-invoice/search`|Võimaldab otsida edastatud ühisarve võrguarveid|
|`POST /api/{version}/forward-invoice/download`|Võimaldab ühisarve võrguarvet alla laadida|
|`POST /api/{version}/forward-invoice/delete`|Võimaldab eemaldada eksliku või töödeldud võrguarve Andmelaost|
|`POST /api/{version}/forward-invoice/changes`|Võimaldab skaneerida võrguarvete muudatusi|

#### Sõnumite reeglid

> **Note**
> Andmete saatmise ja pärimise õigused on kirjeldatud dokumendis [Autentimine ja autoriseerimine](02-autentimine-ja-autoriseerimine.md)