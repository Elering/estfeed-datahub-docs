# Andmete levitamine

## Sisukord

- [Andmete levitamine](#andmete-levitamine)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [Andmeuuenduste skaneerimine](#andmeuuenduste-skaneerimine)
  - [Andmeuuenduste levitamine](#andmeuuenduste-levitamine)

## Sissejuhatus

Äriprotsesside edukaks ja probleemidevabaks toimimiseks on vaja, et liidestunud turuosaliste süsteemid oleks teadlikud lisandunud ja muutunud informatsioonist.

Selleks on vaja uus info turuosaliste süsteemideni toimetada. Käesolev dokument kirjeldab tehnilist lahendust, kuidas masinate vahelise liidese abil andmete uuendusi levitatakse.

## Andmeuuenduste skaneerimine

Erinevalt vanast Andmelaost, uus Andmeladu sõnumeid liidestuvatatele osapooltele ei saada vaid eeldab, et liidestuv süsteem kontrollib kas talle on uus sõnumeid. Selleks on igale andmeobjektile loodud spetsiaalne uuenduste tõmbamise API liides nimega `/change`, mis toimib standardsel moel:

- liidestunud turuosalise süsteem saadab päringu ning paneb kaasa ajatempli (*timestamp*), millal viimati õnnestus antud andmeobjekti uuendusi edukalt tõmmata.
- Andmeladu otsib andmeobjektid, mis on lisandunud või muutunud pärast ajatempli väärtust.
- Andmeladu filtreerib välja need andmeobjektid või andmeobjekti andmed, mida antud olukorras antud turuosalisele väljastada ei tohi.
- Andmeladu tagastab uued või muutunud andmeobjektid koos Andmelao poolse ID-ga.

Liidestunud turuosalise süsteem skaneerib erinevate andmeobjektide API-d endale sobiva intervalliga võttes arvesse andmeobjektide tekkimise ja muutumise tavapärast sagedust:

- aeglaselt lisanduvaid ja muutuvaid andmeid (nt mõõtepunktid) on sobilik skaneerida näiteks 1-4 korda ööpäevas.
- kiiresti lisanduvaid ja muutuvaid andmeid (nt mõõteandmed) on sobilik skaneerida sama tihendusega, nagu on ette nähtud andmete lisandumine - näiteks iga tund või tihedamalt. See aitab Andmelaol koormuste tippudega paremini toime tulla.

## Andmeuuenduste levitamine

Eleringi meeskond arutab erinevaid tehnilisi lahendusi, kuidas võimaldada võimekamatel liidestunud süsteemidel saada andmeuuendusi kiiremini ja ilma skaneerimiseta. Konkreetne tehniline lahendus on alles välja töötamisel. Selle tekkimisel teavitatakse turuosalisi aegsasti ja põhjalikult.
