# Raportid

## Sisukord

<!-- TOC -->
* [Raportid](#raportid)
  * [Sisukord](#sisukord)
  * [Sissejuhatus](#sissejuhatus)
  * [Raportite genereerimine](#raportite-genereerimine)
  * [Raportite edastamine](#raportite-edastamine)
    * [Masinliidese sõnumid](#masinliidese-sõnumid)
      * [Sõnumid](#sõnumid)
  * [Raportite kirjeldused](#raportite-kirjeldused)
    * [Võrguettevõtja raport](#võrguettevõtja-raport)
    * [Avatud tarnija raport](#avatud-tarnija-raport)
    * [Avatud tarnija koondraport](#avatud-tarnija-koondraport)
    * [Võrguettevõtja avatud tarnija raport](#võrguettevõtja-avatud-tarnija-raport)
    * [Bilansihalduse raport](#bilansihalduse-raport)
    * [Bilansihalduri raport No2](#bilansihalduri-raport-no2)
<!-- TOC -->

## Sissejuhatus

Andmeladu koostab regulaarselt avatud tarnijale, võrguettevõtjale ja bilansihaldurile suunatud raporteid.

## Raportite genereerimine

Koondraportid arvutatakse ja edastatakse järgmise ajakavaga:

- Iga päev kella 14.00ks eelmise päeva mõõteandmetega raportid (sh on mõõteandmeid kehtiva kalendrikuu algusest alates);
- Kalendrikuu 1. kuupäeval arvutatakse tagasiulatuvalt kaks kuud ja kolm kuud tagasi mõõteandmed kalendrikuu kohta;
- Kalendrikuu 8. kuupäeval (esimesel bilansiperioodil 00.00-01.00) arvutatakse eelmise kalendrikuu mõõteandmed, mis on aluseks esialgseks bilansiaruandeks.

Näide koondmõõteandmete arvutuse aegadest bilansiaruannete jaoks:

|                         | Jaanuari mõõteandmete koondraport | Veebruari mõõteandmete koondraport | Märtsi mõõteandmete koondraport |
|-------------------------|-----------------------------------|------------------------------------|---------------------------------|
| Esialgne bilansiaruanne | 08. veebr                         | 08. märts                          | 08. aprill                      |
| Lõplik bilansiaruanne   | 1. aprill                         | 1. mai                             | 1. juuni                        |

> **Note**
> Raportid arvutatakse kõikidele operaatoritele samal ajal

## Raportite edastamine

- Raportid on osapooltele kättesaadavad nii veebi- kui ka masinliidese vahendusel.
- Operaatoril on võimalik raporteid alla laadida järgmiselt:
  - Masinliidese vahendusel JSON või EXCEL formaadis
  - Veebiliidese vahendusel EXCEL formaadis
  
### Masinliidese sõnumid

#### Sõnumid

| Sõnum                                     | Eesmärk                                  |
|-------------------------------------------|------------------------------------------|
| `POST /api/{version}/report/search`       | Raportite otsing                         |
| `POST /api/{version}/report/export/excel` | MS Excel formaadis raporti allalaadimine |
| `POST /api/{version}/report/export/json`  | JSON formaadis raporti allalaadimine     |

## Raportite kirjeldused

Kõik raportid sisaldavad ühe kalendrikuu andmeid. Enamus raportid on koostatud bilansiperioodide lõikes. Eraldi on välja toodud tarbimine ja tootmine. Arvesse võetakse vaid kehtivate võrgulepingutega mõõtepunktide andmeid.

### Võrguettevõtja raport

Saajad:

- **Võrguettevõtjad**.

Sagedus:

- Kord ööpäevas toimub D+1 andmete agregeerimine kell 11.00 (saatmine kell 11.00).
- Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine kell 03.00 (saatmine kell 10.00).
- Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine kell 03.00 (saatmine kell 07.00).

Andmed:

- koondmõõteandmed võrguettevõtja piiripunktide kaudu võrku sisenenud kogus (raporti leht „GO_IN_LOSSES_PORTFOLIO“);
- võrguettevõtja võrgust väljunud kogused näidates eraldi summat:
  - avatud tarnijate lõikes lõppkogused - sisse ei arvutata piirimõõtepunkte, kus võrgulepingu kliendiks on teine võrguettevõtja + võrguettevõtja võrgukao mõõtepunkt. Avatud tarnijana on näidatud ka võrguettevõtja ise, kui ta tegutseb müüjana ja omab müügilepinguid turuosalistega (raporti leht „GO_OS_OUT“);
  - üldteenuse summa (tavalises mõõtepunktis võrguleping on, aga puudub müügileping) (raporti leht „GO_OS_OUT“);
  - võrguettevõtjate lõikes kogused– piirimõõtepunktide summa võrguettevõtjate lõikes (raporti leht „GO_GO_OUT“);
- võrguettevõtja võrgukadude arvutus: võrku sisenenud-võrgust väljunud kogused (raporti leht „GO_IN_LOSSES_PORTFOLIO“);
- võrguettevõtja oma portfelli agregeeritud summa = oma müügiportfell +üldteenus + võrgukaod (raporti leht „GO_IN_LOSSES_PORTFOLIO“);

Veergude kirjeldus:

- **LEHT "GO GO OUT"**:
  - Alam-võrguettevõtja EIC – alam-võrguettevõtja EIC kood (gridOperatorEIC)
  - Alam-võrguettevõtja – alam-võrguettevõtja nimi (gridOperatorName)
  - GO Avatud tarnija EIC – alam-võrguettevõtja avatud tarnija EIC kood (gridOperatorBalanceProviderEIC)
  - GO Avatud tarnija – alam-võrguettevõtja avatud tarnija nimi (gridOperatorBalanceProviderName)
  - võrguettevõtja EIC – võrguettevõtja EIC kood (parentGridProviderCustomerEIC)
  - Võrguettevõtja – võrguettevõtja nimi (parentGridProviderCustomerName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Võrku sisenenud kogus, kWh – võrguettevõtja võrku sisenenud kogus alam-võrguettevõtja võrgust (inQuantity)
  - Võrgust väljunud kogus, kWh – võrguettevõtja võrgust väljunud kogus alam-võrguettevõtja võrku (outQuantity)
  - Piirimõõtepunktide arv (meteringPointsTotal)
- **LEHT "GO OS OUT"**:
  - Võrguettevõtja EIC – võrguettevõtja EIC kood (gridOperatorEIC)
  - Võrguettevõtja – võrguettevõtja nimi (gridOperatorName)
  - Avatud tarnija EIC – võrgulepingu mõõtepunktis avatud tarnija EIC kood, üldteenuse korral „TÜHI“ (openSupplierEIC)
  - Avatud tarnija – võrgulepingu mõõtepunktis avatud tarnija nimi , üldteenuse korral „TÜHI“ (openSupplierName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Võrku sisenenud kogus, kWh – võrguettevõtja võrku sisenenud kogus mõõtepunktidest, kus on kehtiv võrguleping ja ei ole piiripunkt (Pin) (inQuantityPortfolio)
  - Võrgust väljunud kogus, kWh – võrguettevõtja võrgust väljunud kogus, kus on kehtiv võrguleping ja ei ole piiripunkt (Pout) (outQuantityPortfolio)
  - Mõõtepunktide arv, tk – võrgulepinguga mõõtepunktide arv (meteringPointsTotal)
- **LEHT "GO_IN_LOSSES_PORTFOLIO":**
  - Võrguettevõtja EIC – võrguettevõtja EIC kood (gridOperatorEIC)
  - Võrguettevõtja – võrguettevõtja nimi (gridOperatorName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - GO võrgukadu, kWh (qtyLosses)
    - Arvutus: Ülemvõrguettevõtja piiripunktidest (Pin-Pout) – GO võrgu mõõtepunktid, kus on kehtiv võrguleping (Pout-Pin).
  - GO portfell kokku kWh, Pin: Pin üldteenus +Pin GO müügileping (inQtyPortfolioGridOperator)
  - GO portfell kokku kWh, Pout: Pout üldteenus+ Pout GO müügileping + Pout võrgukadu (outQtyPortfolioGridOperator)

### Avatud tarnija raport

> **Warning**
> 
> Avatud tarnija ei ole esialgses skoobis

Saajad:

- **Avatud tarnijad**

Sagedus:

- Kord ööpäevas toimub D+1 andmete agregeerimine kell 11.00 (saatmine kell 11.00).
- Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine kell 03.00 (saatmine kell 10.00).
- Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine kell 03.00 (saatmine kell 07.00).

Andmed:

- Avatud tarne portfellis avatud tarnijate ja võrgupiirkonna lõikes agregeeritud kogused mõõtepunktide summas, mille kohta on olemas elektri avatud tarne leping - sisse ei arvutata piirimõõtepunkte, kus võrgulepingu kliendiks on teine võrguettevõtja.

Veergude kirjeldus:

- **LEHT "OS_GO"**:
  - Avatud tarnija EIC : kogu OS portfellis olevate avatud tarnijad, k.a tema ise (openSupplierEIC)
  - Avatud tarnija nimi - sama, mis ülemine (openSupplierName)
  - Võrguettevõtja EIC - mõõtepunkti võrguettevõtja EIC (gridOperatorEIC)
  - Võrguettevõtja nimi – mõõtepunkti võrguettevõtja nimi (gridOperatorName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Võrku sisenenud kogus lõppkliendilt, kWh –võrku sisenenud kogus Pin (kõik MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt) (inQuantityPortfolio)
  - Võrgust väljunud kogus lõppkliendile, kWh – võrguettevõtja võrgust väljunud kogus Pout (kõik MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt) (outQuantityPortfolio)
  - Isoleeritud võrku sisenenud kogus lõppkliendilt, kWh –isoleeritud võrku sisenenud kogus Pin (kõik isoleeritud MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt) (inQuantityIsolated)
  - Isoleeritud võrgust väljunud kogus lõppkliendile, kWh – isoleeritud võrgust väljunud kogus Pout (kõik isoleeritud MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt) (outQuantityIsolated)
  - Mõõtepunktide arv, tk (meteringPointsTotal)

### Avatud tarnija koondraport

> **Warning**
> 
> Avatud tarnija koondraport ei ole esialgses skoobis

Saajad:

- **Avatud tarnijad**

Sagedus:

- Arvutamise aja (päev ja kellaaeg) seadistab administraator – arvutatakse 1x kalendrikuu alguses eelmise kuu kohta.

Andmed:

Avatud tarne portfellis olevate avatud tarnijate kuised kogused mõõtepunktide ja klientide lõikes avatud tarne lepingute alusel.

Veergude kirjeldus:

- Iga mõõtepunkti kohta, millel on olemas kehtiv võrguleping, kalendrikuu andmed:
  - **LEHT "OS_CHAIN":**
    - Kliendi EIC - lõpptarbija EIC kood (customerEIC)
    - Mõõtepunkti EIC - lõpptarbija mõõtepunkti EIC kood (ei sisalda GO-GO punkte) (meteringPointEIC)
    - Avatud tarnija EIC – mõõtepunktis avatud tarnija EIC kood (openSupplierEIC)
    - Avatud tarnija nimi – mõõtepunktis avatud tarnija nimi (openSupplierName)
    - Võrguettevõtja EIC – mõõtepunkti võrguettevõtja EIC kood (gridOperatorEIC)
    - Võrguettevõtja nimi – mõõtepunkti võrguettevõtja nimi (gridOperatorName)
    - Avatud tarnija lepingu algus - mõõtepunktis avatud tarnija lepingu algus (osAgreementStart)
    - Avatud tarnija lepingu lõpp- mõõtepunktis avatud tarnija lepingu lõpp (osAgreementEnd)
    - Arvestusperiood – kalendrikuu (period)
    - Võrku sisenenud kogus lõppkliendilt, kWh (inQuantity)
    - Võrgust väljunud kogus lõppkliendile, kWh (outQuantity)

### Võrguettevõtja avatud tarnija raport

Saajad:

- **Võrguettevõtja avatud tarnija**

Sagedus:

- Kord ööpäevas toimub D+1 andmete agregeerimine kell 11.00 (saatmine kell 11.00).
- Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine kell 03.00 (saatmine kell 10.00).
- Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine kell 03.00 (saatmine kell 07.00).

Andmed:

- koondmõõteandmed võrguettevõtja piiripunktide kaudu võrku sisenenud kogus;
- võrguettevõtja võrgust väljunud kogused näidates eraldi summat:
  - avatud tarnijate summas lõppkogused mõõtepunktide summas, mille kohta on olemas elektri avatud tarne leping - sisse ei arvutata piirimõõtepunkte, kus võrgulepingu kliendiks on teine võrguettevõtja.
  - Üldteenus (tavalises mõõtepunktis võrguleping on, aga puudub müügileping).
  - Kliendiks teiste võrguettevõtjate summas kogus – piirimõõtepunktide summa võrguettevõtjatele (klient).
- Võrguettevõtja võrgukadu.

Veergude kirjeldus:

- **LEHT "GO_IN_BORDER_OS"**
  - Võrguettevõtja EIC – võrguettevõtja EIC kood (gridOperatorEIC)
  - Võrguettevõtja – võrguettevõtja nimi (gridOperatorName)
  - GO Avatud tarnija EIC – võrguettevõtja avatud tarnija EIC kood (gridOperatorBalanceProviderEIC)
  - GO Avatud tarnija – võrguettevõtja avatud tarnija nimi (gridOperatorBalanceProviderName)
  - Ülem-võrguettevõtja EIC – ülem-võrguettevõtja EIC kood (parentGridProviderCustomerEIC)
  - Ülem-Võrguettevõtja – ülem-võrguettevõtja nimi (parentGridProviderCustomerName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Võrku sisenenud kogus, kWh – võrguettevõtja võrku sisenenud kogus ülem-võrguettevõtjalt (inQuantity)
  - Võrgust väljunud kogus, kWh – võrguettevõtja võrgust väljunud kogus ülem-võrguettevõtja võrku (outQuantity)
  - Mõõtepunktide arv, tk (meteringPointsTotal)
- **LEHT "GO_OUT_BORDER_OS"**
  - Alam-võrguettevõtja EIC – alam-võrguettevõtja EIC kood (gridOperatorEIC)
  - Alam-Võrguettevõtja – alam-võrguettevõtja nimi (gridOperatorName)
  - GO Avatud tarnija EIC – ülem-võrguettevõtja avatud tarnija EIC kood (gridOperatorBalanceProviderEIC)
  - GO Avatud tarnija – ülem-võrguettevõtja avatud tarnija nimi (gridOperatorBalanceProviderName)
  - Võrguettevõtja EIC – võrguettevõtja EIC kood (parentGridProviderCustomerEIC)
  - Võrguettevõtja nimi – võrguettevõtja nimi (parentGridProviderCustomerName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Võrku sisenenud kogus, kWh – võrguettevõtja võrku sisenenud kogus alam-võrguettevõtjalt (inQuantity)
  - Võrgust väljunud kogus, kWh – võrguettevõtja võrgust väljunud kogus alam-võrguettevõtja võrku (outQuantity)
  - Mõõtepunktide arv, tk (meteringPointsTotal)
- **LEHT "GO_OS_GO"**
  - Võrguettevõtja EIC – võrguettevõtja EIC kood (gridOperatorEIC)
  - Võrguettevõtja – võrguettevõtja nimi (gridOperatorName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Võrku sisenenud kogus võrgulepinguga ja elektrilepinguga lõppkliendilt, kWh –võrku sisenenud kogus Pin (tootmine) (inQtyWithAgr)
  - Võrgust väljunud kogus võrgulepinguga ja elektrilepinguga lõppkliendile, kWh – võrguettevõtja võrgust väljunud kogus Pout (tarbimine) (outQtyWithAgr)
  - Võrku sisenenud kogus võrgulepinguga üldteenuse lõppkliendilt, kWh –võrku sisenenud kogus Pin (tootmine) (inQtyPortfolioLastResortSupply)
  - Võrgust väljunud kogus võrgulepinguga üldteenuse lõppkliendile, kWh – võrguettevõtja võrgust väljunud kogus Pout (tarbimine) (outQtyPortfolioLastResortSupply)
  - Võrku sisenenud kogus ülem-võrguettevõtja võrgust, kWh – võrguettevõtja võrku sisenenud kogus piirimõõtepunktides (inQuantityBorder)
  - Võrgust väljunud kogus ülem-võrguettevõtja võrku, kWh – võrguettevõtja võrgust väljunud koguspiiripunktides (Pout) (outQuantityBorder)
- Võrguettevõtja võrgukadu, kWh (qtyLosses)
- Piirimõõtepunktide arv, tk (meteringPointsTotalBorder)
- Mõõtepunktide arv, tk (meteringPointsTotal)

### Bilansihalduse raport

Saajad:

- **Bilansihaldurid**

Sagedus:

- Kord ööpäevas toimub D+1 andmete agregeerimine kell 11.00 (saatmine kell 11.00).
- Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine kell 03.00 (saatmine kell 10.00).
- Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine kell 03.00 (saatmine kell 07.00).

Andmed:

- Bilansihalduri + tema portfellis olevate avatud tarnijate bilansiselgituse mõõtepunktide koondandmed, mis arvatakse bilansihalduri bilansiselgituse piirkonda (nn IN mõõtepunktid);
- võrguettevõtja bilansihalduri bilansiselgituse portfellist maha arvutatud müük, gaasilepingud teiste bilansihaldurite portfellides (nn OUT piirimõõtepunktid).
- Leht „BP_OS“ = Bilansihalduri ja tema portfellis olevate avatud tarnijate bilansiselgituse mõõtepunktide koondandmed, mis arvatakse bilansihalduri bilansiselgituse piirkonda (nn IN bilansiselgituse mõõtepunktid);
- Leht „BP_GO“ = võrguettevõtja bilansihalduri bilansiselgituse portfellist maha arvutatud müük, gaasi müügilepingud teiste bilansihaldurite portfellides (nn OUT bilansiselgituse mõõtepunktid).

Veergude kirjeldus:

- **Leht "BH_GO"**
  - Võrguettevõtja EIC – võrguettevõtja EIC kood (gridOperatorEIC)
  - Võrguettevõtja – võrguettevõtja nimi (gridOperatorName)
  - Võrguettevõtja bilansihalduri EIC – võrguettevõtja bilansihalduri EIC kood (gridOperatorBalanceProviderEIC)
  - Võrguettevõtja bilansihalduri nimi – võrguettevõtja bilansihalduri nimi (gridOperatorBalanceProviderName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Portfelliväline võrku sisenenud kogus kWh – Tootmine, mis tuleb bilansiportfellist maha lahutada – bilansihalduri portfelli mittekuuluva turuosalise mõõtepunkti tootmine, Pin. Kõik turuosaliste mõõtepunktid, k.a võrguettevõtja piirimõõtepunktid, kus turuosalise mõõtepunkti BH erineb võrguettevõtja BHst. (inQuantity)
  - Portfelliväline võrgust väljunud kogus kWh - Tarbimine, mis tuleb bilansiportfellist maha lahutada – bilansihalduri portfelli mittekuuluva turuosalise mõõtepunkti tarbimine, Pout. Kõik turuosaliste mõõtepunktid, k.a võrguettevõtja piirimõõtepunktid, kus turuosalise mõõtepunkti BH erineb võrguettevõtja BHst. (outQuantity)
  - Portfelliväline isoleeritud võrku sisenenud kogus kWh. Kõik turuosaliste isoleeritud mõõtepunktid, kus turuosalise mõõtepunkti BH erineb võrguettevõtja BHst. (inQuantityIsolated)
  - Portfelliväline isoleeritud võrgust väljunud kogus kWh. Kõik turuosaliste isoleeritud mõõtepunktid, kus turuosalise mõõtepunkti BH erineb võrguettevõtja BHst. (outQuantityIsolated)
  - Mõõtepunktide arv, tk (meteringPointsTotal)
- **Leht "BH_OS"**
  - Bilansihalduri EIC – bilansihalduri EIC kood (openSupplierBalanceProviderEIC)
  - Bilansihaldur – bilansihalduri nimi (openSupplierBalanceProviderName)
  - Avatud tarnija EIC – avatud tarnija EIC kood (openSupplierEIC)
  - Avatud tarnija – avatud tarnija nimi (openSupplierName)
  - Võrguettevõtja EIC – võrguettevõtja EIC kood (gridOperatorEIC)
  - Võrguettevõtja – võrguettevõtja nimi (gridOperatorName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Võrku sisenenud kogus, kWh – bilansihalduri portfelli kuuluva turuosalise mõõtepunkti tootmine, Pin. Kõik turuosaliste mõõtepunktid, k.a võrguettevõtja piirimõõtepunktid, mis on bilansiportfellis ning millede võrguettevõtja ei ole sama BH bilansiportfellis. (inQuantity)
  - Võrgust väljunud kogus, kWh – bilansihalduri portfelli kuuluva turuosalise mõõtepunkti tarbimine, Pout. Kõik turuosaliste mõõtepunktid, k.a võrguettevõtja piirimõõtepunktid, mis on bilansiportfellis ning millede võrguettevõtja ei ole sama BH bilansiportfellis. (outQuantity)
  - Isoleeritud võrku sisenenud kogus, kWh. Kõik turuosaliste isoleeritud mõõtepunktid, mis on bilansiportfellis ning millede võrguettevõtja ei ole sama BH bilansiportfellis. (inQuantityIsolated)
  - Isoleeritud võrgust väljunud kogus, kWh. Kõik turuosaliste isoleeritud mõõtepunktid, mis on bilansiportfellis ning millede võrguettevõtja ei ole sama BH bilansiportfellis. (outQuantityIsolated)
  - Mõõtepunktide arv (meteringPointsTotal)

### Bilansihalduri raport No2

Saajad:

- **Bilansihaldurid**

Sagedus:

- Kord ööpäevas toimub D+1 andmete agregeerimine kell 11.00 (saatmine kell 11.00).
- Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine kell 03.00 (saatmine kell 10.00).
- Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine kell 03.00 (saatmine kell 07.00).

Andmed:

- Leht „BH_OS_GO“ – bilansihalduri ja tema portfellis olevate avatud tarnijate kogused võrguettevõtjate võrgupiirkondade lõikes.
- Leht „BH_GO_OS_GO“ – bilansihalduri portfellis olevate võrguettevõtjate üldteenusel olevate klientide kogused ning võrgukadude kogused.

Veergude kirjeldus:

- Bilansiportfellis avatud tarnijate koondmõõteandmed näidates eraldi summat:
  - portfellis avatud tarnijate (k.a bilansihaldur ise) ja võrgupiirkonna lõikes agregeeritud kogused mõõtepunktide summas, mille kohta on olemas elektri avatud tarne leping - sisse ei arvutata piirimõõtepunkte, kus võrgulepingu kliendiks on teine võrguettevõtja.
  - portfellis võrguettevõtja portfell üldteenuse ja võrgukadude lõikes eraldi näidatuna;
- **LEHT "BH_OS_GO"**
  - Avatud tarnija EIC - BH portfellis olevad avatud tarnijad mõõtepunkti kohta (openSupplierEIC)
  - Avatud tarnija nimi: sama mis eelmine, aga nimi (openSupplierName)
  - Võrguettevõtja EIC – võrguettevõtja EIC kood mõõtepunktis (gridOperatorEIC)
  - Võrguettevõtja – võrguettevõtja nimi mõõtepunktis (gridOperatorName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - BH portfellis võrku sisenenud kogus lõppkliendilt, kWh –võrku sisenenud kogus Pin (kõik MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt) (inQuantity)
  - BH portfellis võrgust väljunud kogus lõppkliendile, kWh – võrguettevõtja võrgust väljunud kogus Pout (kõik MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt (outQuantity)
  - BH portfellis isoleeritud võrku sisenenud kogus lõppkliendilt, kWh –võrku sisenenud kogus Pin (kõik isoleeritud MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt) (inQuantityIsolated)
  - BH portfellis isoleeritud võrgust väljunud kogus lõppkliendile, kWh – võrguettevõtja võrgust väljunud kogus Pout (kõik isoleeritud MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt (outQuantity)
  - Mõõtepunktide arv, tk (meteringPointsTotal)
- **LEHT "BH_GO_OS_GO"**
  - BH portfellis GO võrku sisenenud kogus võrgulepinguga üldteenuse lõppkliendilt, kWh –võrku sisenenud kogus Pin (tootmine) (inQtyPortfolioLastResortSupply)
  - BH portfellis GO võrgust väljunud kogus võrgulepinguga üldteenuse lõppkliendile, kWh – võrguettevõtja võrgust väljunud kogus Pout (tarbimine) (outQtyPortfolioLastResortSupply)
  - BH portfellis GO võrgukadu (qtyLosses)
  - Mõõtepunktide arv, tk (meteringPointsTotal)
