# Komponens: JSON-data

**Modul:** villamcsapas

## Funkció

A JSON-data komponens feladata a lekérdezési logikából származó adatok strukturált, statikus JSON formátumban való elérhetővé tétele.  
Ezeket a fájlokat a frontend közvetlenül betöltheti, így a rendszer független marad az élő API válaszidőtől.

---

## Technológiák

- Python (fájlkezelés, JSON írás)
- `os`, `datetime`, `json` – fájlnevek, timestamp, sorosítás
- (statikus fájlkiszolgálás: NGINX, Python HTTP server)

---

## Fájlstruktúra (javasolt)

```
json-data/
├── public/
│   ├── latest.json              # legutóbbi lekérdezés eredménye
│   ├── stats_day.json           # napi statisztika
│   └── 20250421_10h_lightning.json  # időbélyeges archív fájl
└── generator/
    └── generate_output.py       # fájlmásolatok, validálás, struktúra biztosítás
```

---

## Kapcsolódási pontok

| Modul / Komponens         | Kapcsolat típusa | Leírás |
|---------------------------|------------------|--------|
| `villamcsapas/query-logic`| bemenet (cache)  | lekérdezések eredményét átveszi, formázza |
| `villamcsapas/frontend`   | olvasás          | térképes felület betölti ezeket a fájlokat |
| `utils/config-manager`    | konfiguráció     | output elérési útvonalak, fájlnév sablonok |
| `utils/logger`            | logolás          | fájlgenerálás eredménye, hibák, validációk |

---

## Használat

A komponens a `query-logic` futása után aktiválható vagy automatikusan hívható:

```bash
python generate_output.py
```

A script:
- átmásolja a cache fájlt a `public/` alá (esetleg átnevezi)
- készít `latest.json`, `stats_day.json` linkeket/szimbólumokat
- elvégezhet formátumellenőrzést vagy adatellenőrzést is

A `public/` mappa lehetőséget ad:
- NGINX-en keresztül történő kiszolgálásra
- CDN vagy reverse proxy cache-re

---

## Tervezett bővítések

- JSON fájlok verziózása és hash-elése
- Automatikus validátor (kulcsok, kötelező mezők)
- GeoJSON támogatás
- Aláírt JSON fájlok (hitelesség ellenőrzéshez)

