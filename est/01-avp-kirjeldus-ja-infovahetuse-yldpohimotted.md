# Andmelao kirjeldus ja infovahetuse üldpõhimõtted

## Sisukord

- [Andmelao kirjeldus ja infovahetuse üldpõhimõtted](#andmelao-kirjeldus-ja-infovahetuse-üldpõhimõtted)
  - [Sisukord](#sisukord)
  - [Andmevahetusplatvorm elektrituru kontekstis](#andmevahetusplatvorm-elektrituru-kontekstis)
  - [Andmelao kasutamise leping](#andmelao-kasutamise-leping)
  - [Andmelao funktsionaalsus](#andmelao-funktsionaalsus)
  - [EIC koodid](#eic-koodid)
  - [Infovahetuse üldpõhimõtted](#infovahetuse-üldpõhimõtted)
    - [Sissejuhatus](#sissejuhatus)
    - [Keskkonnad](#keskkonnad)
    - [Üldreeglid](#üldreeglid)
    - [Aja esitamise reeglid](#aja-esitamise-reeglid)
    - [Aadressi esitamise reeglid](#aadressi-esitamise-reeglid)
    - [Vastussõnumite koodid](#vastussõnumite-koodid)

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

- **Võrguettevõtja** on elektriettevõtja, kes osutab võrguteenust võrgu kaudu ning kes **vastutab** oma võrgupiirkonna mõõtepunktide ja mõõteandmete kogumise ja edastamise eest Andmelattu. Iga võrguettevõtja on turuosaline oma võrgukadudega.  Lisaks vastavalt seadusandlusele,  kui turuosalisel ei ole avatud tarne lepingut, siis on tema avatud tarnijaks automaatselt tema võrguettevõtja või viimase poolt nimetatud müüja.
- **Liinivaldaja** kasutab elektrienergia edastamiseks otseliini ning kes **vastutab** oma liinipiirkonna mõõteandmete kogumise ja edastamise eest Andmelattu.
- **Suletud jaotusvõrk** osutab võrguteenust suletud jaotusvõrgu kaudu kaudu ning kes **vastutab** oma võrgupiirkonna mõõtepunktide ja mõõteandmete kogumise ja edastamise eest Andmelattu. Iga võrguettevõtja on turuosaline oma võrgukadudega.  Suletud jaotusvõrgus edastatakse elektrienergiat geograafiliselt piiratud tootmiskoha, ärirajatise või ühisteenuste koha piires seal asuvatele äritarbijatele, kelle tegevus või tootmisprotsess on tehnilistel või ohutusega seotud põhjustel omavahel ühendatud, või mille kaudu edastatakse elektrienergiat peamiselt võrgu omanikule või võrguettevõtjale, kes seda võrku haldab, või nendega valitseva mõju kaudu seotud ettevõtjale.
- **Tootja**  edastab oma mõõtepunkti(de)ga seotud andmed, kui ei oma liinivaldaja tegevusluba.
- **Laadimispunkti operaator** haldab laadimispunkte, mille kaudu on  võimalik laadida korraga ühte elektrisõidukit või vahetada korraga ühe elektrisõiduki aku.
- **Avatud tarnija** on elektri müüja või ostja, kes osutab kliendile avatud tarnet ehk müüb/ostab kas puudujääva/ülejääva elektrienergia koguse või müüb/ostab kogu mõõdetud elektrienergia koguse sõltuvalt poolte vahelisest kokkuleppest turuosalisega. Avatud tarnija sisestab Andmelattu avatud tarne lepingu andmed turuosalisega.
- **Nimetatud müüja** võrguettevõtja poolt valitud avatud tarnija, kes osutab võrguettevõtja asemel avatud tarne teenust võrguettevõtja teeninduspiirkonna klientidele, kellel puudub avatud tarne leping;
- **Bilansihaldur** on hierarhiliselt kõrgemal olev avatud tarnija, kellel on bilansileping süsteemihalduriga.
- **Agregaator** on tarbimise juhrimise teenuse osutaja ning edastab Andmelattu agregeerimislepingu info, tarbimise juhtimise mõõtepunkti ja andmed.
- **Süsteemihaldur** on Elering, tagab Eesti elektrisüsteemi bilansi, on avatud tarnijaks bilansilepingu sõlminud bilansihalduritele, haldab ja arendab elektrituruseaduse alusel Andmeladu.

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

Sõnumite struktuuride ja validatasioonide kirjeldused on leitavad [Swagger](https://test-datahub.elering.ee/swagger-ui/index.html) keskkonnast.

> **Note**
> Sõnumite näidiste kogumik on loomisel

### Keskkonnad

- [Testkeskkond](https://andmeladu-test.elering.ee/consumer/home)
- [Live keskkond](https://andmeladu.elering.ee/consumer/home)
- [Masinliidestuse sõnumid ja kirjeldused](https://andmeladu.elering.ee/documentation.html)

### Üldreeglid

- Kohustuslikud (tärniga tähistatud) elemendid peavad olema alati lisatud. Elemendi puudumisel muutub
sõnum töötlematuks ja seda ei aktsepteerita vastuvõtval poolel.
- Osad elemendid on kohustuslikud ainult teatud juhtudel. Sellisel juhul on kohustuslikkuse reegel leitav sõnumi või elemendi kirjeldusest või käesolevatest dokumentidest.
- Kui element ei ole kohustuslik, siis võib see puududa.
- Sõnumites kasutatakse vaikimisi UTF-8 kodeeringut.

### Aja esitamise reeglid

- Kõik ajad esitatakse vastavalt [ISO-8601](http://en.wikipedia.org/wiki/ISO_8601) formaadile. Süsteem toetab nii UTC kui ka ajatsooniga ajaväärtust. Seega nii `2023-04-01T00:00Z` kui ka `2023-04-01T00:00+03:00` on lubatud.

### Aadressi esitamise reeglid

Liidestuval süsteemil on aadressi andmete edastamiseks 2 võimalust:

- saata Maaameti ADS süsteemi aadressi ID (ADR_ID).
- saata aadressi kirjeldus tekstilisel kujul.

Mõlemad korraga ei ole lubatud.

Aadressi tekstilisel kujul saatmise korral on andmekvaliteedi huvides palve kasutada ametlikke [EHAK klassifikaatoris](https://klassifikaatorid.stat.ee/Item/stat.ee/c4c47742-12d7-4fea-bc8c-5aeca9112e2a/88) toodud maakonna, omavalitsuse ja asutusüksuse nimekujusid.

Kui Andmelattu laekub ADS süsteemi ID, siis Andmeladu pärib ise ADS süsteemist aadressi komponendid ja tekstilise kuju.

> **Warning**
>
> Turuosaline on kohustatud hoidma Andmelaos olevad aadressi andmed ajakohased. Andmeladu aadresse omal initsiatiivil ei uuenda. See tähendab, et aadressi muutumise korral (nt KOV muudab tänava nime) peab turuosaline saatma vastava andmeobjekti uuendussõnumi, kus on uus aadressi ID või uus aadress tekstilisel kujul.

Aadressi sektsioon koosneb järgmistest atribuutidest:

```json
{
"adsId": "string",
"county": "string",
"municipality": "string",
"locality": "string",
"streetAddress": "string", 
"postalCode": "string",
"comment": "string"
}
```

Atribuutide selgitus:

| Atribuut      | Selgitus                                                                                        | Näide              |
|---------------|-------------------------------------------------------------------------------------------------|--------------------|
| adsId         | Maaameti ADS süsteemi ADR_ID                                                                    | 2105345            |
| county        | Maakond                                                                                         | Harju maakond      |
| municipality  | Omavalitsus                                                                                     | Tallinn            |
| locality      | Asustusüksus (küla, alevik, alev, vallasisene linn) või linnaosa                                | Kesklinna linnaosa |
| streetAddress | Lähiaadress (väikekoht, maaüksuse nimi, tänav, aadressinumber, korteri või muu hooneosa number) | Pärnu mnt 8        |
| postalCode    | Postiindeks                                                                                     | 10148              |
| comment       | Kommentaar                                                                                      | C1T                |

### Vastussõnumite koodid

Kasutusel on klassikalised REST API vastuskoodid. Veaolukordade korral tagastab süsteem võimalusel info vea põhjuse kohta. Vea kirjeldused on nii inim- kui masinloatavas formaadis.

Vastussõnumite struktuurid on leitavad [Sõnumite näidiste kogumik on loomisel](https://test-datahub.elering.ee/swagger-ui/index.html) keskkonnast.
