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
    * [BHT raport](#bht-raport)
    * [Kohtloetavate mõõtepunktide raport](#Kohtloetavate-mõõtepunktide-raport)
    * [Kohtloetavate mõõtepunktide prognoosi raport](#Kohtloetavate-mõõtepunktide-prognoosi-raport)
    * [Võrguettevõtja klientide raport](#Võrguettevõtja-klientide-raport)
<!-- TOC -->

## Sissejuhatus

Andmeladu koostab regulaarselt avatud tarnijale, võrguettevõtjale ja bilansihaldurile suunatud raporteid.

## Raportite genereerimine

Koondraportid arvutatakse ja edastatakse järgmise ajakavaga:

- Elektriturul iga päev orienteeruvalt kella 14.00ks, Gaasiturul kella 18:00ks, eelmise päeva mõõteandmetega raportid (sh on mõõteandmeid kehtiva kalendrikuu algusest alates);
- Kalendrikuu 1. kuupäeval arvutatakse tagasiulatuvalt kaks kuud ja kolm kuud tagasi mõõteandmed kalendrikuu kohta;
- Kalendrikuu 8. kuupäeval (esimesel bilansiperioodil 00.00-01.00) arvutatakse eelmise kalendrikuu mõõteandmed, mis on aluseks esialgseks bilansiaruandeks.

Näide koondmõõteandmete arvutuse aegadest bilansiaruannete jaoks:

|                         | Jaanuari mõõteandmete koondraport | Veebruari mõõteandmete koondraport | Märtsi mõõteandmete koondraport |
|-------------------------|-----------------------------------|------------------------------------|---------------------------------|
| Esialgne bilansiaruanne | 08. veebr                         | 08. märts                          | 08. aprill                      |
| Lõplik bilansiaruanne   | 1. aprill                         | 1. mai                             | 1. juuni                        |

> [!NOTE]
> Raportid arvutatakse kõikidele elektrituru operaatoritele samal ajal ning kõikidele gaasituru operaatoritele samal ajal.  

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

|                                                                | Elekter                                | Gaas                                   |
|----------------------------------------------------------------|----------------------------------------|----------------------------------------|
| Kord ööpäevas toimub D+1 andmete agregeerimine                 | kell 10.00 (kättesaadav ca kell 14.00) | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine        | kell 00.00 (kättesaadav ca kell 10.00) | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine | kell 00.00 (kättesaadav ca kell 07.00) | kell 14.00 (kättesaadav ca kell 18.00) |

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
  - Võrku sisenenud kogus, M3 – võrguettevõtja võrku sisenenud kogus alam-võrguettevõtja võrgust (inQuantityM3) (ainult gaasiraportites)
  - Võrgust väljunud kogus, M3 – võrguettevõtja võrgust väljunud kogus alam-võrguettevõtja võrku (outQuantityM3) (ainult gaasiraportites)
  - Piirimõõtepunktide arv (meteringPointsTotal)
- **LEHT "GO OS OUT"**:
  - Võrguettevõtja EIC – võrguettevõtja EIC kood (gridOperatorEIC)
  - Võrguettevõtja – võrguettevõtja nimi (gridOperatorName)
  - Avatud tarnija EIC – võrgulepingu mõõtepunktis avatud tarnija EIC kood (openSupplierEIC)
  - Avatud tarnija – võrgulepingu mõõtepunktis avatud tarnija nimi (openSupplierName)
  - Avatud tarne lepungu tüüp - üldteenusel olek, kui on GENERAL_SERVICE, (supplyAgreementType)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Võrku sisenenud kogus, kWh – võrguettevõtja võrku sisenenud kogus mõõtepunktidest, kus on kehtiv võrguleping ja ei ole piiripunkt. Arvesse võetakse ka üldteenus. (Pin) (inQuantityPortfolio)
  - Võrgust väljunud kogus, kWh – võrguettevõtja võrgust väljunud kogus, kus on kehtiv võrguleping ja ei ole piiripunkt. Arvesse võetakse ka üldteenus. (Pout) (outQuantityPortfolio)
  - Võrku sisenenud kogus, M3 - gaasi kogus kuupmeetrites (ainult gaasiraportites)
  - Võrgust väljunud kogus, M3 - gaasi kogus kuupmeetrites (ainult gaasiraportites)
  - Mõõtepunktide arv, tk – võrgulepinguga mõõtepunktide arv (meteringPointsTotal)
- **LEHT "GO_IN_LOSSES_PORTFOLIO":**
  - Võrguettevõtja EIC – võrguettevõtja EIC kood (gridOperatorEIC)
  - Võrguettevõtja – võrguettevõtja nimi (gridOperatorName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - GO portfell kokku - kWh, Pin: Pin üldteenus +Pin GO müügileping (inQtyPortfolioGridOperator)
  - GO portfell kokku - kWh, Pout: Pout üldteenus+ Pout GO müügileping + Pout võrgukadu (outQtyPortfolioGridOperator)
  - Võrku sisenenud kogus (piirimõõtepunktid) - kWh, võrku sisenenud kogus ülemvõrguettevõtja võrgust kWh (inQuantityBorderPoints)
  - Võrgust väljunud kogus (piirimõõtepunktid) - kWh, võrgust väljunud kogus teistele võrguettevõtjatele (outQuantityBorderPoints)
  - GO võrgukadu - kWh (quantityLosses)
    - Arvutus: Ülemvõrguettevõtja piiripunktidest (Pin-Pout) – GO võrgu mõõtepunktid, kus on kehtiv võrguleping (Pout-Pin).
  - Ainult gaasiraportites:
    - GO portfelli tarbimine - kWh, (goPortfolioConsumption)
      - Arvutus: outQuantityPortfolioGridOperator + GO_OS_OUT.outQuantityPortfolio (üldteenuse kogused) + quantityLosses 
    - GO portfell kokku - M3, Pin: Pin üldteenus +Pin GO müügileping (inQtyPortfolioGridOperatorM3)
    - GO portfell kokku - M3, Pout: Pout üldteenus+ Pout GO müügileping + Pout võrgukadu (outQtyPortfolioGridOperatorM3)
    - Võrku sisenenud kogus (piirimõõtepunktid) - M3, võrku sisenenud kogus ülemvõrguettevõtja võrgust kWh (inQuantityBorderPointsM3)
    - Võrgust väljunud kogus (piirimõõtepunktid) - M3, võrgust väljunud kogus teistele võrguettevõtjatele (outQuantityBorderPointsM3)
    - GO portfelli tarbimine - M3 (goPortfolioConsumptionM3)
    - GO võrgukadu - M3 (quantityLossesM3)

### Avatud tarnija raport

Saajad:

- **Avatud tarnijad**

Sagedus:

|                                                                | Elekter                                | Gaas                                   |
|----------------------------------------------------------------|----------------------------------------|----------------------------------------|
| Kord ööpäevas toimub D+1 andmete agregeerimine                 | kell 10.00 (kättesaadav ca kell 14.00) | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine        | kell 00.00 (kättesaadav ca kell 10.00) | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine | kell 00.00 (kättesaadav ca kell 07.00) | kell 14.00 (kättesaadav ca kell 18.00) |

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
  - Võrku sisenenud kogus lõppkliendilt, M3 - (inQuantityPortfolioM3) (ainult gaasiturg)
  - Võrgust väljunud kogus lõppkliendile, M3 - (outQuantityPortfolioM3) (ainult gaasiturg)
  - Isoleeritud võrku sisenenud kogus lõppkliendilt, kWh –isoleeritud võrku sisenenud kogus Pin (kõik isoleeritud MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt) (inQuantityIsolated) (ainult elektriturg)
  - Isoleeritud võrgust väljunud kogus lõppkliendile, kWh – isoleeritud võrgust väljunud kogus Pout (kõik isoleeritud MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt) (outQuantityIsolated) (ainult elektriturg)
  - Mõõtepunktide arv, tk (meteringPointsTotal)

### Avatud tarnija koondraport

> [!WARNING] 
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

|                                                                | Elekter                                | Gaas                                   |
|----------------------------------------------------------------|----------------------------------------|----------------------------------------|
| Kord ööpäevas toimub D+1 andmete agregeerimine                 | kell 10.00 (kättesaadav ca kell 14.00) | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine        | kell 00.00 (kättesaadav ca kell 10.00) | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine | kell 00.00 (kättesaadav ca kell 07.00) | kell 14.00 (kättesaadav ca kell 18.00) |

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
  - Võrku sisenenud kogus, m³ – võrguettevõtja võrku sisenenud kogus ülem-võrguettevõtjalt (inQuantityM3) (ainult gaasiturg)
  - Võrgust väljunud kogus, m³ – võrguettevõtja võrgust väljunud kogus ülem-võrguettevõtja võrku (outQuantityM3) (ainult gaasiturg)
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
  - Võrku sisenenud kogus, m³ – võrguettevõtja võrku sisenenud kogus alam-võrguettevõtjalt (inQuantityM3) (ainult gaasiturg)
  - Võrgust väljunud kogus, m³ – võrguettevõtja võrgust väljunud kogus alam-võrguettevõtja võrku (outQuantityM3) (ainult gaasiturg)
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
  - Ainult gaasiraportites:
    - Võrku sisenenud kogus võrgulepinguga üldteenuse lõppkliendilt, m³ –võrku sisenenud kogus Pin (tootmine) (inQtyPortfolioLastResortSupplyM3)
    - Võrgust väljunud kogus võrgulepinguga üldteenuse lõppkliendile, m³ – võrguettevõtja võrgust väljunud kogus Pout (tarbimine) (outQtyPortfolioLastResortSupplyM3)
    - Võrku sisenenud kogus ülem-võrguettevõtja võrgust, m³  - Võrku sisenenud kogus ülem-võrguettevõtja võrgust, kWh – võrguettevõtja võrku sisenenud kogus piirimõõtepunktides (inQuantityBorderM3)
    - Võrgust väljunud kogus ülem-võrguettevõtja võrku, m³ – võrguettevõtja võrgust väljunud koguspiiripunktides (Pout) (outQuantityBorderM3)
    - Võrguettevõtja võrgukadu, m³ (qtyLossesM3)
    - Võrguettevõtja portfelli tarbimine, kWh (goPortfolioConsumption)
    - Võrguettevõtja portfelli tarbimine, m3 	(goPortfolioConsumptionM3)

### Bilansihalduse raport

Saajad:

- **Bilansihaldurid**

Sagedus:

|                                                                | Elekter                                | Gaas                                   |
|----------------------------------------------------------------|----------------------------------------|----------------------------------------|
| Kord ööpäevas toimub D+1 andmete agregeerimine                 | kell 10.00 (kättesaadav ca kell 14.00) | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine        | kell 00.00 (kättesaadav ca kell 10.00) | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine | kell 00.00 (kättesaadav ca kell 07.00) | kell 14.00 (kättesaadav ca kell 18.00) |

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
  - Portfelliväline võrku sisenenud kogus, M3 - gaasi kogus kuupmeetrites (inQuantityM3) (ainult gaasiturg)
  - Portfelliväline Võrgust väljunud kogus, M3 - gaasi kogus kuupmeetrites (outQuantityM3) (ainult gaasiturg) 
  - Portfelliväline isoleeritud võrku sisenenud kogus, kWh - Kõik turuosaliste isoleeritud mõõtepunktid, kus turuosalise mõõtepunkti BH erineb võrguettevõtja BHst. (inQuantityIsolated) (ainult elektriturg)
  - Portfelliväline isoleeritud võrgust väljunud kogus, kWh - Kõik turuosaliste isoleeritud mõõtepunktid, kus turuosalise mõõtepunkti BH erineb võrguettevõtja BHst. (outQuantityIsolated) (ainult elektriturg)
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
  - Võrku sisenenud kogus, M3 - gaasi kogus kuupmeetrites (inQuantityM3) (ainult gaasiturg)
  - Võrgust väljunud kogus, M3 - gaasi kogus kuupmeetrites (outQuantityM3) (ainult gaasiturg) 
  - Isoleeritud võrku sisenenud kogus, kWh - Kõik turuosaliste isoleeritud mõõtepunktid, mis on bilansiportfellis ning millede võrguettevõtja ei ole sama BH bilansiportfellis. (inQuantityIsolated) (ainult elektriturg)
  - Isoleeritud võrgust väljunud kogus, kWh - Kõik turuosaliste isoleeritud mõõtepunktid, mis on bilansiportfellis ning millede võrguettevõtja ei ole sama BH bilansiportfellis. (outQuantityIsolated) (ainult elektriturg)
  - Mõõtepunktide arv (meteringPointsTotal)

### Bilansihalduri raport No2 
### (ainult elektriturg) 

Saajad:

- **Bilansihaldurid**

Sagedus:

|                                                                | Elekter                                |
|----------------------------------------------------------------|----------------------------------------|
| Kord ööpäevas toimub D+1 andmete agregeerimine                 | kell 10.00 (kättesaadav ca kell 14.00) |
| Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine        | kell 00.00 (kättesaadav ca kell 10.00) |
| Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine | kell 00.00 (kättesaadav ca kell 07.00) |

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
  - BH portfellis võrgust väljunud kogus lõppkliendile, kWh – võrguettevõtja võrgust väljunud kogus Pout (kõik MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt (outQuantity))
  - BH portfellis isoleeritud võrku sisenenud kogus lõppkliendilt, kWh –võrku sisenenud kogus Pin (kõik isoleeritud MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt) (inQuantityIsolated)
  - BH portfellis isoleeritud võrgust väljunud kogus lõppkliendile, kWh – võrguettevõtja võrgust väljunud kogus Pout (kõik isoleeritud MPd, kus on kehtiv võrguleping ja punkt ei ole GO-GO piiripunkt (outQuantity))
  - Mõõtepunktide arv, tk (meteringPointsTotal)
- **LEHT "BH_GO_OS_GO"**
  - BH portfellis GO võrku sisenenud kogus võrgulepinguga üldteenuse lõppkliendilt, kWh –võrku sisenenud kogus Pin (tootmine) (inQtyPortfolioLastResortSupply)
  - BH portfellis GO võrgust väljunud kogus võrgulepinguga üldteenuse lõppkliendile, kWh – võrguettevõtja võrgust väljunud kogus Pout (tarbimine) (outQtyPortfolioLastResortSupply)
  - BH portfellis GO võrgukadu (qtyLosses)
  - Mõõtepunktide arv, tk (meteringPointsTotal)

### BHT raport

> [!NOTE]
> BHT raport on mõeldud Eleringile, kuid bilansihalduritel on ligipääs enda BHT raportitele

Saajad:

- **Bilansihaldurid**
- **Elering AS**

Sagedus:

|                                                                | Elekter                                | Gaas                                   |
|----------------------------------------------------------------|----------------------------------------|----------------------------------------|
| Kord ööpäevas toimub D+1 andmete agregeerimine                 | Ei koostata                            | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 8. kuupäeval toimub M+1 andmete agregeerimine        | kell 00.00 (kättesaadav ca kell 10.00) | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 1. kuupäeval toimub M+2 ja M+3 andmete agregeerimine | kell 00.00 (kättesaadav ca kell 07.00) | kell 14.00 (kättesaadav ca kell 18.00) |

Veergude kirjeldus:

BHT raporti väärtused tulenevad bilansihalduri raportist.

- **Leht "BMS_RAPORT"**
  - Bilansihalduri EIC – bilansihalduri EIC kood (balanceProviderEic)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Tootmine - Tootmine mõõtepunktides, mis on bilansihalduri portfellis, kuid võrguettevõtja ei ole samas portfellis. Sellest lahutatakse kogused, kus võrguettevõtja kuulub bilansihalduri portfelli, kuid avatud tarnija kuulub teise bilansihalduri portfelli. Arvesse võetakse ka isoleeritud mõõtepunktide kogused. (Portfolio Production)
  - Tarbimine - Tarbimine mõõtepunktides, mis on bilansihalduri portfellis, kuid võrguettevõtja ei ole samas portfellis. Sellest lahutatakse kogused, kus võrguettevõtja kuulub bilansihalduri portfelli, kuid avatud tarnija kuulub teise bilansihalduri portfelli. Arvesse võetakse ka isoleeritud mõõtepunktide kogused. (Portfolio Consumption)
  - Saldo - arvutatakse eelnevate veergude põhjal valemiga: Portfolio Production - Portfolio Consumption (Portfolio Saldo)
- **Leht "In_portfolio_production" (ainult gaasiturg)**
  - Bilansihalduri EIC – bilansihalduri EIC kood (balanceProviderEic)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Portfelli sisene tootmine - bilansihalduri portfelli sisene tootmine MWH (portfolioProduction)

### Kohtloetavate mõõtepunktide raport
### (ainult gaasiturg)

Saajad:

- **Bilansihaldurid**

Sagedus:

|                                                                    | Gaas                                   |
|--------------------------------------------------------------------|----------------------------------------|
| Kord kuus 28. kuupäeval. Raport koostatakse järgmise kuu kohta     | kell 01.30 (kättesaadav ca kell 10.00) |

**Leht "NON_REMOTE_READ_MP MM.YYYY"**
  - Mõõtepunkti EIC – kohtloetava mõõtepunkti EIC kood (meteringPointEIC)
  - Periood – tulba nimetaja on dünaamiline MM.YYYY (näiteks: 07.2026) ja näitab, millise kuu.aasta kohta raport on koostatud (MM.YYYY)
  - Kliendi EIC - kohtloetava mõõtepunkti kliendi (võrgulepingu klient) EIC kood (customerEIC)
  - Ühenduse olek - Mõõtepunkti ühenduse olek (kas on ühendatud või mitte). (connectionState)



### Kohtloetavate mõõtepunktide prognoosi raport
### (ainult gaasiturg)

Saajad:

- **Bilansihaldurid**

Sagedus:

|                                                                    | Gaas                                   |
|--------------------------------------------------------------------|----------------------------------------|
| Kord kuus 28. kuupäeval. Raport koostatakse järgmise kuu kohta     | kell 02.00 (kättesaadav ca kell 10.00) |

**Leht "FORECAST_DATA MM.YYYY"**
  - Võrguettevõtja EIC – kohtloetava mõõtepunkti võrguettevõtja EIC kood (gridOperatorEic)
  - Võrguettevõtja nimi - kohtloetava mõõtepunkti võrguettevõtja nimi (gridOperatorName)
  - Bilansiperiood – bilansiperioodi algust tähistav aeg (kuupäev + kellaaeg) (DateTime)
  - Võrku sisenenud kogus, kWh – võrguettevõtja võrku sisenenud kogus ülem-võrguettevõtjalt (inQuantityKwh)
  - Võrgust väljunud kogus, kWh – võrguettevõtja võrgust väljunud kogus ülem-võrguettevõtja võrku (outQuantityKwh)
  - Mõõtepunktide arv, tk (meteringPointsTotal)


  ### Võrguettevõtja klientide raport
  ### (ainult gaasiturg)

Saajad:

- **Võrguettevõtjad**

Sagedus:

|                                                                    | Gaas                                   |
|--------------------------------------------------------------------|----------------------------------------|
| Kord kuus 8. kuupäeval toimub M+1 raporti koostamine               | kell 14.00 (kättesaadav ca kell 18.00) |
| Kord kuus 1. kuupäeval toimub M+1, M+2 ja M+3 raporti koostamine   | kell 14.00 (kättesaadav ca kell 18.00) |

**Leht "GO_MP"**
  - Mõõtepunkti EIC – mõõtepunkti EIC kood (meteringPointEIC)
  - Gaasi müüja EIC - mõõtepunktis gaasi müüva turuosalise EIC (openSupplierEIC)
  - Kliendi EIC - mõõtepunkti kliendi EIC kood (customerEIC)
  - Kliendi nimi - mõõtepunkti kliendi nimi (customerName)
  - Katkestatud - kui perioodi jooksul on leping katkestatud, siis on 1, muidu 0 (Canceled)
  - Perioodi algus - jooksva kuu algus kell 07:00 või uue võrgulepingu korral lepingu alguskuupäev (periodStarts)
  - Perioodi lõpp - raporti koostamise kuupäev või jooksval kuu lõppenud võrgulepingu lõppkuuäev (periodEnds)
  - Tunnid – lepingu kehtivus tundides aruande kuus (hours)
  - Võrku sisenenud koguste edastuste arv  - loendatakse (count) kokku edastatud mõõteandmed (sh nullkogused) (inNumber)
  - Võrgust väljunud koguste edastaste arv - loendatakse (count) kokku edastatud mõõteandmed (sh nullkogused) (outNumber)
  - Tootmine m3 - võrku antud kuupmeetrid (inM3)
  - Tarbimine m3 - võrgust võetud kuupmeetrid (outM3)
  - Tootmine Kwh - võrku antud KWH (inkWh)
  - Tarbimine Kwh - võrgust võetud KWH (outkWh)


