# Äriprotsessid

## Sisukord

- [Äriprotsessid](#äriprotsessid)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Mõõtepunkti haldus](#mõõtepunkti-haldus)
    - [Mõõtepunkti registreerimine](#mõõtepunkti-registreerimine)
    - [Mõõtepunkti metaandmete uuendamine](#mõõtepunkti-metaandmete-uuendamine)
  - [Klientide haldus](#klientide-haldus)
    - [Kliendi registreerimine](#kliendi-registreerimine)
    - [Kliendi metaandmete uuendamine](#kliendi-metaandmete-uuendamine)
  - [Lepingute haldus](#lepingute-haldus)
    - [Võrgulepingu registreerimine](#võrgulepingu-registreerimine)
    - [Avatud tarne lepingu registreerimine](#avatud-tarne-lepingu-registreerimine)
    - [Üldteenuse lepingute genereerimine ja levitamine](#üldteenuse-lepingute-genereerimine-ja-levitamine)
    - [Kliendi arveldusandmete vahendamine võrguettevõtjalt nimetatud müüjale](#kliendi-arveldusandmete-vahendamine-võrguettevõtjalt-nimetatud-müüjale)
  - [Võrguühenduse välja- ja sisselülitamine](#võrguühenduse-välja--ja-sisselülitamine)
    - [Lahti ühendamine](#lahti-ühendamine)
    - [Sisse lülitamine](#sisse-lülitamine)
  - [Ühisarve haldus](#ühisarve-haldus)
    - [Ühisarve lisamine](#ühisarve-lisamine)
    - [Ühisarve muutmine](#ühisarve-muutmine)
  - [Võrguteenuse arve haldus](#võrguteenuse-arve-haldus)
    - [Võrguteenuse arve lisamine](#võrguteenuse-arve-lisamine)
    - [Võrguteenuse arve muutmine](#võrguteenuse-arve-muutmine)

## Sissejuhatus

Käesolev dokument kirjeldab peamisi Andmelaoga seotud äriprotsesse ja proovib seeläbi anda ülevaadet, kuidas erinevad masinliidese sõnumid äriprotsesside suhestuvad.

Diagrammid on koostatud selliselt, et keerukamad äriprotsessid taaskasutavad lihtsamaid äriprotsesse. Näiteks protsess "Võrgulepingu registreerimine" taaskasutab järgmisi olemasolevaid protsesse:

- Kliendi registreerimine
- Kliendi metaandmete uuendamine
- Mõõtepunkti registreerimine

Taaskasutatud protsesside tähis on diagrammidel järgmine:

![Taaskasutatava protsessi tähis](../diagrams/reusable-process-marking.png)

## Mõõtepunkti haldus

### Mõõtepunkti registreerimine

![Mõõtepunkti registreerimine](../diagrams/metering-point-management/mootepunkti-registreerimine.svg)

### Mõõtepunkti metaandmete uuendamine

![Mõõtepunkti metaandmete uuendamine](../diagrams/metering-point-management/mootepunkti-metaandmete-uuendamine.svg)

## Klientide haldus

### Kliendi registreerimine

![Kliendi registreerimine](../diagrams/customer-management/kliendi-registreerimine.svg)

### Kliendi metaandmete uuendamine

![Kliendi metaandmete uuendamine](../diagrams/customer-management/kliendi-metaandmete-uuendamine.svg)

## Lepingute haldus

### Võrgulepingu registreerimine

![Võrgulepingu registreerimine](../diagrams/agreement-management/v%C3%B5rgulepingu-registreerimine.svg)

### Avatud tarne lepingu registreerimine

![Avatud tarne lepingu registreerimine](../diagrams/agreement-management/avatud-tarne-lepingu-registreerimine.svg)

### Üldteenuse lepingute genereerimine ja levitamine

![Üldteenuse lepingute genereerimine ja levitamine](../diagrams/agreement-management/yldteenuse-lepingute-genereerimine-ja-levitamine.svg)

Alljärgnev diagram aitab paremini mõista protsessi, kuidas üldteenuse lepinguid genereeritakse:

![Täiendav diagramm](../diagrams/agreement-management/general-service-agreement-generation-additional-info.svg)

### Kliendi arveldusandmete vahendamine võrguettevõtjalt nimetatud müüjale

![Kliendi arveldusandmete vahendamine võrguettevõtjalt nimetatud müüjale](../diagrams/agreement-management/kliendi-arveldusandmete-vahetus.svg)

## Võrguühenduse välja- ja sisselülitamine

### Lahti ühendamine

![Lahti ühendamine](../diagrams/connection-state/lahti-yhendamine.svg)

### Sisse lülitamine

![Sisse lülitamine](../diagrams/connection-state/sisse-lylitamine.svg)

## Ühisarve haldus

### Ühisarve lisamine

![Ühisarve lisamine](../diagrams/joint-invoice/yhisarve-lisamine.svg)

### Ühisarve muutmine

*protsessi kirjeldus on loomisel*

## Võrguteenuse arve haldus

### Võrguteenuse arve lisamine

![Võrguteenuse arve lisamine](../diagrams/network-bill/vorguteenuse-arve-lisamine.svg)

### Võrguteenuse arve muutmine

![Võrguteenuse arve muutmine](../diagrams/network-bill/vorguteenuse-arve-muutmine.svg)