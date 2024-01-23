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

Erinevalt vanast Andmelaost, uus Andmeladu sõnumeid liidestuvatatele osapooltele ei saada vaid eeldab, et liidestuv süsteem kontrollib kas talle on uus sõnumeid. Selleks on loodud spetsiaalne uuenduste tõmbamise API liides `/data-distribution/search `, mis toimib standardsel moel:

- liidestunud turuosalise süsteem saadab päringu defineerides ajavahemiku ja andmeobjekti tüübi(d).
- Andmeladu leiab eelnevalt genereeritud andmete levitamise sõnumid, mille adressaat on sõnumi saatnud turuosaline ning mis vastavad päringu tingimustele.
- Andmeladu tagastab uued või muutunud andmeobjektide andmed koos muudatuse põhjendusega.

Liidestunud turuosalise süsteem skaneerib muudatuste API-t endale sobiva intervalliga võttes arvesse andmeobjektide tekkimise ja muutumise tavapärast sagedust:

- aeglaselt lisanduvaid ja muutuvaid andmeid (nt mõõtepunktid) on sobilik skaneerida näiteks 1-4 korda ööpäevas.
- kiiresti lisanduvaid ja muutuvaid andmeid (nt mõõteandmed) on sobilik skaneerida sama tihendusega, nagu on ette nähtud andmete lisandumine - näiteks iga tund või tihedamalt. See aitab Andmelaol koormuste tippudega paremini toime tulla.

## Andmeuuenduste levitamine

Eleringi meeskond arutab erinevaid tehnilisi lahendusi, kuidas võimaldada võimekamatel liidestunud süsteemidel saada andmeuuendusi kiiremini ja ilma skaneerimiseta. Konkreetne tehniline lahendus on alles välja töötamisel. Selle tekkimisel teavitatakse turuosalisi aegsasti ja põhjalikult.
