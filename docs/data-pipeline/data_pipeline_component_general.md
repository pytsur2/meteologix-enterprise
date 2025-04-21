# Modul: Data-flow

## Funkció

A `data-flow` modul a Meteologix rendszer adatfeldolgozó láncát valósítja meg. Feladata a külső forrásból származó meteorológiai és villámcsapás-adatok:

1. letöltése,
2. feldolgozása és validálása,
3. strukturált adatbázisba történő betöltése.

A feldolgozás lépésenkénti Python scriptekre van bontva, amelyek `cron`-nal időzítve futnak, és kimenetük egy következő script bemenete.

---

## Feldolgozási lépések és scriptek

### 1. `_1_letoltes.py`
- Külső ZIP fájlok letöltése
- Kicsomagolás dedikált könyvtárba
- Előkészítés a további feldolgozáshoz

### 2. `_2_allomas_frissites.py`
- Metaadatok (állomások) kinyerése meteo fájl fejlécéből
- Kimenet: Excel, TXT (állomásnév, koordináta, azonosító)

### 3. `_3_allomas_adatbetoltes.py`
- Az előző Excel fájl adatbázisba töltése (`stations` tábla)
- SQLAlchemy használatával, duplikációkezeléssel

### 4. `_4_villam_feldolgozas.py`
- Villámadatok szűrése magyar területre
- Strukturális ellenőrzések, hibás sorok kiszűrése
- Validált `*_mod.csv` mentése

### 5. `_5_meteo_feldolgozas.py`
- Meteorológiai CSV fájlok struktúrájának egységesítése
- Oszlopok átnevezése, konverziók, validáció
- Validált `*_mod.csv` fájlok generálása

### 6. `_6_feltoltes.py`
- `*_mod.csv` fájlok betöltése MariaDB-be (`LOAD DATA`)
- Táblák: `meteo_observations`, `villamcsapas_helyszinek`
- Duplikációk szűrése, statisztika, logolás

---

## Kapcsolódási pontok

| Modul / Komponens       | Kapcsolat típusa | Leírás |
|-------------------------|------------------|--------|
| `core/db`               | adatbázis        | SQL kapcsolat MariaDB-be a 3. és 6. scriptnél |
| `utils/logger`          | naplózás         | hibák, statisztikák naplózása (jövőbeli terv) |
| `core/backend`          | indirekt         | betöltött adatok elérhetővé válnak API-n keresztül |
| `utils/config-manager`  | konfiguráció     | paraméterek YAML-ben, input/output elérési utak |

---

## Használat

A scriptek önállóan futtathatók fejlesztés közben:

```bash
python _1_letoltes.py
python _2_allomas_frissites.py
...
python _6_feltoltes.py
```

Éles környezetben időzítve futnak `cron` segítségével.

Kimenetek:
- Nyers és validált CSV fájlok (köztes eredmények)
- Betöltött adatok a `core/db` tábláiban

---

## Tervezett bővítések

- Központi YAML-alapú pipeline definíció
- JSONL logolás minden scripthez
- Adatminőség ellenőrzés: fájlméret, oszlopszám, hash
- Hibakezelési központ (pl. Slack / email értesítés)
- Job status fájlok: `last_successful`, `last_error`

---

## Forrás

Részletes folyamatleírás: [`data_flow_module_general.md`](./data_flow_module_general.md)

Kódok helye: `modules/data_pipeline/`
