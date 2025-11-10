# Mõõtepunktid

## Sisukord

<!-- TOC -->
* [Mõõtepunktid](#mõõtepunktid)
  * [Sisukord](#sisukord)
  * [Sissejuhatus](#sissejuhatus)
  * [Mõõtepunkti andmete edastamine](#mõõtepunkti-andmete-edastamine)
    * [Veebiliides](#veebiliides)
    * [Mõõtepunktide masslaadimine](#mõõtepunktide-masslaadimine)
    * [Masinliidese sõnumid](#masinliidese-sõnumid)
      * [Sõnumid](#sõnumid)
        * [Versioonide info](#versioonide-info)
      * [Sõnumite reeglid](#sõnumite-reeglid)
  * [Mõõtepunkti andmete küsimine](#mõõtepunkti-andmete-küsimine)
    * [Masinliidese sõnumid](#masinliidese-sõnumid-1)
      * [Sõnumid](#sõnumid-1)
        * [Versioonide info](#versioonide-info-1)
      * [Sõnumite reeglid](#sõnumite-reeglid-1)
        * [`meter/search` ja `meter/export` reeglid](#metersearch-ja-meterexport-reeglid)
        * [`meter/search/customer` reeglid](#metersearchcustomer-reeglid)
<!-- TOC -->

## Sissejuhatus

Mõõtepunkt on seade, mis mõõdab energia tarbimise ja tootmise koguseid teatud asukohas.

Mõõtepunkte haldavad järgmised turuosalised:

- võrguettevõtja;
- liinivaldaja;
- suletud jaotusvõrgu ettevõtja;
- agregaator;
- tootja;
- laadimispunkti operaator;
- salvestusjaama operaator;
- gaasitankla operaator.

Käesolevas dokumendis nimetatakse neid ühisnimetajaga **Mõõtepunkti haldur**.

Mõõtepunkti haldur vastutab Andmelaos tema piirkonnas olevate mõõtepunktid kohta mõõtepunkti andmete lisamise ja uuendamise eest.

> [!WARNING] 
> NB! Mõõtepunkti haldur on kohustatud mõõtepunkti andmeid uuendama esimesel võimalusel.

## Mõõtepunkti andmete edastamine

Mõõtepunkti haldur saab mõõtepunktide tehnilised andmed edastada Andmelattu:

- ükshaaval veebiliidese või vastava automaatse andmevahetuse liidese kaudu
- masslaadimisega veebiliidese või vastava automaatse andmevahetuse liidese kaudu

Mõõtepunktide andmed on samalaadsed nii andmevahetuse teenustes kui ka veebiliides. Mõõtepunkti andmed on:

- Ühised andmed kõikidele mõõtepunktidele:

| Atribuut teenuses | Tulba nimetus masslaadimise templiidis | Selgitus                         | Kohustuslik? | Muud reeglid                                                                                        |
|-------------------|----------------------------------------|----------------------------------|--------------|-----------------------------------------------------------------------------------------------------|
| meterEic          | Metering Point EIC                     | mõõtepunkti 16 kohaline EIC kood | jah          | Peab olema valiidne EIC kood ja mahtuma eraldatud EIC koodi vahemikku                               |
| meteringType      | Metering Type                          | mõõtmise viis                    | jah          | Üks neist: REMOTE_READING (kaugloetav), VIRTUAL (virtuaalne), NON_REMOTE_READING (mitte kaugloetav) |
| meteringPointType | Metering Point Type                    | mõõtepunkti tüüp                 | jah          | Üks neist: REGULAR (tavaline), INTERNAL (sisemine), BORDER(piiri), AGGREGATION (agregeerimise)      |

- Elektri ja gaasi mõõtepunktide ühised metaandmed:

| Atribuut teenuses      | Tulba nimetus masslaadimise templiidis | Selgitus                                 | Kohustuslik?             | Muud reeglid                                                                                                                                                                                                                  |
|------------------------|----------------------------------------|------------------------------------------|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| consumptionScale       | Consumption Scale                      | tarbimise maht mõõtepunktis              | jah                      | Üks neist: SMALL (väiketarbija), LARGE (suurtarbija)                                                                                                                                                                          |
| connectionState        | Conection State                        | ühenduse olek mõõtepunktis               | jah                      | Üks neist: CONNECTED (ühendatud), DISCONNECTED (katkestatud)                                                                                                                                                                  |
| resolution             | Resolution                             | mõõtepunkti resolutsioon                 | jah                      | Üks neist: PT15M (15 minutit), PT1H (1 tund)                                                                                                                                                                                  |
| customerType           | Customer Type                          | tarbimise tüüp mõõtepunktis              | jah                      | Üks neist:  CONSUMER (tarbija), GRID_OPERATOR (võrguettevõtja), PRODUCER (tootja), MICRO (mikrotootja), LINE_OPERATOR (liinivaldaja), ENERGY_STORAGE_UNIT (salvestusjaam), CHARGING_POINT_OPERATOR (laadimispunkti operaator) |
| production             | Production                             | kas mõõtepunktis toimub energia tootmist | jah                      | Üks neist: TRUE (jah), FALSE (ei)                                                                                                                                                                                             |
| productionSource       | Production Source                      | energia tootmise allikas                 | jah, kui production=true | Üks neist: SOLAR (päike), WIND (tuul), HYDRO (vesi), BIOGAS (biogaas), BIOMASS (biomass), NATURAL_GAS (gaas), OIL_SHALE (põlevkivi), OTHER_RENEWABLE (muu taastuv), OTHER_NON_RENEWABLE (muu mittetaastuv)                    |
| transmissionNetworkEic | Transmission Network EIC               | ülekandevõrgu 16 kohaline EIC kood       | jah                      | Määratud ülekandevõrgu EIC kood peab eksisteerima süsteemis. Energiakandja tüüp peab ühtima mõõtepunkti omaga. Koodi puudumisel võib kasutada koodi 38A-1234567890-1.                                                         |
| apartmentAssociation   | Apartment Association                  | kas tegu on korteriühistuga              | jah                      | Üks neist: TRUE (jah), FALSE (ei)                                                                                                                                                                                             |

- Elektri mõõtepunkti spetsiifilised metaandmed:

| Atribuut teenuses     | Tulba nimetus masslaadimise templiidis | Selgitus                                  | Kohustuslik V1 versioonis? | Kohustuslik V2 versioonis? | Muud reeglid                                                                                |
|-----------------------|----------------------------------------|-------------------------------------------|----------------------------|----------------------------|---------------------------------------------------------------------------------------------|
| isolatedMeteringPoint | Isolated Metering Point                | kas tegemist on isoleeritud mõõtepunktiga | jah                        | jah                        | Üks neist: TRUE (jah), FALSE (ei)                                                           |
| electricalHeating     | Electrical Heating                     | kas mõõtepunktis toimub elektriga kütmist | jah                        | jah                        | Üks neist: TRUE (jah), FALSE (ei)                                                           |
| chargingPoint         | Charging Point                         | kas mõõtepunktis toimub elektri laadimist | jah                        | jah                        | Üks neist: TRUE (jah), FALSE (ei)                                                           |
| storageCapacity       | Storage Capacity                       | energiasalvestusvõimsus (kW)              | ei                         | jah                        | Peab olema täis- või komakohaga (max. 2 komakohta)number. Väärtuse puudumisel jätta tühjaks |
| storageEnergy         | Storage Energy                         | energiasalvesti mahtuvus (kWh)            | ei                         | jah                        | Peab olema täis- või komakohaga (max. 2 komakohta)number. Väärtuse puudumisel jätta tühjaks |
| productionCapacity    | Production Capacity                    | tootmise maht (kW)                        | ei                         | jah                        | Peab olema täis- või komakohaga (max. 2 komakohta)number. Väärtuse puudumisel jätta tühjaks |
| transmissionCapacity  | Transmission Capacity                  | ülekande maht (kW)                        | ei                         | jah                        | Peab olema täis- või komakohaga (max. 2 komakohta)number. Väärtuse puudumisel jätta tühjaks |

- Agregeerimise mõõtepunkti spetsiifilised metaandmed:

| Atribuut teenuses         | Tulba nimetus masslaadimise templiidis | Selgitus                             | Kohustuslik V1 versioonis? | Kohustuslik V2 versioonis?       | Muud reeglid                                                                                                                              |
|---------------------------|----------------------------------------|--------------------------------------|----------------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| parentMeterEic            | Parent Metering Point EIC              | ülemmõõtepunkti 16 kohaline EIC kood | jah                        | jah                              | Peab viitama Andmelaos registreeritud tava mõõtepunktile. Väärtuse muutmine ei ole lubatud.                                               |
| aggregationProductType    | Agregation product type                | Agregeerimise toote tüüp             | -                          | jah                              | Üks neist: MFRR, AFRR, FCR, D1, D, LOCAL_PRODUCT. Väärtuse uuendamine on lubatud ainult siis, kui eelnev väärtus puudub.                  |
| assetType                 | Asset type                             | Mõõtepunkti vara tüüp                | -                          | jah                              | Üks neist: CONSUMPTION, PRODUCTION. Väärtuse uuendamine on lubatud ainult siis, kui eelnev väärtus puudub.                                |
| aggregationProductionType | Aggregation production type            | Mõõtepunkti tootmise tüüp            | -                          | jah, kui vara tüüp on PRODUCTION | Üks neist: BESS, BV, WIND, HYDRO, OTHER. Väärtuse uuendamine on lubatud ainult siis, kui eelnev väärtus puudub ja vara tüüp on PRODUCTION |
| resourceEic               | Resource EIC                           | Ressursi EIC                         | -                          | jah                              | Ei pea viitama Andmelaos registreeritud EIC koodile. Väärtuse uuendamine on lubatud ainult siis, kui eelnev väärtus puudub.               |

- Ühised aadressi andmed kõikidele mõõtepunktidele:

| Atribuut teenuses | Tulba nimetus masslaadimise templiidis | Selgitus                                              | Kohustuslik V1 versioonis?              | Kohustuslik V2 versioonis?     | Muud reeglid                                                                                                                                    |
|-------------------|----------------------------------------|-------------------------------------------------------|-----------------------------------------|:-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| adrId             | Adr ID                                 | Maaameti ADS süsteemi aadressi ID (ADR_ID)            | jah kui county ja municipality on puudu | ei                             | Peab olema täisarv                                                                                                                              |
| comment           | Comment                                | kommentaar                                            | ei                                      | ei                             |                                                                                                                                                 |
| county            | County                                 | maakond (ADS tase 1)                                  | jah                                     | jah                            |                                                                                                                                                 |
| municipality      | Municipality                           | vald, linn(ADS tase 2)                                | jah                                     | jah                            |                                                                                                                                                 |
| locality          | Locality                               | asustusüksus(ADS tase 3)                              | ei                                      | jah                            |                                                                                                                                                 |
| streetAddress     | Street Address                         | kohaadress (tänav, maja, korter jne, ADS tasemed 4-8) | jah                                     | jah                            |                                                                                                                                                 |
| postcode          | Postcode                               | sihtnumber                                            | jah                                     | jah                            | Õige sihtnumbri puudumisel tuleks kasutada sihtnumbrina 00000.                                                                                  |
| latitude          | Latitude                               | koordinaadi laiuskraad                                | ei                                      | ei                             | LEST97 puhul peab väärtus olema olema 7 kohta enne ja 1-3 kohta peale koma. WGS84 puhul peab väärtus olema 2 kohta enne ja 4-8 kohta peale koma |
| longitude         | Longitude                              | koordinaadi pikkuskraad                               | ei                                      | ei                             | LEST97 puhul peab väärtus olema olema 6 kohta enne ja 1-3 kohta peale koma. WGS84 puhul peab väärtus olema 2 kohta enne ja 4-8 kohta peale koma |
| coordinateSystem  | Coordinate Sytem                       | koordinaatsüsteem                                     | jah, kui koordinaadid on antud          | jah, kui koordinaadid on antud | Üks neist: WGS84, LEST97                                                                                                                        |

> [!NOTE]
> Aadressi andmete struktuur ja validatsioonid on täiendamisel

### Veebiliides

Vajadusel on võimalik järgmine vaba mõõtepunkti EIC kood genereerida veebiliidese kaudu navigeerides "Metering points" -> "Metering Point Bulk Import" lehele. Täpsustada tuleb soovitud EIC koodide arv.

![EIC koodi genereerimine](../images/opp-ui/metering-point/generate-EIC.png)

Mõõtepunkti lisamiseks veebiliideses on 2 võimalust:

- ükshaaval;
- masslaadimisega.

Ükshaaval laadimiseks tuleks navigeerida "Metering points" lehele.

1. Alustuseks tuleks vajutada nupule "New".
2. Seejärel on vaja avanevas modaalaknas täita kõik kohustuslikud väljad (märgitud tärniga).
3. Kui "Create" nupp on mitteaktiivne on tõenäoliselt jäänud mõni kohustuslik väli täitmata.

![Uue mõõtepunkti lisamine](../images/opp-ui/metering-point/add-meter-point-1.png)

![Uue mõõtepunkti andmete täitmine](../images/opp-ui/metering-point/add-meter-point-2.png)

Mõõtepunktide masslaadimine on võimalik MS Excel faili abil navigeerides "Metering points" -> "Metering Point Bulk Import" lehele.

1. Vajutades lehel "Download" nupule on võimalik allalaadida template.
2. "Import" nupp avab modaalakna.
3. Seejärel on võimalik lisada mõõtepunki(de) andmetega täidetud fail.

![Mõõtepunktide masslaadimine](../images/opp-ui/metering-point/meter-point-import.png)

Mõõtepunktide otsimiseks tuleks navigeerida "Metering points" lehele.

1. Soovi korral on võimalik lisada 1 või rohkem otsingukriteeriumit.
2. Ilma ühtegi välja täitmata ja kohe "Search" nuppu vajutades väljastatakse kõigi mõõtepunktide andmed.
Ühe või rohkema otsingukriteeriumi lisamisel väljastatakse vaid nendele kriteeriumitele vastavad mõõtepunktid.
3. Võimalik on otsingut täpsustada täiendavate kriteeriumitega, need valikud avanevad vajutades "Detailed search" nupule.

![Mõõtepunktide otsimine](../images/opp-ui/metering-point/meter-point-search.png)

Peale mõõtepunkti otsingu tulemuste saamist on võimalik:
1. vaadata mõõtepunkti mõõteandmeid;
2. vaadata mõõtepunktiga seotud lepinguid;
3. muuta mõõtepunkti andmeid.

Kirjeldatud on mõõtepunkte haldavate turuosaliste õigused, teistel rollidel mõõtepunkti muutmise õigus puudub.

![Mõõtepunktide informatsioon](../images/opp-ui/metering-point/meter-point-info.png)

### Mõõtepunktide masslaadimine

Nii veebiliideses kui ka andmevahetuse liideses on loodud võimalus mõõtepunkide masslaadimiseks MS Excel faili abil. Selleks tuleb veebiliidese või teenuse `template` kaudu laadida alla energikandja liigi spetsiifiline templiit, lisada andmed ning täidetud templiit uuesti veebi või teenuse `import` vahendusel üles laadida.

Mõõtepunkti andmed on kirjeldatud peatükis [Mõõtepunkti andmete edastamine](#mõõtepunkti-andmete-edastamine), kuid esineb üks erisus - kuivõrd andmete templiit on juba energiakandja tüübi spetsiifiline, siis mõõtepunkti tüüpi tuleb täpsustada ainult elektri või gaasi mõõtepunkti puhul (REGULAR või INTERNAL).

### Masinliidese sõnumid

#### Sõnumid

| V1 Sõnum                      | V2 Sõnum                      | Eesmärk                                             |
|-------------------------------|-------------------------------|-----------------------------------------------------|
| `POST /api/v1/meter`          | `POST /api/v2/meter`          | Mõõtepunkti lisamine                                |
| `PUT /api/v1/meter`           | `PUT /api/v2/meter`           | Mõõtepunkti muutmine                                |
| `POST /api/v1/template/meter` | `POST /api/v2/template/meter` | Mõõtepunktide masslisamise templiidi alla laadimine |
| `POST /api/v1/meter/import`   | `POST /api/v2/meter/import`   | Mõõtepunktide massimport templiidi abil             |
| `POST /api/v1/eic/amount`     | -                             | **Enda** EIC vahemikust vabade EIC koodide otsing   |
| `POST /api/v1/eic/range`      | -                             | Turusalise **enda** EIC koodi vahemike otsing       |

##### Versioonide info

V2 versiooni lisandumisel toimusid järgmised muudatused:
  - V2 versioonis lisandusid agregeerimise mõõtepunktile 4 uut atribuuti: `aggregationProductType`, `assetType`, `aggregationProductionType` ja `resourceType`. 
  - V2 versioonis muutusid asukoha ja elektri mõõtepunkti spetsiifiliste atribuutide kohustuslikkuse reeglid 
  - V1 versioonis pole enam võimalik lisada ega muuta agregeerimise mõõtepunkte

#### Sõnumite reeglid

- Mõõtepunkti EIC kood peab jääma võrguettevõtja mõne EIC koodide vahemiku piiresse
- Mõõtepunki sõnumi `marketParticipantContext.commodityType` määrab mõõtepunkti energiakandja liigi ning sellest tulenevalt lubatud metaandmestiku:
  - väärtuse `ELECTRICITY` puhul - lubatud ja nõutud on elektri või agregeerimise metaandmestik;
  - väärtuse `NATURAL_GAS` puhul - lubatud ja nõutud on gaasi või agregeerimise metaandmestik;
- Mõõtepunkti tüüp defineerib lubatud metaandmestiku:
  - regulaarne, piirimõõtepunkt, sisemine - lubatud on gaasi või elektri metaandmestik;
  - agregeerimise - lubatud on agregeerimise metaandmestik;
- Mõõtepunkti resolutsioon on täiendav info ja ei mõjuta mõõteandmete edastamist tulevikus vaid iseloomustab, kas mõõtepunkt suudab  reaalsuses tarbimist mõõta 15 minuti, 1 tunni või päeva täpsusega.
- XY koordinaatide reeglid:
  - XY koordinaadid ei ole nõutud;
  - XY koordinaadid peavad olema numbrid, mis võivad sisaldada komakohtasid;
  - XY koordinaadid peavad jääma Eestit ümbritseva mõttelise ristküliku sisse;
- Elektri tava mõõtepunkti loomiseks peab `marketParticipantRole` väärtus olema üks neist:
  - GRID_OPERATOR
  - LINE_OPERATOR
  - CLOSED_DISTRIBUTION_NETWORK
  - PRODUCER_OPERATOR
  - CHARGING_POINT_OPERATOR
- Gaasi tava mõõtepunkti loomiseks peab `marketParticipantRole` väärtus olema üks neist:
  - GRID_OPERATOR
  - PRODUCER_OPERATOR
- Piiri mõõtepunkti loomiseks peab `marketParticipantRole` väärtus olema üks neist:
  - GRID_OPERATOR
- Agregeerimise mõõtepunkti loomiseks peab `marketParticipantRole` väärtus olema AGGREGATOR
- Aadressi tekstilisel kujul saatmise korral on andmekvaliteedi huvides palve kasutada ametlikke [EHAK klassifikaatoris](https://klassifikaatorid.stat.ee/Item/stat.ee/c4c47742-12d7-4fea-bc8c-5aeca9112e2a/88) toodud maakonna, omavalitsuse ja asutusüksuse nimekujusid.

## Mõõtepunkti andmete küsimine

Üldiselt võivad kõik õigustatud kasutajad pärida mõõtepunktide andmeid kasutades `search` teenuseid, kuid avatud tarnija ja bilansihaldur saavad pärida ka uute ja muutunud mõõtepunktide andmete uuendusi kasutades andmete levitamise teenust.

### Masinliidese sõnumid

#### Sõnumid

| V1 Sõnum                             | V2 Sõnum                             | Eesmärk                                                                                                                                                                                                         |
|--------------------------------------|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `POST /api/v1/meter/search`          | `POST /api/v2/meter/search`          | Mõõtepunktide otsing erinevate tunnuste alusel. Vaata järgnevaid peatükke reeglite osas.                                                                                                                        |
| `POST /api/v1/meter/search/customer` | `POST /api/v2/meter/search/customer` | Leida kliendi mõõtepunktid (aktiivsete või tulevikus aktiveeruvate GRID lepingutega) kliendi EIC koodi alusel selleks, **et luua uus SUPPLY leping** (võrgueeskirja §8 lg 5 ette nähtud kontrolli teostamiseks) |
| `POST /api/v1/meter/search/border`   | -                                    | Piirimõõtepunkti otsing                                                                                                                                                                                         |
| `POST /api/v1/meter/export`          | `POST /api/v2/meter/export`          | Mõõtepunktide eksportimine erinevate tunnuste alusel. Vaata järgnevaid peatükke reeglite osas.                                                                                                                  |

> [!CAUTION] 
> Teenust `POST /api/{version}/meter/search/customer` on lubatud kasutada ainult uue lepingu loomisel ja selle õiguspärast kasutamist monitooritakse

##### Versioonide info

- V2 versioonis lisandusid agregeerimise mõõtepunktile 4 uut atribuuti: `aggregationProductType`, `assetType`, `aggregationProductionType` ja `resourceType`.

#### Sõnumite reeglid

##### `meter/search` ja `meter/export` reeglid

- Andmeladu väljastab kõik mõõtepunkti andmed juhul kui:
  - andmete pärija on mõõtepunkti omanik
  - andmete pärijal on Kliendiportaali kaudu väljastatud ligipääsuõigus
  - andmete pärija on avatud või nimetatud tarnija, kellel on hetkel aktiivne (või oli viimase 12 kuu jooksul aktiivne) avatud või nimetatud tarne leping antud mõõtepunktis
  - andmete pärija on agregaator, kellel on hetkel aktiivne (või oli viimase 12 kuu jooksul aktiivne) agregeerimise leping mõnes antud mõõtepunkti alammõõtepunktis
  - andmete pärija on ülemmõõtepunkti omanik ja päritakse mõne alammõõtepunkti andmeid
- Ülejäänud juhtudel andmeid ei tagastata

##### `meter/search/customer` reeglid

- Andmeladu väljastab kõik mõõtepunkti andmed juhul kui:
  - andmete pärijal on Kliendiportaali kaudu väljastatud ligipääsuõigus
  - andmete pärija on avatud või nimetatud tarnija, kellel on hetkel aktiivne (või oli viimase 12 kuu jooksul aktiivne) avatud või nimetatud tarne leping antud mõõtepunktis
  - andmete pärija otsib juriidilise isiku või organisatsiooni mõõtepunkte ja kinnitab, et tal on süsteemiväline kirjalikku taasesitust võimaldavas vormis volitus (`legalConsent` väärtus on `true`)
- Ülejäänud juhtudel tagastatakse ainult mõõtepunkti EIC kood
