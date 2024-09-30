# Andmelao kirjeldus ja infovahetuse üldpõhimõtted

## Sisukord

<!-- TOC -->
* [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](#andmelao-kirjeldus-ja-infovahetuse-üldpõhimõtted)
  * [Sisukord](#sisukord)
  * [Andmevahetusplatvorm elektrituru kontekstis](#andmevahetusplatvorm-elektrituru-kontekstis)
  * [Andmelao kasutamise leping](#andmelao-kasutamise-leping)
  * [Andmelao funktsionaalsus](#andmelao-funktsionaalsus)
  * [EIC koodid](#eic-koodid)
  * [Infovahetuse üldpõhimõtted](#infovahetuse-üldpõhimõtted)
    * [Sissejuhatus](#sissejuhatus)
    * [Keskkonnad](#keskkonnad)
    * [Üldreeglid](#üldreeglid)
    * [Aja esitamise reeglid](#aja-esitamise-reeglid)
    * [Vastussõnumite koodid](#vastussõnumite-koodid)
    * [Vastuste lehitsemine](#vastuste-lehitsemine)
  * [Kasutajaliidese üldpõhimõtted](#kasutajaliidese-üldpõhimõtted)
<!-- TOC -->

## Andmevahetusplatvorm elektrituru kontekstis

Vastavalt elektrituruseaduses sätestatule toimub avatud elektriturul kogu andmevahetusprotsess läbi andmevahetusplatvormi (edaspidi **Andmeladu**).

Andmeladu on digitaalne keskkond, mille kaudu toimub elektriturul andmevahetus avatud tarnija ja agregaatori vahetamiseks, mõõteandmete edastamiseks turuosaliste vahel, nende säilitamiseks ning turuosalisele seadusega pandud kohustuste täitmiseks ja talle antud õiguste tagamiseks.

Andmelao eesmärk on turuosaliste võrdse kohtlemise printsiipe arvestav efektiivse andmevahetuse protsessi tagamine avatud elektriturul. Andmeladu tagab selleks õigusi omavatele turuosalistele võrdsetel alustel juurdepääsu elektrienergia mõõteandmetele ja võimaldab kiiret tarnija vahetuse protsessi.

Andmelao arenduse eest vastutab Elering, kelle ülesandeks on ka kogu süsteemi edaspidine hooldus. Võrguettevõtjad vastutavad sisestatud andmete mahu ja nende kvaliteedi, mõõteandmete täpsuse, tunni või 15 minuti resolutsiooni põhise jaotuse ja sisestatud kliendiinfo korrektsuse eest. Avatud tarnijad vastutavad sisestatud elektrimüügi lepingute info õigsuse eest. Agregaatorid vastutavad agregeerimislepingute info ja edastatud tarbimise juhtimise andmete õigsuse eest.

Andmelao süsteem koosneb tarkvara ja riistvara lahendusest, mille abil hallatakse elektrienergia mõõteandmete vahetamist turuosaliste vahel, toetatakse elektrienergia tarnijate vahetuse protsessi ja säilitatakse mõõteandmed. Andmelaos on defineeritud Eesti elektriturul tegutsevad turuosalised, samuti kõik turuosaliste vahelist elektrienergia liikumist mõõtvad mõõtepunktid. Kõik turuosalised ja mõõtepunktid identifitseeritakse üheselt Andmelao poolt väljastatud unikaalse koodiga (EIC kood).

Andmelao kasutamiseks on kokku lepitud ühtsed andmeformaadid.

Turuosalised saavad Eleringi kliendiportaali kaudu oma mõõteandmetele ligipääsu ja võimaluse andmete allalaadimiseks. Samuti on kliendiportaalis turuosalisele nähtav kogu Andmelaos teda puudutav info: lepingute tähtajad, avatud tarnijad, agregaatorid, mõõteandmed, turuosalise EIC kood ja turuosalisega seotud mõõtepunktide EIC koodid. Iga turuosaline saab anda kliendiportaali kaudu volitusi eelmiste perioodide mõõteandmetele juurdepääsuks, seda eelkõige eesmärgiga saada avatud tarnijatelt personaalseid pakkumisi, agregeerimislepingu sõlmimiseks või oma energiaandmete jagamiseks muule energiateenusele. Turuosalise andmetele saavad ligipääsu need turuosalised ja muud energiateenused, kellel selleks on seadusjärgne õigus või kellele turuosaline ise on sellise õiguse andnud.

Kõik füüsiliste isikutega seotud andmed (sh EIC koodid) on isikuandmed ja isikuandmete töötlemisele Andmelaos kohaldub Euroopa Parlamendi ja Nõukogu määrus (EL) 2016/679, 27. aprill 2016, füüsiliste isikute kaitse kohta isikuandmete töötlemisel ja selliste andmete vaba liikumise ning direktiivi 95/46/EÜ kehtetuks tunnistamise kohta (edaspidi isikuandmete kaitse üldmäärus).

Õiguslikud alused Andmelao kasutamiseks ja andmevahetuseks kõikidele turuosalistele tulenevad Elektrituruseadusest ja Elektrituru toimimise võrgueeskirjast.

## Andmelao kasutamise leping

Andmelattu andmete sisestajaid nimetatakse operaatoriteks, kelle ülesanded ja vastutused jagunevad järgmiselt:

- **Võrguettevõtja (GO)** on elektriettevõtja, kes osutab võrguteenust võrgu kaudu ning kes **vastutab** oma võrgupiirkonna mõõtepunktide ja mõõteandmete kogumise ja edastamise eest Andmelattu. Iga võrguettevõtja on turuosaline oma võrgukadudega.  Lisaks vastavalt seadusandlusele,  kui turuosalisel ei ole avatud tarne lepingut, siis on tema avatud tarnijaks automaatselt tema võrguettevõtja või viimase poolt nimetatud müüja.
- **Liinivaldaja (LO)** kasutab elektrienergia edastamiseks otseliini ning kes **vastutab** oma liinipiirkonna mõõteandmete kogumise ja edastamise eest Andmelattu.
- **Suletud jaotusvõrgu ettevõtja (CDN)** osutab võrguteenust suletud jaotusvõrgu kaudu kaudu ning kes **vastutab** oma võrgupiirkonna mõõtepunktide ja mõõteandmete kogumise ja edastamise eest Andmelattu. Iga võrguettevõtja on turuosaline oma võrgukadudega. Suletud jaotusvõrgus edastatakse elektrienergiat geograafiliselt piiratud tootmiskoha, ärirajatise või ühisteenuste koha piires seal asuvatele äritarbijatele, kelle tegevus või tootmisprotsess on tehnilistel või ohutusega seotud põhjustel omavahel ühendatud, või mille kaudu edastatakse elektrienergiat peamiselt võrgu omanikule või võrguettevõtjale, kes seda võrku haldab, või nendega valitseva mõju kaudu seotud ettevõtjale.
- **Tootja (PO)**  edastab oma mõõtepunkti(de)ga seotud andmed, kui ei oma liinivaldaja tegevusluba.
- **Laadimispunkti operaator (CO)** haldab laadimispunkte, mille kaudu on võimalik laadida korraga ühte elektrisõidukit või vahetada korraga ühe elektrisõiduki aku.
- **Salvestusjaama operaator (STO)** haldab mõõtepunkte, mis on seotud elektrienergia salvestamisega energiasalvestusüksustes, kus salvestatakse energiat, sealhulgas kahesuunalist laadimist võimaldav elektrisõiduki laadimispunkt.
- **Gaasitankla operaator (GST)** haldab laadimispunkte, mille kaudu on võimalik tankida gaasi mootorsõidukitele.
- **Muu energiateenuse osutaja (ES)** on juriidiline isik, kes osutab energiateenuseid või rakendab muid energiatõhususe parandamise meetmeid lõpptarbija seadmetes või ruumides.
- **Avatud tarnija (OS)** on elektri müüja või ostja, kes osutab kliendile avatud tarnet ehk müüb/ostab kas puudujääva/ülejääva elektrienergia koguse või müüb/ostab kogu mõõdetud elektrienergia koguse sõltuvalt poolte vahelisest kokkuleppest turuosalisega. Avatud tarnija sisestab Andmelattu avatud tarne lepingu andmed turuosalisega.
- **Nimetatud müüja (NS)** võrguettevõtja poolt valitud avatud tarnija, kes osutab võrguettevõtja asemel avatud tarne teenust võrguettevõtja teeninduspiirkonna klientidele, kellel puudub avatud tarne leping.
- **Bilansihaldur (BRP)** on hierarhiliselt kõrgemal olev avatud tarnija, kellel on bilansileping süsteemihalduriga.
- **Agregaator (AGG)** on tarbimise juhtimise teenuse osutaja ning edastab Andmelattu agregeerimislepingu info, tarbimise juhtimise mõõtepunkti ja andmed.
- **Süsteemihaldur (TSO)** on Elering, tagab Eesti elektrisüsteemi bilansi, on avatud tarnijaks bilansilepingu sõlminud bilansihalduritele, haldab ja arendab elektrituruseaduse alusel Andmeladu.

Operaatoritele, v.a energiateenuse osutajad, tagatakse andmete edastamiseks ja kättesaamiseks andmevahetus nii masinliidestuse (API) kui täiendava veebirakenduse kaudu.

Energiateenuste osutajatele võimaldatakse andmetele ligipääs ainult turuosalise poolt Andmelao kliendiportaali kaudu antud ligipääsuõiguse alusel ning tagatakse andmevahetus masinliidestuse (API) kaudu.

Lõppklientidele on oma andmetele ligipääsuks loodud kliendiportaal, mille kaudu saab klient hallata oma esindusõigusi, anda õigusi teistele isikutele andmetele ligipääsuks ning vaadata tema mõõtepunktidega seotud andmete päringute logisid.

Andmelao kasutamiseks, v.a lõppklient, tuleb sõlmida süsteemi¬halduriga Andmelao kasutamise leping, millega määratakse poolte vahelised õigused ja kohustused andmete sisestamiseks ja pärimiseks vastavalt seadusandlusele.

**Süsteemihaldur tagab operaatoritele Andmelao kasutamise järgmiselt:**

1. tagab elektroonilisel teel edastatavate andmete turvalisuse;
2. teavitab Operaatorit võimalikest hooldus- ja arendustöödest, mis mõjutavad Andmelao kasutamist e-posti teel või Andmelao vahendusel hiljemalt 5 (viis) tööpäeva enne tööde teostamist;
3. teavitab Operaatorit e-posti teel või Andmelao vahendusel planeeritavatest hooldustöödest ja seisakutest vähemalt 3 (kolm) tööpäeva ette;
4. korraldama Andmelao tõrgeteta tööks vajalikku hooldust ja arendust lähtudes põhimõttest, et hooldustöid ei planeerita ajavahemikus 8.00-12.00;
5. informeerima Operaatorit tõrgetest Andmelao töös esimesel võimalusel, sh teavitades tööpäeva perioodil tekkinud tõrgetest operaatoreid 15 minuti jooksul;
6. taastama Andmelao kasutamise esimesel võimalusel (reeglina 4 tunni jooksul).

Kõik ülaltoodud elektroonsed teavitused edastatakse operaatori poolt lepinguga määratud Haldurile (käesoleva dokumendi peatükk 16). Halduril on võimalus ülaltoodud teadete edastamine delegeerida mõnele teisele e-posti aadressile, teavitades sellest elektroonselt süsteemihalduri Andmelao administraatorit.

## Andmelao funktsionaalsus

Andmeladu kui süsteem katab järgmised põhiprotsessid:

1. kodeerimise protsess;
2. mõõtepunkti tehniliste andmete ja mõõteandmete esitamise protsess;
3. tarnijavahetuse ja seda kirjeldava sõnumite vahetamise protsess;
4. võrguettevõtja võrguarve edastuse protsess;
5. avatud tarnija ja võrguettevõtja vahelise infovahetuse kanal;
6. katkematu avatud tarne ahela ja bilansiportfellide (bilansipiirkondade) haldus;
7. bilansiselgituse agregeeritud koondraportite arvutamine ja edastamine;
8. agregeerimislepingute ja tarbimise juhtimise mõõteandmete edastamine.

![Joonis 1: Andmelao põhiprotsessid](../images/andmeladu.png)
*Joonis 1: Andmelao põhiprotsessid*

## EIC koodid

EIC kood (*Energy Identification Code*) on unifitseeritud kodeerimissüsteemi alusel turuosalisele või mõõtepunktile määratud unikaalne identifikaator, mis on vajalik elektriturul tegutsevate turuosaliste kohta käiva infovahetuse automatiseerimiseks.

Iga turul osalev isik peab omama EIC koodi, millega seostatakse kõik tema turutegevused.

EIC koodide register asub Andmelaos.

- **Turuosalise EIC kood** on turuosalist üheselt identifitseeriv unikaalne märgikombinatsioon. Turuosalise EIC koodi määrab süsteemihaldur või süsteem automaatselt.
- **Mõõtepunkti EIC kood** on mõõtepunkti üheselt identifitseeriv unikaalne märgikombinatsioon. Süsteemihaldur eraldab jaotusvõrguettevõtjale või liinivaldajale kasutamiseks koodivahemiku.

## Infovahetuse üldpõhimõtted

### Sissejuhatus

Automaatne infovahetus (masinliidestus) toimub Andmelao ja kliendi infosüsteemi vahel REST liidese abil. Infovahetuseks süsteemide vahel kasutatakse JSON-formaadis esitatud sõnumeid.

Sõnumite struktuuride ja validatsioonide kirjeldused on leitavad järgmiselt:

- [Test Swagger](https://public-test-datahub.elering.ee/swagger-ui/index.html) keskkonnas on nähtav versioon, mis on rakenduses realiseeritud. Selles keskkonnas on võimalik Swagger interaktiivse keskkonna abil rakendusele päris sõnumeid saata.
- [Github](https://github.com/Elering/Estfeed-API) keskkonnas on nähtav tuleviku visioon. Liides on kirjeldatud OpenAPI formaadis.

> [!NOTE]
> Sõnumite näidiste kogumik on loomisel

### Keskkonnad

Andmelao veebirakendus:

- [Avalik test keskkond](https://public-test-datahub.elering.ee/login)
- [Live keskkond](https://datahub.elering.ee/login)

Andmelao masinliidese otspunktid:

- Avalik test keskkond:
  - Andmete levitamise teenused: `https://public-test-dd-datahub.elering.ee`
  - Raportite teenused: `https://public-test-rpt-datahub.elering.ee`
  - Ülejäänud teenused: `https://public-test-datahub.elering.ee`
- Live keskkond:
  - Andmete levitamise teenused: `https://dd-datahub.elering.ee`
  - Raportite teenused: `https://rpt-datahub.elering.ee`
  - Ülejäänud teenused: `https://datahub.elering.ee`

Andmelao OpenApi teenuste kirjeldused:

- Avalik test keskkond:
  - [Andmete levitamise teenused](https://public-test-dd-datahub.elering.ee/swagger-ui/index.html)
  - [Raportite teenused](https://public-test-rpt-datahub.elering.ee/swagger-ui/index.html)
  - [Ülejäänud teenused](https://public-test-datahub.elering.ee/swagger-ui/index.html)
- Live keskkond:
  - [Andmete levitamise teenused](https://dd-datahub.elering.ee/swagger-ui/index.html)
  - [Raportite teenused](https://rpt-datahub.elering.ee/swagger-ui/index.html)
  - [Ülejäänud teenused](https://datahub.elering.ee/swagger-ui/index.html)

### Üldreeglid

- Kohustuslikud (tärniga tähistatud) elemendid peavad olema alati lisatud. Elemendi puudumisel muutub
sõnum töötlematuks ja seda ei aktsepteerita vastuvõtval poolel.
- Osad elemendid on kohustuslikud ainult teatud juhtudel. Sellisel juhul on kohustuslikkuse reegel leitav sõnumi või elemendi kirjeldusest või käesolevatest dokumentidest.
- Kui element ei ole kohustuslik, siis võib see puududa.
- Sõnumites kasutatakse vaikimisi UTF-8 kodeeringut.

### Aja esitamise reeglid

- Kõik ajad esitatakse vastavalt [ISO-8601](http://en.wikipedia.org/wiki/ISO_8601) formaadile. Süsteem toetab nii UTC kui ka ajatsooniga ajaväärtust. Seega nii `2023-04-01T00:00Z` kui ka `2023-04-01T00:00+03:00` on lubatud.

### Vastussõnumite koodid

Kasutusel on klassikalised REST API vastuskoodid. Veaolukordade korral tagastab süsteem võimalusel info vea põhjuse kohta. Vea kirjeldused on nii inim- kui masinloatavas formaadis.

Loe täpsemalt dokumendist [Andmevahetusliidese veakoodid](35-veakoodid.md)

### Vastuste lehitsemine

Paljud teenused, mis võimaldavad andmeid otsida pakuvad andmete lehitsemise (paging) võimalust. Lehitsemisega on võimalik piirata korraga päritavate andmete hulka ja vaadelda andmeid lehtede kaupa.
Standardne lehitsemise sektsioon päringus on järgmine:

```json
"pagination": {
  "page": 0,
  "pageSize": 500
}
```

* `page`ehk leheküljenumber algab 0-st. Iga järgneva päringuga saab väärtust 1 võrra tõsta ja seega teostada andmete sirvimist lehekülgede kaupa
* `pageSize` on maksimaalne lubatud kirjete arv ühel lehel. Swaggeris on dokumenteeritud maksimaalsed väärtused.

Teenused, mis võimaldavad lehitsemist, annavad vastussõnumis infot, mis lehe andmeid hetkel kuvatakse (`page`) ning palju lehti kokku tuvastati (`totalPages`):

```json
"pagination": {
  "page": 0,
  "totalPages": 1
}
```

## Kasutajaliidese üldpõhimõtted

Käesoleva dokumentatsiooni teised lehed ja lõigud sisaldavad täpsemaid juhiseid kasutajaliidese kasutamiseks. Kuid me soovitame esmalt vaadata sissejuhatavat videot: [The new Estfeed data exchange platform user interface workshop, 21.08.2024](https://www.youtube.com/watch?v=YTClvPhINEg)