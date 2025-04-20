# Meteologix – Rendszer-áttekintés és Projektszemlélet

## Mi ez a projekt?

A Meteologix nem csupán egy meteorológiai adatokat szolgáltató rendszer.  
Ez egy **komplex, többdimenziós vállalati prototípus**, ahol:

- működő szolgáltatások születnek,
- valós üzleti célokat szolgáló modulok épülnek,
- és közben dokumentáltan modellezem az **infrastruktúra, üzemeltetés, fejlesztés, biztonság, tesztelés és döntéshozatal** teljes ívét.

Ez nem csak egy rendszer, hanem egy **labor**, ahol:
- önállóan, de vállalati szemlélettel építem újra azt, amit általában külön DevOps, backend, frontend, SOC és analyst csapatok kezelnek.
- nem egyetlen szerepkörben működöm, hanem **interdiszciplináris gondolkodásban**.

---

## A rendszer célja

**Üzleti szempontból:**  
Lehetővé tenni időjárási adatok lekérdezését konkrét biztosítási célokra.

### Fő felhasználási területek:
1. **Biztosítótársaságok backoffice munkatársai**  
   - Validálják, hogy egy adott időben és helyen történt-e biztosítási esemény (pl. jégeső, vihar).
2. **Ügyfelek**  
   - Előzetesen ellenőrizhetik, hogy kárigényük valószínűsíthetően elfogadható-e.

**Technológiai szempontból:**  
Egy stabil, jól dokumentált, moduláris architektúra, amely támogatja:
- időjárási adatpipeline-ek működtetését,
- API-k kiszolgálását,
- user managementet,
- biztonságos üzemeltetést és skálázhatóságot.

---

## Miért jött létre?

### *Mert nem az eszközök számítanak – hanem az, hogy tudom, hogyan építem fel őket.*

Ez a projekt egyben válasz:
- a túlspecializált, egymástól elszigetelt szerepkörökre,
- a széttöredezett vállalati folyamatokra,
- és az átláthatatlan, újra nem építhető rendszerekre.

---

## Személyes céljaim

### 1. **Valós, működő szolgáltatást építeni**
- amely piacképes, használható, és valódi értéket ad.

### 2. **A gondolkodásmódomat dokumentálni**
- minden döntést, tanulságot, elágazást rögzíteni,
- nem csak a kódot, hanem a mögöttes szándékot is láthatóvá tenni.

### 3. **Tanulhatóvá tenni a teljes folyamatot**
- a rendszer ne csak működjön, hanem tanítható, újraépíthető, adaptálható legyen.

---

## Ki vagyok én ebben a projektben?

Nem vagyok...

- …**developer**
- …**enterprise admin**
- …**SOC analyst**
- …**code camp oktató**

**Sőt. Egyik SEM vagyok.**

Nem egy szerepkörből tekintek a rendszerre –  
hanem **együtt látom az egészet**: az infrastruktúrát, a kódot, a döntést, a tanulást, az átláthatóságot.

Ez nem karrierút.  

Ez **belső konstrukció**: egy rendszer- és gondolkodásmód, amit magamnak építek – és mások számára is láthatóvá teszek.

Hanem olyan alkotó, aki **egyetlen gondolati egységként kezeli**:
- a szolgáltatást,
- az architektúrát,
- a döntéshozatalt,
- a dokumentációt,
- és a tanulási folyamatot.

---

## Elsődleges célok

- Egy működő meteorológiai szolgáltatás biztosítási validációhoz.
- Stabil adatpipeline, kiszolgáló backend, jogosultságkezelés, frontend interfész.
- Piacképes prototípus: eladható, bővíthető, használható.

## Másodlagos célok

- Részletes, reflektív dokumentáció: *hogyan épül fel egy termék a nulláról?*
- Fejlesztési tanulmány: tananyag, coaching eszköz.
- Személyes portfólió: nem csak kód, hanem gondolkodás bemutatása.

---

## Fő komponensek (moduláris felépítés)

- `data_pipeline`: Külső időjárási adatok letöltése, feldolgozása, betöltése
- `core_database`: Adatmodell és séma karbantartás
- `api_core`: Központi API-k az adatok kiszolgálására
- `user_auth`: Jogosultságkezelés, audit, session control
- `frontend`: Interaktív felhasználói felület
- `infrastructure`: Docker-compose, VPN, firewall, monitoring
- `meta`: Projektfilozófia, reflexiók, dokumentációs tér

---

## Hogyan haladok?

A fejlesztés **moduláris és iteratív**, de mindig egy központi cél mentén zajlik:
- nem adhoc építkezem,
- nem funkciót toldok, hanem keretrendszert bővítek.

---

## Záró gondolat

**Ez nem csak egy rendszer.  
Ez annak a tudásnak az összegzése, hogyan építünk fel valamit az alapoktól –  
úgy, hogy az ne csak működjön, hanem tanítható és újraépíthető is legyen.**

