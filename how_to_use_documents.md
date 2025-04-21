# Dokumentációs útmutató – 'Házmester fájl'

Ez a dokumentum segít eligazodni a Meteologix projekt dokumentációs rendszerében:  
összefoglalja, hogy milyen típusú dokumentumok készülnek, mire valók, kinek szólnak, és hol találhatók.

---

## 🧭 Dokumentumtípusok és céljaik

| Dokumentumtípus | Kiterjesztés | Szerep | Kinek szól | Tartalom |
|------------------|--------------|--------|------------|----------|
| **Projektleíró** | `*_general.md` | A projekt vagy modul céljának, szerepének leírása | mindenki | stratégiai, kontextus |
| **Komponensleíró** | `*_component_general.md` | Egy komponens technikai és funkcionális ismertetése | fejlesztő | technikai dokumentáció |
| **Technikai README** | `README.md` | Általános technikai sablon, fejlesztés közbeni placeholder | fejlesztő | fájlstruktúra, usage |
| **Meta** | `meta/*.md` | Rendszerszintű reflexiók, térképek, jövőkép | vezető fejlesztő, tananyag | roadmap, komponenskapcsolatok |
| **Általános architektúra** | `ARCHITECTURE.md` | A teljes rendszer modul–komponens struktúrája | mindenki | összefoglaló, linkek |
| **Főképviseleti fájl** | `meteologix_enterprise_general.md` | A teljes rendszer legfelső szintű célkitűzése | mindenki | vízió, célok, filozófia |

---

## 📁 Dokumentációs fájlrendszer logikája

```
docs/
├── ARCHITECTURE.md                # teljes rendszer architektúra
├── <modulnév>/
│   ├── <modulnév>_module_general.md     # modul cél, tartalom, kontextus
│   └── <komponens>/
│       └── <komponens>_component_general.md # funkció, kapcsolatok, használat
│       └── README.md                # technikai sablon (fejlesztés alatt állók)
meta/
├── 00_SYSTEM_OVERVIEW.md          # magas szintű leírás
├── 01_COMPONENT_MAP.md            # vizuális komponenskép
├── 02_ROADMAP.md                  # stratégiai terv
├── 03_REFLECTIONS.md              # reflexiók, tanulságok

meteologix_enterprise_general.md   # a projekt legfelső szintű célkitűzése
```

---

## 📌 Tájékozódási javaslatok

- Új csapattagként: `meteologix_enterprise_general.md` → `ARCHITECTURE.md` → `docs/<modul>_module_general.md`
- Fejlesztőként: menj a megfelelő `docs/<modul>/<komponens>/<komponens>_component_general.md` fájlhoz
- Dokumentálás alatt álló elemnél: `README.md` fájl placeholderként szolgál
- Stratégiai döntés vagy tervezés: `meta/` mappa
- Komplett rendszerkép: `ARCHITECTURE.md`

---

## 🗂 Megjegyzések

- A `README.md` fájlok **boilerplate-ként** szolgálnak, míg az `*_general.md` fájlok **kidolgozott tartalom**.
- A dokumentáció célja a teljes rendszer **auditálhatósága, újrafelhasználhatósága és tanulhatósága**.

---

Ezt a fájlt ajánlott minden dokumentációs mappa elejére elhelyezni `00_README_NAVIGATOR.md` néven.
