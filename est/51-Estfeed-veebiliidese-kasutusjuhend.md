# Estfeed veebiliidese kasutusjuhend

## Sisukord

<!-- TOC -->

* [Kasutajad ja õigused](#kasutajad-ja-õigused)
  * [Uue tavakasutaja lisamine ettevõtte alla](#uue-tavakasutaja-lisamine-ettevõtte-alla)
  * [Kasutaja õiguste muutmine](#kasutaja-õiguste-muutmine)
  * [Uue tehnilise kasutaja loomine](#uue-tehnilise-kasutaja-loomine)
  * [Olemasolevale tehnilisele kasutajale õiguste andmine või nende muutmine](#olemasolevale-tehnilisele-kasutajale-õiguste-andmine-või-nende-muutmine)
* [Mõõtepunktid](#mõõtepunktid)
  * [Mõõtepunkti EIC koodi genereerimine](#mõõtepunkti-eic-koodi-genereerimine)
  * [Uue mõõtepunkti loomine](#uue-mõõtepunkti-loomine)
  * [Mõõtepunktide masslaadimine](#mõõtepunktide-masslaadimine)
  * [Mõõtepunkti muutmine](#mõõtepunkti-muutmine)
  * [Mõõtepunktide otsing](#mõõtepunktide-otsing)
  * [Mõõtepunktide allalaadimine](#mõõtepunktide-allalaadimine)
* [Mõõteandmed](#mõõteandmed)
  * [Mõõteandmete Estfeedi üles laadimine](#mõõteandmete-estfeedi-üles-laadimine)
  * [Mõõteandmete allalaadimine](#mõõteandmete-allalaadimine)
  * [Mõõteandmete otsing](#mõõteandmete-otsing)
* [Lepingud](#lepingud)
  * [Võrguleping](#võrguleping)
  * [Uue kliendi lisamine süsteemi](#uue-kliendi-lisamine-süsteemi)
  * [Avatud tarne leping](#avatud-tarne-leping)
  * [Agregeerimislepingud](#agregeerimislepingud)
  * [Avatud tarne lepingute tagasiulatuv lisamine](#avatud-tarne-lepingute-tagasiulatuv-lisamine)
  * [Lepingu kustutamine](#lepingu-kustutamine)
  * [Lepingu muutmine](#lepingu-muutmine)
  * [Avatud tarne lepingute tagasiulatuv muutmine](#avatud-tarne-lepingute-tagasiulatuv-muutmine)
  * [Lepingute otsing](#lepingute-otsing)
  * [Lepingute allalaadimine](#lepingute-allalaadimine)
  * [Lepingute kooskõlastused](#lepingute-kooskõlastused)
* [Võrguühenduse sisse või välja lülitamine](#võrguühenduse-sisse-või-välja-lülitamine)
  * [Taotluse saatmine](#taotluse-saatmine)
  * [Taotluste lugemine](#taotluste-lugemine)
  * [Taotlusele vastamine](#taotlusele-vastamine)


## Kasutajad ja õigused
Peale andmevahetusplatvormi kasutamise lepingu sõlmimist lisame administraatori õigused lepingus lisatud haldurile. Haldur saab jagada õiguseid ka teistele enda ettevõtte töötajatele ja luua tehnilisi kasutajaid. Tehniline kasutaja on vajalik Estfeed Datahubi API liidese kasutamiseks. Veebiliidese kasutamiseks pole tehnilist kasutajat vaja.

### Uue tavakasutaja lisamine ettevõtte alla

- Veendu, et oled õiges rollis
- 'Avaleht' -> 'Kasutajad ja õigused'
- 'Uus kasutaja' -> vali kasutaja tüübiks 'Tavakasutaja' 
- Sisesta selle inimese isikukood ja riik, kellele ligipääse anda
- Vali soovitud õigused (Administraator sisaldab kõiki õiguseid; iga kasutaja saab anda maksimaalselt endaga samaväärseid õiguseid). 
- 'Määra'
- Soovitud õigused on isikule antud

Rohkem selgitusi kasutajatüüpide ja muu kohta: [Kasutajate haldus](03.02-kasutajate-haldus.md)

### Kasutaja õiguste muutmine

- 'Avaleht' -> 'Kasutajad ja õigused'
- (soovi korral täpsusta otsingut nime ja/või isikukoodiga) -> 'Otsi'
- Vali kasutaja, kelle õiguseid muuta
- Kliki vastava rea parema oleval mustal pliiatsi ikoonil. Kui nupp ei ole koheselt nähtav kasuta tabeli kohal olevat riba paremale kerimiseks.
- Lisa, eemalda või vaheta kasutaja õiguseid vastavalt soovile
- 'Määra'
- Kasutaja õigused on uuendatud

Rohkem selgitusi kasutajatüüpide ja muu kohta: [Kasutajate haldus](03.02-kasutajate-haldus.md)


### Uue tehnilise kasutaja loomine

- 'Avaleht' -> 'Kasutajad ja õigused'
- 'Uus kasutaja' -> vali kasutaja tüübiks 'Tehniline kasutaja'
- Märgi linnuke 'Või loo uus' ette
- Sisesta soovitud järellliide
- Vali õigused, mida on soov sellele tehnilisele kasutajale anda
- 'Lisa kasutaja'
- Kopeeri "Kliendi ID" ning "Kliendi saladus" kuhugi omale **koheselt** ära
- Sulge moodulaken, tehniline kasutaja on loodud ning sellele on õigused antud

> [!WARNING]
>Moodulaknal kuvatakse loodud tehnilise "Kliendi ID" ja "Kliendi Saladus", mis tuleb koheselt omale kuhugi kopeerida, sest "Kliendi Saladust" **hiljem mitte kusagilt kätte ei saa!**

Rohkem selgitusi kasutajatüüpide ja muu kohta: [Kasutajate haldus](03.02-kasutajate-haldus.md)

### Olemasolevale tehnilisele kasutajale õiguste andmine või nende muutmine

Selle jaoks on kaks võimalust.

Uue kasutaja mooduli kaudu:
- 'Avaleht' -> 'Kasutajad ja õigused'
- 'Uus kasutaja' -> vali kasutaja tüübiks 'Tehniline kasutaja'
- Vali tehniline kasutaja (kui tehnilisi kasutajaid on üks, valitakse see automaatselt, kui neid on mitu tuleb avada rippmenüü ning valida üks)
- Lisa, eemalda või vaheta tehilise kasutaja õiguseid vastavalt soovile
- 'Määra'
- Tehnilise kasutaja õigused on uuendatud

Otsingu kaudu:
- 'Avaleht' -> 'Kasutajad ja õigused'
- 'Otsi'
- Vali tehniline kasutaja, mille õiguseid muuta
- Kliki vastava rea parema oleval mustal pliiatsi ikoonil. Kui nupp ei ole koheselt nähtav kasuta tabeli kohal olevat riba paremale kerimiseks.
- Lisa, eemalda või vaheta tehilise kasutaja õiguseid vastavalt soovile
- 'Määra'
- Tehnilise kasutaja õigused on uuendatud

Rohkem selgitusi kasutajatüüpide ja muu kohta:  [Kasutajate haldus](03.02-kasutajate-haldus.md)

## Mõõtepunktid

### Mõõtepunkti EIC koodi genereerimine
Igale võrguettevõtjale, suletud jaotusvõrgule, liinivaldajale, tootjale ja agregaatorile määrab andmevahetusplatvorm EIC koodi vahemikku. Seejärel peavad kõik mõõtepunkti EIC koodid jääma sellesse vahemikku. Järgmise vaba mõõtepunkti EIC koodi saab genereerida Datahubis.

- 'Mõõtepunktid' -> 'Mõõtepunktide masslaadimine' -> 'Genereeri EIC koodid' -> vali mitut koodi vaja on -> 
'Genereeri'
- Kopeeri genereeritud EIC kood(id)

### Uue mõõtepunkti loomine
Enne võrgulepingu registreerimist on vaja registreerida mõõtepunkt. Mõõtepunkti lisades tuleb lisada ka nõutud tehnilised andmed.

- 'Mõõtepunktid' -> 'Uus'
- Täida vajalikud lahtrid (kohustuslikud väljad on märgitud punase tärniga)
- 'Loo' 
- Uus mõõtepunkt on loodud

Lisainfo:
- **Võrguettevõtja**, **suletud jaotusvõrgu**, **liinivaldaja** või **tootja**  rollis on uue mõõtepunkti loomiseks vajalik kehtiv "Ülekandevõrgu EIC kood" ehk Eleringi alajaama EIC kood. Alajaamade EIC koodid on leitavad Eleringi veebilehelt.
- **Agregaatori** rollis on vajalik "Ülemmõõtepunkti EIC koodi", mille alla loodav agregeerimispunkt kuuluma hakkab. Ülemmõõtepunkt peab kuuluma võrguettevõtjale.

> [!WARNING] 
> Kui lisate mõõtepunkti tüübiks **Sisemine** ei ole teil enam võimalik võrgulepingut registreerida. Mõõtepunkti tüüpi peale registreerimist enam muuta ei saa ja sellisel juhul tuleb registreerida uus mõõtepunkt uue EIC koodiga.

Rohkem selgitusi: [Veebiliideses](05-mootepunktid.md)

### Mõõtepunktide masslaadimine
Mõõtepunktide loomiseks või uuendamiseks on võimalik kasutada ka masslaadimist. See on mõistlik lahendus, kui vaja on lisada korraga rohkem mõõtepunkte. Maksimaalselt on ühe Exceliga võimalik lisada või uuendada 1500 mõõtepunkti.

- 'Mõõtepunktid' -> 'Mõõtepunktide masslaadimine' -> 'Laadi alla'
- Täitke alla laetud fail ära soovitud mõõtepunktide andmetega ning salvestage see arvutisse
- 'Impordi' -> 'Otsi' -> valige eelnevalt täidetud fail -> 'Impordi'
- Eduka importimise korral on kõik failis kirjeldatud mõõtepunktid süsteemi lisatud. Seda saab kontrollida kui minna mõõtepunktide otsingusse (vt [Mõõtepunktide otsing](#mõõtepunktide-otsing)) ning otsida mõnda mõõtepunki, mis just üles laeti.

Rohkem selgitusi: [Veebiliideses](05-mootepunktid.md)

### Mõõtepunkti muutmine
Mõõtepunkti andmed peavad alati olema ajakohased. Selleks tuleb andmete muutumisel uuendada need ka Estfeed Datahubis. Kõiki andmeid (nt mõõtepunkti tüüp) pole uuendada võimalik, sellisel juhul tuleb registreerida uus mõõtepunkt.

- 'Mõõtepunktid'
- Täpsusta otsingut vastavalt vajadusele (klikkides 'Üksikasjalik otsing' näeb rohkem otsingut täpsustavaid parameetreid)
- 'Otsi'
- Otsingu tulemustes on rea lõpus pliiatsi ikoon. Vajadusel kasuta kerimiseks tabeli kohal olevat riba.
- Muuda soovitud andmed
- Vajuta nuppu 'Muuda'
- Mõõtepunkti andmed on muudetud

Rohkem selgitusi: [Veebiliideses](05-mootepunktid.md)

### Mõõtepunktide otsing
Mõõtepunktide tehniliste andmete ja aadressi vaatamiseks tuleks kasutada mõõtepunkti otsingut. Otsingus kuvatakse vaid mõõtepunktid, mille nägemiseks on turuosalisel seaduslik alus.

- 'Mõõtepunktid'
- Täpsusta otsingut vastavalt vajadusele (klikkides 'Üksikasjalik otsing' näeb rohkem otsingut täpsustavaid parameetreid)
- 'Otsi'
- Otsingutulemustes näidatakse otsingu parameetritele vastavaid mõõtepunkte.

Rohkem selgitusi: [Veebiliideses](05-mootepunktid.md)

### Mõõtepunktide allalaadimine
Mõõtepunkte koos tehniliste andmetega on võimalik ka Excelisse laadida.

- 'Mõõtepunktid'
- Täpsusta otsingut vastavalt vajadusele (klikkides 'Üksikasjalik otsing' näeb rohkem otsingut täpsustavaid parameetreid)
- 'Otsi'
- 'Laadi alla'

Rohkem selgitusi: [Veebiliideses](05-mootepunktid.md)

## Mõõteandmed

### Mõõteandmete Estfeedi üles laadimine
Iga päev kella kümneks peavad andmevahetusplatvormile olema lisatud eelmise päeva mõõteandmed. Andmeid saab veebiliideses lisada Excelina.

- 'Mõõteandmed' -> 'Mall' -> vali sobivad parameetrid (*tunni andmete puhul peavad kellaajad olema täistunnid või 15 min andmete puhul veerandtunnid*) -> 'Laadi alla'
- Täida alla laetud mall ära üles laetavate mõõteandmetega ja salvesta oma arvutisse, Exceli täitmise juhendi leiab siit: [Mõõteandmete edastamine Exceli teel](12-mooteandmed.md#mõõteandmete-edastamine-exceli-teel)
- 'Mõõteandmed' -> 'Impordi' -> vali fail, mida üles laadida -> 'Impordi'
- Kui fail oli ilma vigadeta, siis peaks mõõteandmed olema üles laetud või üles laadimisel
- Kas mõõteandmed said üles laetud saab kontrollida kahte moodi:
  -  'Mõõteandmed' -> 'Mõõteandmete olek' -> vali ajavahemik -> 'Otsi'
  - 'Mõõteandmed' -> täida vastavad väljad -> 'Otsi' -> vaata kas üles laetud mõõteandmed tagastatakse otsingu tulemustes.

> [!WARNING] 
> Mõõteandmete laadimisel valideeritakse **reading time** väärtust ehk andmete lugemise aega. Estfeed kuvab kasutajale vaid kõige hilisema lugemise ajaga andmeid. Palun jälgige andmeid korrigeerides, et andmete lugemise aeg oleks eelmisest laadimisest hilisem. Jättes see veerg Excelis tühjaks lisatakse lugemise ajaks andmete ülesse laadimise hetk.

> [!WARNING] 
> Peale andmete lisamist kontrollige kindlasti ka andmete töötlemise staatust, et veenduda andmete edukas salvestamises. Seda saab teha veebiliideses lehel 'Mõõteandmete olek'

  Rohkem selgitusi: [Mõõteandmete edastamine veebiliidese kaudu](12-mooteandmed.md)

### Mõõteandmete allalaadimine
Mõõteandmeid saate laadida ka Excelisse. Excelisse laetakse andmed orginaalses resolutsioonis ja seda kasutaja ise määrata ei saa.
- 'Mõõteandmed' -> täida nõutud väljad -> 'Otsi' -> 'Laadi alla'
- Fail soovitud mõõteandmetega laetakse alla

> [!WARNING] 
> Korraga saab vaadata vaid ühe mõõtepunkti mõõteandmeid.

### Mõõteandmete otsing
Mõõteandmeid saate vaadata ka veebiliideses. Veebiliideses saab andmeid vaadata erinevates resolutsioonides, näiteks arvutades kokku kuu tarbimise.
- 'Mõõteandmed'
- Sisesta "Mõõtepunkti EIC kood" ja "Perioodi algus" (otsingut saab täpsustada kasutades erinevaid parameetreid)
- 'Otsi'
- Sisestatud otsingule vastavad mõõteandmed on kuvatud otsingu tulemustes

> [!WARNING] 
> Korraga saab vaadata vaid ühe mõõtepunkti mõõteandmeid.

Rohkem selgitusi: [Mõõteandmete otsimine veebiliidese kaudu](12-mooteandmed.md)

## Lepingud

### Võrguleping
Võrgulepingut saab lisada vaid mõõtepunkti omanik ehk võrguettevõtja, suletud jaotusvõrk, liinivaldaja või tootja. Eelnevalt peab olema registreeritud [mõõtepunkt](05-mootepunktid.md).

- 'Lepingud' -> 'Uus leping' 
- Vali lepingu tüüp (Võrk, Piirivõrk)
- Lisa enda mõõtepunkti EIC kood või vajuta nuppu 'Otsi mõõtepunkti'
- Vali üks või mitu mõõtepnkti
- 'Otsi klienti'
- Vali klient (*või registreeri uus kui soovitud klient ei ole juba süsteemis, selleks vt [Uue kliendi lisamine süsteemi](#Uue kliendi lisamine süsteemi)*)
- Lisage lepingu alguse kuupäev (ja lõpukuupäev)
- 'Registreeri uus leping'
- Uus leping on lisatud

Rohkem selgitusi: [Veebiliideses](06.2-vorguleping.md)

### Uue kliendi lisamine süsteemi
Võrgulepingut lisades tuleb alati määrata ka klient. Kui klienti veel andmevahetusplatvormil registreeritud ei ole peab võrgulepingu lisamisel kliendi registreerima.

- 'Lepingud' -> 'Uus leping' -> 'Otsi mõõtepunkti' -> täpsusta otsingut -> 'Otsi'
- Vali üks või mitu mõõtepunkti
- 'Otsi klienti' -> 'Registreeri uus klient'
- Vali kliendi tüüp (füüsiline isik, juriidiline isik, organisatsioon)
- Täida nõutud väljad
- 'Salvesta'
- Uus klient on süsteemi lisatud ning temaga saab nüüd lepinguid vormistada

Rohkem selgitusi: [Veebiliideses](06.2-vorguleping.md)

### Avatud tarne leping
Avatud tarne lepingut saab lisada ainult avatud tarnija rollis. Kliendil peab olema mõõtepunktis võrguleping.

- 'Lepingud' -> 'Uus leping' 
- Lisa kliendi EIC või vajuta 'Otsi klienti', mille abil saab klienti otsida erinevate parameetrite järgi
- Kui klient on valitud -> 'Otsi mõõtepunkti'
- Vali üks või mitu mõõtepunkti, millele soovitakse tarne leingut koostada
- Lisage lepingu alguse kuupäev (ja vajadusel lõppkuupäev)
- 'Registreeri uus leping'
- Uus leping on lisatud

Rohkem selgitusi: [Veebiliideses](06.3-avatud-tarne-leping.md)

### Agregeerimisleping
Agregeerimislepingut saab lisada vaid agregaatori rollis. Eelnevalt peab olema registreeritud [mõõtepunkt](05-mootepunktid.md).

- 'Lepingud' -> 'Uus leping' 
- Lisa enda mõõtepunkti EIC kood või vajuta nuppu 'Otsi mõõtepunkti'
- Lisa enda kliendi EIC kood või vajuta nuppu 'Otsi klienti'
- Lisa kehtivuse periood
- 'Registreeri uus leping'
- Uus leping on lisatud

> [!WARNING] 
> Võrgumõõtepunktis peab soovitud perioodil olema kliendil võrguleping ja ühelgi teisel agregaatoril ei tohi olla võrgumõõtepunktis sellel perioodil agregeerimislepingut.

Rohkem selgitusi: [Agregeerimisleping](06.6-agregeerimisleping.md)

### Avatud tarne lepingute tagasiulatuv lisamine
Avatud tarne lepingute lisamise kuupäevadele kehtivad kindlad reeglid, mis on kirjeldatud [siin](06.3-avatud-tarne-leping.md). Kui õigel ajal jäi leping lisamata saad algatada ka lepingute kooskõlastuse. Sellisel juhul registreeritakse leping alles peale osapoolte poolt kinnitamist. Loe täpsemalt [siit](06.8-kooskolastusega-lepingute-muudatused.md). Seda saab teha ainult avatud tarnija rollis.

- 'Lepingud' -> 'Uus leping' 
- Märgi lepingu lisamise vormis 'Lepingute kooskõlastamine'
- Lisa kliendi EIC kood või vajuta nuppu 'Otsi klienti'
- Lisa mõõtepunkti EIC kood või vajuta nuppu 'Otsi mõõtepunkti'
- Lisa soovitud kuupäevad
- Lisa põhjus
- Vajuta nuppu 'Algata kooskõlastus'
- Kooskõlastus on algatatud.

Rohkem selgitusi: [Veebiliideses](06.8-kooskolastusega-lepingute-muudatused.md)

### Lepingu kustutamine
Lepingute kustutamine on lubatud mingitel juhtudel tulevikus algavate lepingute puhul. Täpsemalt saab reeglitega tutvuda siin dokumentatsioonis lepingu tüübi lehel.

- 'Lepingud'
- Täida soovitud väljad, et täpsustada otsingut (rohkem valikuid 'Üksikasjalik otsing' all)
- 'Otsi'
- Kui kustutamine on lubatud on rea lõpus nupp 'Kustuta'
- Kinnita kustutamine
- Leping on kustutatud

### Lepingu muutmine
Lepinguid on võimalik ka muuta, näiteks lisada lõppkuupäev. Täpsemalt saab reeglitega tutvuda siin dokumentatsioonis lepingu tüübi lehel.

- 'Lepingud'
- Täida soovitud väljad, et täpsustada otsingut (rohkem valikuid 'Üksikasjalik otsing' all)
- 'Otsi'
- Kui muutmine on lubatud on rea lõpus nupp 'Muuda'
- Tee soovitud muudatused
- 'Salvesta'
- Lepingu muudatus on salvestatud

### Avatud tarne lepingute tagasiulatuv muutmine
Avatud tarne lepingute muutmise kuupäevadele kehtivad kindlad reeglid, mis on kirjeldatud [siin](06.3-avatud-tarne-leping.md). Kui õigel ajal jäi leping muutmata saad algatada ka lepingute kooskõlastuse. Loe täpsemalt [siit](06.8-kooskolastusega-lepingute-muudatused.md). Seda saab teha ainult avatud tarnija rollis.

- 'Lepingud'
- Täida soovitud väljad, et täpsustada otsingut (rohkem valikuid 'Üksikasjalik otsing' all)
- 'Otsi'
- Lepingute tulemustes vajuta rea lõpus nuppu 'Muuda' või selle puudumisel 'Kooskõlastus'.
- Muutmise aknas märgi valik 'Lepingute kooskõlastamine'
- Tee soovitud muudatused
- Lisa põhjendus
- Vajuta nuppu 'Algata'
- Kooskõlastus on algatatud.

Rohkem selgitusi: [Veebiliideses](06.8-kooskolastusega-lepingute-muudatused.md)

### Lepingute otsing
Lepingute otsimine võib vajalik olla näiteks arveldamiseks, andmete kontrollimiseks või lepingute muutmiseks.

- 'Lepingud'
- Täida soovitud väljad, et täpsustada otsingut (rohkem valikuid 'Üksikasjalik otsing' all)
- 'Otsi'
- Valitud parameetritele vastavad lepingud on kuvatud otsingu tulemustes

### Lepingute allalaadimine
Pakume võimalust ka lepingud Excelisse allalaadida. Excelisse saab laadida maksimaalselt 40 000 lepingut, suurema hulga vähendamiseks kasutage täiendavaid otsingu parameetreid või kasutage API lahendust.

- 'Lepingud'
- Täida soovitud väljad, et täpsustada otsingut (rohkem valikuid 'Üksikasjalik otsing' all)
- 'Otsi'
- Valitud parameetritele vastavad lepingud on kuvatud otsingu tulemustes
- Vajuta nuppu 'Laadi alla'
- Excel on alla laetud

### Lepingute kooskõlastused
Peale lepingute kooskõlastuste algatamist peavad mõjutatud osapooled muudatused kinnitama või tagasi lükkama.

- 'Lepingud' -> 'Lepingute kooskõlastamine' 
- Soovi korral täpsusta otsingut. Näiteks lisa linnuke 'Ootab minu otsust' ette
- 'Otsi'
- Soovi korral vajuta kooskõlastuse reale, et näha rohkem informatsiooni. Vajutades dokumendi ikoonile saab vaadata ka seotud lepinguid.
- Iga kinnitamist ootava kooskõlastuse rea lõpus on nupud 'Kinnita' või 'Keeldu'. Tee sobiv valik.
- Avanevas modaalis kinnita oma valik. Keeldumisel tuleb lisada ka põhjendus.
- Kooskõlastusele on vastus antud

Rohkem selgitusi: [Veebiliideses](06.8-kooskolastusega-lepingute-muudatused.md)


## Võrguühenduse sisse või välja lülitamine

Võrguühenduse sisse või välja lülitamise taotluse saatmise eelduseks on vastavate osapoolte vahel juba eksisteerivad ühisarve leping (vt [Ühisarve leping](#Ühisarve-leping)), võrguleping (vt [Võrguleping](#võrguleping)) ning avatud tarne leping (vt [Avatud tarne leping](#avatud-tarne-leping)).

![Võrguühenduse lülituste eelduste skeem](../images/Võrguühenduse_skeem.PNG)

***Joonis 1.** Võrguühenduse lülituste eelduste skeem*

### Taotluse saatmine

Seda saab teha vaid avatud tarnija rollis. Kui kõik eelduseks olevad lepingud on olemas, siis:

- 'Lülitamise taotlused' -> 'Algata'
- Täida kohustuslikud väljad (need on tähistatud punase tärniga)
- *"Saaja EIC kood" - võrguettevõtja EIC kood, kellel on hetkel kehtiv võrguleping valitud mõõtepunktis valitud kliendiga ning kellega on olemas kehtiv ühisarve leping*
- *"Kliendi EIC kood" - kliendi EIC kood, kellel on kehtivad võrgu- ja avatud tarne lepingud valitud mõõtepunktis*
- *"Mõõtepunkti EIC kood" - mõõtepunkti EIC kood, millel on kehtivad võrgu- ja avatud tarne lepingud vastava kliendiga*
- Soovi korral saab lisada ka sõnumi
- 'Saada'
- Võrguühenduse sisse või välja lülitamise taotlus on saadetud

### Taotluste lugemine

Seda saab teha avatud tarnija, suletud jaotusvõrgu või võrguettevõtja rollis.

- 'Lülitamise taotlused'
- Vali ajavahemik, mille sisse peaks otsitava taotluse loomise kuupäev jääma (valida tuleb nii "Loomise alguskuupäev" kui ka "Loomise lõppkuupäev")
- 'Otsi'
- Otsingu tulemustes kuvatakse vastavas ajavahemikus loodud lülitamiste taotlusi
- Avades vastava sõnumi real kõige parempolse ikooni 'Sõnumiajalugu' saab vaadata vastava lülituse taotluse sõnumite ajalugu 

### Taotlusele vastamine

Seda saab teha avatud tarnija või võrguettevõtja rollis.

- 'Lülitamise taotlused'
- Tee vastavas ajavahemikus otsing
- Vali taotluse sõnum, millele soovid vastata
- Kliki paremalt teisel ikoonil 'Kiirvastus'
- Täida ära kõik vajalikud lahtrid
- 'Vasta'
- Lülitamise taotlusele on vastus saadetud. Seda saab kotrollida 'Sõnumiajalugu' alt.