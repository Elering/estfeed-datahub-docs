# Üldteenuse teavitus

## Sisukord

- [Üldteenuse teavitus](#üldteenuse-teavitus)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)

## Sissejuhatus

Andmeladu tuvastab perioodid, millal klient kasutab või hakkab kasutama üldteenust. Nendest perioodidest tuvastab Andmeladu alamperioodid, mis on kaetud nimetatud müüja lepinguga. 
Tuvastatud (alam)perioodide kohta koostab Andmeladu tehnilised üldteenuse (`GENERAL_SERVICE`) lepingud ja määrab teenusepakkujaks kas võrguettevõtja või nimetatud müüja. 
Tegemist on puhtalt tehnilise lahendusega, et üldteenuse algust ja lõppu eksplitsiitselt talletada. Tegemist ei ole juriidilises mõttes lepinguga.

Andmeladu teeb üldteenuse lepingud kättesaadavaks võrguettevõtjale ja nimetatud müüjale `data-distribution/search` teenuse abil. Loe täpsemalt GENERAL_SERVICE lepingute levitamisest lehelt [Andmete levitamine](30-andmete-levitamine.md)

> [!NOTE]
> Andmeladu ei hoia GENERAL_SERVICE lepingute muudatusi. Muudatuste puhul vanad lepingud kustutatakse ja luuakse uued

Üldteenuse rakendumisel sõltub edasine andmevahetuse sellest, kas võrguettevõtjal on sõlmitud nimetatud tarnija leping või mitte:

- Kui ei ole, siis täiendavat andmevahetust pole ette nähtud.
- Kui on, siis Andmeladu võimaldab võrguettevõtjal ja nimetatud müüjal vahetada kliendi meta- ja arveldusandmete uuendusi kasutades teenust `PUT customer`

> [!NOTE]
> Tasub tähele panna, et antud protsessis on Andmeladu lihtsalt sõnumivahendaja ning kliendi täiendavate metaandmete edastamine on vabatahtlik.
