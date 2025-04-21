# Komponens: Query-logic

**Modul:** villamcsapas

## Funkció

A Query-logic komponens felelős az adatok időzített lekérdezéséért a `core/backend` API-ból.  
Az így lekért adatok lehetnek:

- feldolgozatlanul mentett JSON cache-k,
- aggregált statisztikák,
- vagy célzott, tér-idő szűrésen átesett válaszok.

A komponens célja, hogy a frontendet ne mindig élő API terhelje, hanem gyors, előkészített válaszokat használjon.

---

## Technológiák

- Python 3.x
- `requests` – API hívások
- `schedule` vagy `cron` – időzítés
- `json`, `os`, `datetime` – fájlkezelés, dátumlogika

---

## Felépítés (javasolt)

```
query-logic/
├── run_query.py             # belépési pont
├── queries/
│   ├── recent_lightning.py  # legfrissebb események lekérése
│   └── stats.py             # aggregált adatok lekérdezése
├── cache/
│   └── ...                  # JSON válaszok ide mentve
├── config/
│   └── query_config.yaml    # API URL-ek, lekérdezési paraméterek
```

---

## Kapcsolódási pontok

| Modul / Komponens       | Kapcsolat típusa | Leírás |
|-------------------------|------------------|--------|
| `core/backend`          | HTTP API         | `/api/lightning`, `/api/stats` |
| `villamcsapas/json-data`| fájlmegosztás    | cache eredmények mentése statikus JSON-ként |
| `utils/logger`          | logolás          | kérés státuszok, válaszidők, hibák |
| `utils/config-manager`  | konfiguráció     | API endpointok, lekérdezési paraméterek központi kezelése |

---

## Használat

A komponens időzítve fut (cron vagy `schedule`):

```bash
python run_query.py
```

A script végrehajt:
- API hívásokat (GET /api/lightning)
- válasz mentése JSON fájlba (pl. `cache/lightning_20250421_10h.json`)
- logolás fájlba vagy stdout-ra

---

## Tervezett bővítések

- Lekérdezési státuszfájlok (`last_success`, `last_error`)
- GeoJSON export
- Rugalmas lekérdezési minták definíciója (pl. “utolsó 30 perc Borsod megye”)
- Naplózott, verziózott válasz-cache rendszer

