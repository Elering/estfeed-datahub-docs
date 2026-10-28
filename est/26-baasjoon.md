# Baasjoon

> [!WARNING]
> **MUSTAND.** See dokument kirjeldab baasjoone funktsionaalsuse esimest etappi. API lepingud — eelkõige
> otsingu parameetrid ja vastuse struktuur — võivad enne kasutuselevõttu veel muutuda.

## Sisukord

- [Sissejuhatus](#sissejuhatus)
- [Põhimõisted](#põhimõisted)
- [Esitamise tähtaeg ja ajareeglid](#esitamise-tähtaeg-ja-ajareeglid)
- [Baasjoone andmete edastamine](#baasjoone-andmete-edastamine)
  - [Masinliidese sõnum](#masinliidese-sõnum)
  - [Veebiliides ja Exceli import](#veebiliides-ja-exceli-import)
- [Töötlemise staatuse kontrollimine](#töötlemise-staatuse-kontrollimine)
- [Baasjoone andmete küsimine](#baasjoone-andmete-küsimine)
- [Ressursi andmete küsimine](#ressursi-andmete-küsimine)
- [Parandused pärast tähtaega ja esitamata baasjoon](#parandused-pärast-tähtaega-ja-esitamata-baasjoon)

## Sissejuhatus

Baasjoon on reguleerimisteenuse pakkuja (edaspidi agregaator) prognoos mõõtepunkti tarbimise või tootmise kohta 15-minutilisel arveldusperioodil olukorras, kus reguleerimistarnet ei toimuks. See kirjeldab mõõtepunkti eeldatavat energiakäitumist 
ning loob võrdlustaseme, mille alusel hinnatakse hiljem nii prognoosi täpsust kui ka deklareeritud aFRR- ja mFRR-reguleerimistarnete tegelikku toimumist.

Baasjoone täpsuse eest vastutab agregaator.

Baasjoone rakendamise esimeses etapis võtab Estfeed Datahub baasjoone esitusi vastu, salvestab need ning võimaldab neid pärida
koos mõõteandmetega. Baasjoone täpsuse hindamine ja deklareeritud reguleerimistarnete valideerimine lisanduvad järgmistes etappides.

Baasjoone metoodika avaliku konsultatsiooni materjalid on leitavad Eleringi kodulehelt: https://www.elering.ee/konsultatsioon/baasjoone-metoodika-avalik-konsultatsioon

> [!NOTE]
> Baasjoone funktsionaalsus kehtib ainult **elektriturule**.

## Põhimõisted

| Mõiste | Selgitus |
| --- | --- |
| Ressurss | Eelkvalifitseeritud reguleerimisressurss, mida identifitseerib **ressursi EIC**. Ressurss koondab ühte või mitut võrgumõõtepunkti. Ressursse registreerib ja haldab Elering. |
| Võrgumõõtepunkt | (Võrgu)mõõtepunkt, mille kohta baasjoon esitatakse. Võrgumõõtepunkt on ühe või mitme agregeerimismõõtepunkti ülemmõõtepunkt. |
| Agregeerimismõõtepunkt | Agregaatori poolt võrgumõõtepunkti alla registreeritud mõõtepunkt. Ressursi EIC deklareeritakse agregeerimismõõtepunkti tunnustel. |
| Arveldusperiood | 15-minutiline periood, mida identifitseerib selle **UTC algusaeg**. Turuperiood, aktiveerimisperiood ja arveldusperiood tähistavad sama 15-minutilist ajavahemikku. |
| Baasjoone esitamise õigus | agregaator võib esitada ja pärida baasjoont võrgumõõtepunkti kohta täpselt siis, kui tal on kehtiv agregeerimisleping agregeerimismõõtepunktil, mille ülemmõõtepunkt see võrgumõõtepunkt on. |

**Baasjoon esitatakse võrgumõõtepunkti kohta**, kahe eraldi väärtusena iga arveldusperioodi kohta:

| Suund | Tähendus |
| --- | --- |
| Tarbimise baasjoon (`outQty`) | Võrgumõõtepunkti prognoositud tarbimine, kWh |
| Tootmise baasjoon (`inQty`) | Võrgumõõtepunkti prognoositud tootmine, kWh |

> [!IMPORTANT]
> „IN/OUT" tähistab reguleerimisteenuste dokumentatsioonis kahte eri asja, mis võivad sama sündmuse puhul
> osutada vastassuundadesse:
>
> - **Energiasuunad** (võrgu vaatepunkt) — baasjoone esitamisel on `inQty` võrku *sisse* antav energia
>   (tootmise prognoos) ja `outQty` võrgust *välja* võetav energia (tarbimise prognoos).
> - **Reguleerimissuunad** (süsteemi vaatepunkt) — deklareeritud aFRR/mFRR reguleerimistarnetel tähendab
>   IN **ülesreguleerimist** (tarbimise vähendamine või tootmise suurendamine) ja OUT **allareguleerimist** (tarbimise suurendamine
>   või tootmise vähendamine).
>
> Näide: kui tarbimist *vähendatakse*, on reguleerimistarne **IN** (ülesreguleerimine), kuid selle mõju
> paistab **tarbimise** (`outQty`) energiaveerus. Sama füüsiline sündmus kannab kahel juhul vastupidiseid
> silte.

## Esitamise tähtaeg ja ajareeglid

> Soovitus on esialgne baasjoon saata aegsasti ette ning peale seda edastada baasjoone täpsustusi. See tagab, et baasjoones ei jää sisse auke.   

> [!WARNING]
> Arveldusperioodi baasjoone "30 minutit enne" saabumise nõude täitmist kontrollitakse sõnumi Estfeed Datahubi saabumise aja alusel, mistõttu on soovitatav baasjoon saata ajavaruga.

Arveldusperioodi baasjoon peab olema Estfeed Datahubi poolt vastu võetud **hiljemalt 30 minutit enne
perioodi UTC algusaega**:

```
tähtaeg(P) = perioodi algus (UTC) − 30 minutit
```

Tähtajaks (kaasa arvatud) vastu võetud esitus katab perioodi. Näiteks kui sõnum jõuab Estfeed Datahubi kell 10.07, saab kõige varasema perioodina esitada perioodi algusega kell **10.45**. Selle perioodi esitamise tähtaeg on kell 10.15. Perioodi algusega kell 10.30 enam esitada ei saa, sest selle tähtaeg oli kell 10.00.

- Baasjoont võib esitada kuni **32 päeva** enne perioodi.
- Kuni tähtajani võib agregaator baasjoont **vabalt parandada või asendada**. Kehtivaks loetakse **viimane enne tähtaega edukalt vastu võetud baasjoone väärtus. Varasemaid baasjoone väärtusi eraldi kehtivate andmeversioonidena ei säilitata, kuid kõik esitatud sõnumid ja nende töötlemise tulemused säilitatakse sõnumite ajaloos.
- Pärast tähtaega ei saa agregaator baasjoont enam muuta (vt
  [Parandused pärast tähtaega](#parandused-pärast-tähtaega-ja-esitamata-baasjoon)).
- Esitamise kohustus ei sõltu sellest, kas perioodil reguleerimisteenust tellitakse või aktiveeritakse —
  baasjoon tuleb esitada seotud võrgumõõtepunktide **kõikide** arveldusperioodide kohta.

Aja- ja kalendrireeglid:

- Arveldusperioode identifitseerib nende **UTC algusaeg**. Eesti kohalik aeg määrab arvelduspäeva ja -kuu
  ning seda kasutatakse andmete kuvamisel.
- Tavalisel kohaliku aja päeval on 96 arveldusperioodi, suveajale ülemineku päeval 92 ja talveajale
  ülemineku päeval 100. Talveajale ülemineku päeva korduvad kohaliku aja perioodid eristatakse nende UTC
  ajatemplite alusel.
- Lepingute kehtivust hinnatakse Eesti kalendripäeva kaupa: kehtiva kalendripäeva kõik arveldusperioodid
  on kaetud.

Muud reeglid:
- vaata ka [Infovahetuse üldpõhimõtted](01.2-infovahetuse-yldpohimotted.md). Masinliidese sõnumites kasutatakse [Päis versioon 2](01.2-infovahetuse-yldpohimotted.md#päis-versioon-2).

## Baasjoone andmete edastamine

Baasjoone andmete edastamise üldine protsess on järgmine:

1. Agregaator saadab Datahubi baasjoone andmete [masinliidese sõnumi](26-baasjoon.md#masinliidese-sõnum) või Exceli faili.

2. Datahub registreerib sõnumi saabumise aja, mida kasutatakse tähtaegade kontrollimiseks. Hilisemad tehnilised viivitused ei mõjuta tähtaegsuse hinnangut.

3. **Tehakse ärireeglite kontrollid:**
   - Agregaatoril peab olema õigus vastava võrgumõõtepunkti baasjoont esitada.
   - Kontrollitakse tähtaegu ja andmete korrektsust.
   - Kui leitakse viga, tagastatakse kohe **422 (REJECTED)** ning andmeid ei salvestata.

4. **Kui kõik kontrollid läbivad edukalt**, tagastatakse kohe **202 (ACCEPTED)** ning sõnum saab oleku **PROCESSING**.

5. **Andmete salvestamine toimub asünkroonselt** taustprotsessis.

6. **Baasjoone andmete vastuvõtmisel kehtib põhimõte "kõik või mitte midagi":**
   - Kui vähemalt üks periood on vigane, lükatakse kogu sõnum tagasi.
   - Osalist salvestamist ei toimu.

7. **Enne tähtaega võib andmeid uuesti esitada:**
   - Uus edukalt aktsepteeritud väärtus asendab varasema.
   - Arvesse läheb viimane edukalt aktsepteeritud versioon.

8. **Pärast tähtaega andmeid enam muuta ei saa.**

9. **Kõik esitatud sõnumid säilitatakse ajaloos**, sealhulgas tagasi lükatud sõnumid, ning neid saab vaadata [staatuse päringuga](26-baasjoon.md#töötlemise-staatuse-kontrollimine) .

10. **Staatused:**
    - **PROCESSING** – sõnum on vastu võetud ja töötlemisel.
    - **SUCCESSFUL** – andmed on edukalt salvestatud.
    - **REJECTED** – sõnum lükati tagasi valideerimis- või ärireegli vea tõttu.
    - **ERROR** – töötlus lõppes vigadega
``

### Masinliidese sõnum

`POST /api/v1/baseline`

Sõnumi keha on **loend** objektidest, üks iga võrgumõõtepunkti kohta:

**CreateBaselineRequest**

| Atribuut | Tüüp | Kohustuslik? | Selgitus ja reeglid |
| --- | --- | --- | --- |
| `meteringPointEic` | string (EIC) | jah | **Võrgu**mõõtepunkti EIC kood. Peab süsteemis eksisteerima; mõõtepunkti energialiik peab vastama `x-commodity-type` päisele. Üks sõnum ei tohi sisaldada sama mõõtepunkti EIC-d kaks korda. |
| `periods` | loend | jah | Arveldusperioodide loend. Vähemalt üks periood on kohustuslik; perioodide maksimaalne arv sõnumis sõltub konfiguratsioonist. |

**Perioodi objekt**

| Atribuut | Tüüp | Kohustuslik? | Selgitus ja reeglid |
| --- | --- | --- | --- |
| `pS` | string (date-time) | jah | Arveldusperioodi algus, ISO-8601 koos nihkega UTC suhtes (nt 2026-01-01T00:00:00+02:00). Peab langema veerandtunni piirile (hh:00, hh:15, hh:30, hh:45). Peab vastama esitamise tähtajale ja 32 päeva ülempiirile. |
| `inQty` | number | vt allpool | **Tootmise** baasjoon, kWh. Ei või olla negatiivne; null on lubatud; täpsus 0,001 kWh (kolm komakohta). |
| `outQty` | number | vt allpool | **Tarbimise** baasjoon, kWh. Ei või olla negatiivne; null on lubatud; täpsus 0,001 kWh (kolm komakohta). |

> [!WARNING]
> Baasjoone metoodika eeldab iga perioodi kohta **mõlemat** väärtust — nii tarbimist (OUT) kui tootmist (IN). Väärtus 0 tähendab esitatud baasjoont, mille prognoositud kogus on null. Välja puudumine või perioodi kohta kirje puudumine tähendab, et vastavat baasjoont ei ole esitatud.

**Sõnumi reeglid**

- Esitajal peab olema baasjoone esitamise õigus sõnumi **iga** võrgumõõtepunkti ja **iga** perioodi kohta: kehtiv
  agregeerimisleping, mis katab iga esitatud perioodi (hinnatuna perioodi ajahetkel, mis on alati
  tulevikus).
- Tähtaja kontrollis kasutatav esitamise aeg on sõnumi Estfeed Datahubi saabumise aeg.
- Kui **kasvõi üks** periood sõnumis rikub mõnda reeglit (sh tähtaeg, veerandtunni piir, väärtusereeglid,
  õigused), lükatakse **kogu sõnum tagasi** ja midagi ei salvestata. Veavastus loetleb kõik vigased
  perioodid ja reeglid, et sõnumi saaks enne tähtaega parandada ja uuesti esitada. Sõnumi staatuse kontrollimiseks kasuta [staatuse API-t](#töötlemise-staatuse-kontrollimine)
- Sama perioodi uuesti esitamine enne selle tähtaega ei ole viga: uus väärtus asendab vana.
- Baasjoone saatmisel kehtib piirang perioodide arvule, mida saab ühe sõnumiga edastada. Korraga on võimalik saata baasjoont kuni 35 040 perioodi.

**Vastused**

| HTTP | Tähendus |
| --- | --- |
| `202` | Kõik perioodid läbisid valideerimise; sõnum on salvestamiseks järjekorda pandud. Tehnilise tulemuse kinnitamiseks kasuta [staatuse API-t](#töötlemise-staatuse-kontrollimine) oma `x-document-identification` väärtusega. |
| `422` | Äriline tagasilükkamine — midagi ei salvestatud. Vealoend nimetab kõik vigased perioodid ja reeglid. |
| `400` / `403` | Vigane päring / vale energialiik, tururoll või puuduvad õigused. |

Eduka vastuse keha on tühi: äriline otsus on HTTP staatuskood ning salvestamise tulemus on kättesaadav
staatuse API kaudu.

### Veebiliides ja Exceli import

Veebiliides pakub sama funktsionaalsust Exceli failiga:

| Toiming | Selgitus |
| --- | --- |
| Mall | Tühi `.xlsx` mall: võrgumõõtepunkti EIC, perioodi algus, tarbimise baasjoon (kWh), tootmise baasjoon (kWh) |
| Import | Multipart `.xlsx` üleslaadimine. Faili valideeritakse tervikuna (kõik reavead kogutakse kokku ja tagastatakse korraga); korrektne fail töödeldakse täpselt nagu masinliidese sõnum |
| Eksport | [Otsingu](#baasjoone-andmete-küsimine) tulemus `.xlsx` failina; samad parameetrid mis otsingu API-l |


Exceli failiga baasjoone saatmisel on faili mahu piiranguks 35000 rida. Näiteks korraga 31 päeva baasjoone andmete ette edastamisel on võimalik edastada ühe failiga kuni 11 mõõtepunkti kohta baasjoone andmed.

Impordi vastused: `202` = vastu võetud ja järjekorda pandud; `422` koos vealoendiga = faili- või äritaseme
vead, midagi ei salvestatud; `400`/`403` = katkine fail / vale energialiik või roll. Üks import loob ühe
sõnumi (ühe `x-document-identification`), mis on staatuse API-s nähtav täpselt nagu masinliidese esitus.

## Töötlemise staatuse kontrollimine



`GET /api/v1/baseline/status`

Tagastab baasjoone sõnumite töötlemise staatuse ja esituste ajaloo — üks kirje sõnumi kohta, kaasa arvatud
sünkroonselt tagasi lükatud sõnumid.

**Parameetrid**

| Atribuut | Kohustuslik? | Selgitus ja reeglid |
| --- | --- | --- |
| `lastModifiedTimeFrom` | jah | ISO-8601; staatuse viimase muudatuse ajavahemiku algus |
| `lastModifiedTimeTo` | jah | Peab olema suurem kui `from`; ajaakna maksimaalne pikkus sõltub konfiguratsioonist |
| `originalDocumentIdentification` | ei | Esitusega kaasa saadetud `x-document-identification` — kitsenda konkreetse dokumendi/sõnumi ID järgi, näide: 3fa85f64-5717-4562-b3fc-2c963f66afa6 |
| `meteringPointEics` | ei | Kitsenda tulemus konkreetsetele võrgumõõtepunktidele |
| `status` | ei | Üks väärtustest: `REJECTED`, `PROCESSING`, `SUCCESSFUL`, `ERROR` |
| `page` / `size` | ei | Lehekülgede kaupa; vaikimisi 0 / 20, `size` maksimaalselt 500 |

**Vastus** — lehekülgede kaupa; igas kirjes on:

| Atribuut | Selgitus |
| --- | --- |
| `originalDocumentIdentification` | esitatud sõnumi/dokumendi/ ID |
| `receivedTime` | Saabumise aeg, mille suhtes valideeriti baasjoone esitamise õigeaegsust |
| `status` | `REJECTED` (lõplik) \| `PROCESSING` → `SUCCESSFUL` \| `ERROR` |
| `statusMessage` | Inimloetav kokkuvõte |
| `errors` | Struktureeritud vealoend: valideerimisvead staatusel `REJECTED`, salvestamisvead staatusel `ERROR`, muidu tühi |
| `meteringPoints` | Kokkuvõte võrgumõõtepunktide kaupa: `eic`, `periodCount`, `earliestPeriodStart`, `latestPeriodStart` |
| `lastModifiedTime` | Inkrementaalseks pärimiseks |

Staatusekirje (`PROCESSING` → `SUCCESSFUL`) luuakse HTTP 202 ja ärilise valideerimise tõttu tagastatud (`REJECTED`) HTTP 422 vastuste korral (valideerimisvead on toodud väljal errors). Tehniliselt vigase päringu korral, millele tagastatakse HTTP 400 või 403, staatusekirjet ei looda. Agregaator näeb ainult oma sõnumeid.

## Baasjoone andmete küsimine

`GET /api/v1/baseline`

Tagastab baasjoone väärtused koos võrgumõõtepunkti mõõteandmetega ja agregeerimismõõtepunktide
aktiveeritud (mõõdetud) kogustega, valitud agregeerimistasemel.

> [!WARNING]
> Otsingu API parameetrid ja vastuse struktuur on veel lõplikult kinnitamata. Allolev on esialgne
> mustand.

**Parameetrid**

| Atribuut | Kohustuslik? | Selgitus ja reeglid |
| --- | --- | --- |
| `meteringPointEics` | üks valikutest kohustuslik | Võrgu- või agregeerimismõõtepunktide EIC koodid; vähemalt üks; ülempiir sõltub tururollist ja `purpose` väärtusest |
| `resourceEics` | üks valikutest kohustuslik | Alternatiivne valik: ressursi EIC koodid |
| `purpose` | tingimuslik | Päringu eesmärk; määrab lubatud ajaloo sügavuse ja ajaakna pikkuse |
| `periodStart` | jah | Kaasa arvatud |
| `periodEnd` | ei | Välja arvatud; vaikimisi praegune hetk; ajaakna maksimaalne pikkus sõltub `purpose` väärtusest |
| `aggregateBy` | ei | `RESOURCE` \| `GRID_METERING_POINT` \| `AGGREGATION_METERING_POINT` — Vastuse ridade detailsusaste. Vaikimisi kasutatakse valitud parameetri (meteringPointEics või resourceEics) taset |
| `frequencyReserve` | ei | `aFRR` \| `mFRR` — piirab, milliste agregeerimismõõtepunktide aktiveerimiskogused sisalduvad vastuses, kui parameeter ei ole määratud, sisalduvad mõlemad |
| `resolution` | ei | `PT15M` 15 minutit |
| `page` / `size` | ei | Lehekülgede kaupa |

**Vastus** — üks kirje agregeerimisüksuse ja arveldusperioodi kohta:

| Atribuut | Selgitus |
| --- | --- |
| `unit` | Parameetris valitud: ressursi EIC või mõõtepunkti EIC |
| `periodStart`, `resolution` | Arveldusperioodi identiteet (UTC algus) |
| `inResource` / `outResource` | Rea ressursi aktiveeritud koguste summa |
| `inBaseline` / `outBaseline` | Baasjoon: tootmise / tarbimise prognoos (energiasuunad) |
| `inQuantity` / `outQuantity` | Võrgumõõtepunkti mõõteandmed |
| `inActivated` / `outActivated` | Agregeerimismõõtepunktide mõõteandmed (kitsendatud `frequencyReserve` järgi, kui see on antud) |
| `inCorrected` / `outCorrected` | Lõplikud valideeritud reguleerimistarned — tühjad kuni valideerimisetapi käivitumiseni |
| `warnings` | Andmete kättesaadavuse märkused, nt kui mõõteandmed olid ajutiselt kättesaamatud |

Reeglid:

- Agregaator näeb ainult neid võrgumõõtepunkte, mille perioode tema baasjoone esitamise õigus katab — **kaasa arvatud
  ajaloolised perioodid**: agregaator saab pärida baasjooni võrgumõõtepunktide kohta, millega ta oli varem
  seotud.
- Periood, mille kohta baasjoont ei esitatud, tagastatakse **tühjade** baasjooneveergudega. Puuduvaid
  andmeid ei esitata kunagi nullina.
- Agregeerimistasemed: ühe identifikaatori järgi otsides tagastatakse ka seotud tasemed — ressursi põhine päring
  summeerib ressursuga seotud võrgumõõtepunktid; võrgumõõtepunkti päring näitab tema enda väärtusi koos ressursi
  kogusummadega; agregeerimismõõtepunkti päring näitab tema enda aktiveeritud koguseid koos ülem võrgumõõtepunkti
  ja ressursi kontekstiga.

## Ressursi andmete küsimine

`GET /api/v1/resources`

Ressursside register: millised ressursid eksisteerivad ja millised agregeerimismõõtepunktid nendesse
kuuluvad. Ressursse **registreerib ja haldab Elering**; agregaator deklareerib ressursi EIC
agregeerimismõõtepunkti tunnustel mõõtepunkti registreerimisel.

**Parameetrid**

| Atribuut | Kohustuslik? | Selgitus |
| --- | --- | --- |
| `resourceEics` | ei | Filter ressursi EIC järgi |
| `meteringPointEics` | ei | Agregeerimismõõtepunktid — millise ressursiga on mõõtepunkt seotud |
| `validAt` | ei | Kuuluvuse loendi ajahetk; vaikimisi praegune hetk |
| `includeMeteringPoints` | ei | Vaikimisi `true` |
| `page` / `size` | ei | Lehekülgede kaupa |

**Vastuse kirje**: `resourceEic`, `baselineType`, `ownerEic`, `createdTime` ning (kui kaasatud)
`meteringPoints[]` väljadega `eic`, `parentMeteringPointEic`, `validFrom`, `validTo`.

Agregaator näeb ainult oma ressursse.

## Parandused pärast tähtaega ja esitamata baasjoon

Pärast tähtaega ei saa agregaator esitatud baasjoont muuta. On kaks Eleringi vahendatud protseduuri:

1. **Parandamine.** Põhjendatud erandjuhul ja objektiivsete andmete alusel võib Elering juba esitatud
   baasjoont parandada. Parandatud andmepunktid märgistatakse andmekvaliteedi
   märkega *„Andmed muudetud"* ja paranduste ajalugu säilitatakse.
2. **Esitamata baasjoon.** Tähtajaks puuduv baasjoon on baasjoone mitteesitamine
   
> [!CAUTION]
> Möödalastud tähtaeg on agregaatori jaoks lõplik. Planeeri esitused nii, et iga seotud
> võrgumõõtepunkti iga arveldusperiood oleks kaetud vähemalt 30 minutit ette.
