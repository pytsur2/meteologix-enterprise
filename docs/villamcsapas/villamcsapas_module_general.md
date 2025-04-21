# Modul: Villámcsapás (villamcsapas)

## Funkció

Ez a modul felelős a Meteologix rendszerben a villámadatok nyilvános megjelenítéséért.  
Külön frontend, lekérdezési logika és statikus JSON formátumú adatközlés tartozik hozzá.

A cél, hogy a múltbeli villámcsapás-információk elérhetők legyenek a nyilvánosság számára.

---

## Komponensek

| Komponens         | Szerep |
|-------------------|--------|
| `frontend`        | A villamcsapas.hu térképes UI-ja, statikus weboldalként kiszolgálva |
| `query-logic`     | API-ból történő lekérdezések időzítése, aggregálása, cache-elése |
| `json-data`       | Statikus JSON fájlok generálása és publikálása a lekérdezési eredmények alapján |

---

## Modul sajátosságai

- Nem tartalmaz adatbázist, hanem a `core/backend` API-jára támaszkodik
- A frontend teljesen külön áll, akár más domainen is publikálható (`villamcsapas.hu`)
- Időzített lekérdezések és statikus fájl generálás jellemzi (egyszerű, gyors kiszolgálás)

---

## Kapcsolódások más modulokkal

| Modul / Komponens   | Kapcsolat típusa | Leírás |
|---------------------|------------------|--------|
| `core/backend`      | HTTP API         | adatok lekérése villám eseményekről |
| `utils/logger`      | opcionális       | lekérdezési log, hibák naplózása |
| `utils/config-manager` | konfiguráció   | URL-ek, kulcsok, időzítési paraméterek központi kezelése |

---

## Tervezett bővítések

- Frontend lokalizálása (többnyelvűség)
- CSV vagy GeoJSON export
- Email/SMS értesítés integráció (pl. aktív területek figyelése)
- HTTPS / Let's Encrypt automatikus beállítás

---

## Fájlrendszerbeli elhelyezkedés

```
docs/
└── villamcsapas/
    ├── villamcsapas_module_general.md
    ├── frontend/
    ├── query-logic/
    └── json-data/
```
