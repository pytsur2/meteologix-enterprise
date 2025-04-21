# Meteologix – Adatfeldolgozó folyamat (Data Pipeline) – Áttekintés

Ez a dokumentum a Meteologix rendszer adatfeldolgozó pipeline-jának részletes, lépésenkénti leírását tartalmazza.
A célja, hogy átláthatóvá tegye az időjárási és villámadatok feldolgozásának és adatbázisba töltésének folyamatát,
kiemelve a felépítést, az egymásra épülő scripteket, és a rendszer érzékenységi pontjait.

---

## Funkció

A pipeline célja, hogy két különböző típusú adatot (meteorológiai és villám) külső forrásból letöltsön,
feldolgozzon, szűrjön, és strukturált adatbázisba töltsön – előkészítve az API és frontend kiszolgálást.

---

## Folyamatlépések

### 1. **Adatletöltés**
**Script:** `_1_letoltes.py`

- Külső ZIP fájlok letöltése (meteo és villám forrás)
- Kicsomagolás dedikált könyvtárba
- Előkészítés a feldolgozáshoz

---

### 2. **Metaadatok kinyerése (állomások)**
**Script:** `_2_allomas_frissites.py`

- A meteo CSV fájlok fejlécéből állomásmetaadatokat nyer ki
- Excel és TXT formátumban elmenti
- Alapja az állomásadatbázisnak (geokoordináták, azonosítók)

---

### 3. **Metaadat betöltése adatbázisba**
**Script:** `_3_allomas_adatbetoltes.py`

- Az előzőleg generált Excel fájlt beolvassa
- Betölti a `stations` táblába SQLAlchemy-n keresztül
- Hibakezeléssel, duplikációmentesen

---

### 4. **Villámadat feldolgozás**
**Script:** `_4_villam_feldolgozas.py`

- Magyarország területére szűr
- Soronként ellenőrzi a fájlokat (formátum, koordináta, oszlopszám)
- A jó fájlokat `*_mod.csv` formában menti

---

### 5. **Meteorológiai adatok feldolgozása**
**Script:** `_5_meteo_feldolgozas.py`

- Nyers CSV-k konvertálása szabványosított struktúrába
- Oszlopnevek egységesítése, konverziók
- Validált `*_mod.csv` kimeneti fájlok generálása

---

### 6. **Adatbetöltés az adatbázisba**
**Script:** `_6_feltoltes.py`

- `*_mod.csv` fájlok betöltése MariaDB-be (`LOAD DATA LOCAL INFILE`)
- `meteo_observations` és `villamcsapas_helyszinek` táblák frissítése
- Duplikációk törlése csoportosítással
- Statisztika, naplózás, hibatűrés

---

## Tapasztalatok és tanulságok

- A pipeline jól működik, de érzékeny a forrásfájlok formátumára és elérhetőségére.
- Több script implicit kapcsolatban áll egymással (pl. mappanév, fájltípus, állomáskód).
- Újrafelhasználhatóság nehézkes a dokumentálatlanság miatt – ez most kerül felszámolásra.
- A rendszerben **nincs központi orchestrátor**, cron alapú futtatás valósul meg (ez később cserélhető).
- Erőssége: moduláris, jól elkülönülő lépések
- Gyengesége: kevés validáció és globális állapotfigyelés (ezt érdemes bővíteni)

---

## Jövőbeli irányok

- YAML-alapú pipeline deklaráció
- Centralizált naplózás és hibakezelés
- Verziózott feldolgozási logika (input → output mapping)
- Automatikus adatminőség-ellenőrzés (pl. fájlméret, hash, oszlopszám)

---

## Kapcsolódó modulok

- `modules/data_pipeline/`
- `modules/core_database/`
- `meta/03_REFLECTIONS.md`

