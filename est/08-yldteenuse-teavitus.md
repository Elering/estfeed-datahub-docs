# Üldteenuse teavitus

## Sisukord

<!-- TOC -->
* [Üldteenuse teavitus](#üldteenuse-teavitus)
  * [Sisukord](#sisukord)
  * [Sissejuhatus](#sissejuhatus)
  * [Üldteenuse teavituse sõnumid](#üldteenuse-teavituse-sõnumid)
<!-- TOC -->

## Sissejuhatus

Andmeladu tuvastab perioodid, millal klient kasutab või hakkab kasutama üldteenust. Nendest perioodidest tuvastab Andmeladu alamperioodid, mis on kaetud nimetatud müüja lepinguga. 
Tuvastatud (alam)perioodide kohta koostab Andmeladu tehnilised üldteenuse (`GENERAL_SERVICE`) lepingud ja määrab teenusepakkujaks kas võrguettevõtja või nimetatud müüja:

![yldteenus.svg](../diagrams/general-service/yldteenus.svg)

Tegemist on puhtalt tehnilise lahendusega, et üldteenuse algust ja lõppu eksplitsiitselt talletada. Tegemist ei ole juriidilises mõttes lepinguga.

Andmeladu teeb üldteenuse lepingud kättesaadavaks võrguettevõtjale ja nimetatud müüjale andmete levitamise teenuse abil vahetult pärast selle aktiveerumist. **Tulevikus kehtima hakkavaid üldteenuse lepinguid ei levitata** ning samuti pole need leitavad tavaliste lepingute otsingutega. Loe täpsemalt GENERAL_SERVICE lepingute levitamisest lehelt [Andmete levitamine](30-andmete-levitamine.md)

> [!NOTE]
> Andmeladu ei hoia GENERAL_SERVICE lepingute muudatusi. Muudatuste puhul vanad lepingud kustutatakse ja luuakse uued.

Üldteenuse rakendumisel sõltub edasine andmevahetuse sellest, kas võrguettevõtjal on sõlmitud nimetatud tarnija leping või mitte:

- Kui ei ole, siis täiendavat andmevahetust pole ette nähtud.
- Kui on, siis Andmeladu võimaldab võrguettevõtjal ja nimetatud müüjal vahetada kliendi meta- ja arveldusandmete uuendusi kasutades teenust `PUT customer`

> [!NOTE]
> Tasub tähele panna, et antud protsessis on Andmeladu lihtsalt sõnumivahendaja ning kliendi täiendavate metaandmete edastamine on vabatahtlik.

## Üldteenuse teavituse sõnumid

Kuivõrd üldteenuse lepingute puhul ei toimu muudatuste tuvastamist, siis ka andmete levitamise kanalis puuduvad üldteenuse lepingute puhul sõnumid, kus atribuudi `reason` väärtus oleks `UPDATE`. Eksisteerivad ainult väärtused `CREATE` ja `DELETE`.

**Näide "Uus GRID leping":**

- GO loob uue GRID lepingu
- Kui GRID lepingu alguskuupäev on tulevikus, siis GENERAL_SERVICE lepingu teavitust ei järgne
- Kui GRID lepingu alguskuupäev on täna või minevikus, siis GO saab GENERAL_SERVICE lepingu teavituse, kus:
  - `reason` väärtus on `CREATE`
  - `validFrom` ja `validTo` väärtused on GRID lepingu `validFrom` ja `validTo` väärtustega identsed (kuna puuduvad SUPPLY lepingud)

Joonis:

![general-service-ex-1-est.svg](../diagrams/general-service/general-service-ex-1-est.svg)

**Näide "Uus SUPPLY leping, mille algus on minevikus ja lõpp tulevikus või puudub":**

Käesolev näide illustreerib SUPPLY lepingu ärireeglit: "Lepingu alguskuupäev tohib olla kuni 48h minevikus juhul, kui avatud tarnija registreerib avatud tarne lepingut tagantjärele ja lepingu alguskuupäev langeb kokku võrgulepingu alguskuupäevaga."

- Kliendil on mõõtepunktis hetkel kehtivad GRID ja GENERAL_SERVICE lepingud
- OS loob uue SUPPLY lepingu, mille `validFrom` on minevikus ja langeb kokku GRID lepingu `validFrom` väärtusega ning mille `validTo` on tulevikus või puudub
- Andmeladu tuvastab, et eelnevalt loodud GENERAL_SERVICE leping ei ole enam valiidne ja kustutab selle
- GO saab GENERAL_SERVICE lepingu teavituse, kus:
  - `reason` väärtus on `DELETE`
  - `validFrom` ja `validTo` väärtused on identsed eelmise teavitusega (see võimaldab GO-l GENERAL_SERVICE leping üles leida)

Joonis:

![general-service-ex-2-est.svg](../diagrams/general-service/general-service-ex-2-est.svg)

**Näide "Uus SUPPLY leping, mille algus ja lõpp on tulevikus":**

- Kliendil on mõõtepunktis hetkel kehtivad GRID ja GENERAL_SERVICE lepingud
- OS loob uue SUPPLY lepingu, mille `validFrom` on tulevikus
- Andmeladu tuvastab, et kehtiv GENERAL_SERVICE leping ei ole enam valiidne ja kustutab selle
- Andmeladu loob uue GENERAL_SERVICE lepingu, mille: `validFrom` on võrdne kustutatud GENERAL_SERVICE lepingu `validFrom` väärtusega ja `validTo` on võrdne SUPPLY lepingu `validFrom` väärtusega
- GO saab 2 GENERAL_SERVICE lepingu teavitust:
  - Teavitus 1:
    - `reason` väärtus on `DELETE`
    - `validFrom` ja `validTo` väärtused on identsed eelmise teavitusega (see võimaldab GO-l GENERAL_SERVICE leping üles leida)
  - Teavitus 2:
    - `reason` väärtus on `CREATE`
    - `validFrom` on võrdne `DELETE` sõnumis olnud `validFrom` väärtusega
    - `validTo` on võrdne SUPPLY lepingu `validFrom` väärtusega
- Lisaks toimub ka tavapärane teavitus SUPPLY lepingu lisandumisest

Joonis:

![general-service-ex-3-est.svg](../diagrams/general-service/general-service-ex-3-est.svg)

**Näide "Uus SUPPLY leping, mille algus on minevikus ja lõpp minevikus":**

Käesolev näide illustreerib SUPPLY lepingu ärireeglit: "Lepingu alguskuupäev tohib olla kuni 48h minevikus juhul, kui avatud tarnija registreerib avatud tarne lepingut tagantjärele ja lepingu alguskuupäev langeb kokku võrgulepingu alguskuupäevaga." ja ülimalt vähetõenäolist olukorda, kus lisatakse nt ühepäevane SUPPLY leping minevikku.

- Kliendil on mõõtepunktis hetkel kehtivad GRID ja GENERAL_SERVICE lepingud
- OS loob uue SUPPLY lepingu, mille `validFrom` on minevikus ja langeb kokku GRID lepingu `validFrom` väärtusega ning mille `validTo` on minevikus (ekstreemne näide 1 või 2 päevasest lepingust)
- Andmeladu tuvastab, et kehtiv GENERAL_SERVICE leping ei ole enam valiidne ja kustutab selle
- Andmeladu loob uue GENERAL_SERVICE lepingu, mille `validFrom` on võrdne SUPPLY lepingu `validTo` väärtusega
- GO saab 2 GENERAL_SERVICE lepingu teavitust:
  - Teavitus 1:
    - `reason` väärtus on `DELETE`
    - `validFrom` ja `validTo` väärtused on identsed eelmise teavitusega (see võimaldab GO-l GENERAL_SERVICE leping üles leida)
  - Teavitus 2:
    - `reason` väärtus on `CREATE`
    - `validFrom` on võrdne SUPPLY lepingu `validTo` väärtusega
    - `validTo` on puudu
- Lisaks toimub ka tavapärane teavitus SUPPLY lepingu lisandumisest

Joonis:

![general-service-ex-4-est.svg](../diagrams/general-service/general-service-ex-4-est.svg)

**Näide "Lisandub NAMED_SUPPLIER leping":**

- Kliendil on mõõtepunktis hetkel kehtivad GRID ja GENERAL_SERVICE lepingud
- GO loob uue NAMED_SUPPLIER leping, mille `validFrom` on tulevikus
- Andmeladu tuvastab, et kehtiv GENERAL_SERVICE leping ei ole enam valiidne, kuna teenusepakkuja on muutunud ja kustutab selle
- Andmeladu loob uue GENERAL_SERVICE lepingu, mille: `validFrom` on võrdne kustutatud GENERAL_SERVICE lepingu `validFrom` väärtusega ja `validTo` on võrdne NAMED_SUPPLIER lepingu `validFrom` väärtusega
- GO saab 2 GENERAL_SERVICE lepingu teavitust:
  - Teavitus 1:
    - `reason` väärtus on `DELETE`
    - `validFrom` ja `validTo` väärtused on identsed eelmise teavitusega (see võimaldab GO-l GENERAL_SERVICE leping üles leida)
  - Teavitus 2:
    - `reason` väärtus on `CREATE`
    - `validFrom` on võrdne `DELETE` sõnumis olnud `validFrom` väärtusega
    - `validTo` on võrdne NAMED_SUPPLIER lepingu `validFrom` väärtusega

> [!NOTE]
> Andmeladu loob küll ka tuleviku GENERAL_SERVICE lepingu, kuid kuna see pole aktiveerunud, siis teavitust selle kohta ei loo

Joonis:

![general-service-ex-5-est.svg](../diagrams/general-service/general-service-ex-5-est.svg)