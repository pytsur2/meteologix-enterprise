# Meteologix – Fejlesztési ütemterv (ROADMAP)

Ez a dokumentum a Meteologix projekt fejlesztési fázisait rögzíti –  
nem klasszikus tasklistaként, hanem gondolkodási és építkezési ívként.

A roadmap célja nem az, hogy „készen legyünk”, hanem hogy **átlássuk az utat**,  
és minden szakaszban reflektált döntéseket hozzunk.

---

## 1. Alapozó fázis – Projektkeret létrehozása

**Cél:**  
Létrehozni azt a keretet, amelyben minden más komponens elhelyezhető – strukturálisan és gondolatilag is.

**Feladatok:**
- `README.md` – nyitó üzenet, célkép
- `meta/00_SYSTEM_OVERVIEW.md` – projekt identitás, üzleti célok, gondolkodásmód
- `meta/01_COMPONENT_MAP.md` – komponensszintű térkép
- `meta/02_ROADMAP.md` – jelen dokumentum
- `meta/03_REFLECTIONS.md` – gondolati napló, tanulságok

---

## 2. Dokumentációs fázis – Megértés és feltérképezés

**Cél:**  
A már létező, működő rendszer elemeinek dokumentálása, hogy érthető, auditálható és később újraépíthető legyen.

**Kulcsmodul:**
- `modules/data_pipeline/00_summary.md`
- `docs/data_flow.md` – adatfeldolgozás lépései
- `core_database` struktúrájának dokumentálása
- Jelenlegi architektúra-függések feltárása

---

## 3. Stabilizációs fázis – Keretrendszer újraépítése

**Cél:**  
Létrehozni azt a minimális, de vállalati szinten működő alapot,  
amelyre a későbbi funkciók épülhetnek.

**Elemei:**
- Új adatbázis-séma és inicializáló modul
- API váz (Flask alapok, struktúrák)
- Docker-compose környezet
- Logging, monitoring vázlat

---

## 4. Funkcionális bővítés – Új komponensek

**Cél:**  
A rendszer funkcióinak kibővítése – először belső, majd felhasználói modulokkal.

**Komponensek:**
- `user_auth` modul (JWT, jogosultság, audit trail)
- API endpoints: adatlekérés, meta-információk
- Frontend skeleton (admin UI, ügyfél UI)
- Kulcskezelés, API token rendszer

---

## 5. Biztonsági fázis – Infrastruktúra és kontroll

**Cél:**  
Olyan üzemeltetési réteg hozzáadása, amely biztonságos, fenntartható és auditálható működést garantál.

**Elemei:**
- WireGuard alapú belső kommunikáció
- UFW, fail2ban, reverse proxy
- Naplózás, kulcskezelés, szerveridentitás
- Scriptek auditálása (pl. crontab, rsync, log pipeline)

---

## 6. Dokumentációs kiteljesítés – Termékesítésre kész forma

**Cél:**  
A projekt olyan állapotba hozása, hogy újra deployolható, tanítható, vagy akár eladható legyen.

**Output:**
- Teljes `docs/` mappa
- `INSTALL.md`, `USER_GUIDE.md`, `DEPLOY_GUIDE.md`
- `Softwired Development Handbook` (fejlesztési kultúra és workflow)

---

## 7. Reflektív lezárás vagy továbblépés

**Cél:**  
Összegyűjteni, mit tanultam, mit hagytam ki, mit csinálnék másképp –  
és eldönteni, hogy:

- publikálom-e tananyagként,
- integrálom-e más projektekbe,
- továbbfejlesztem-e SaaS irányba,
- vagy újrakezdem – immár még egy szinttel feljebb.

---

## Megjegyzés

Ez a roadmap **nem végleges**.  
A projekt *organikus struktúra*, és bármikor reagálhat belső vagy külső változásokra.

A cél:  
**ne csak legyen egy termékem –  
hanem tudjam, hogyan építettem meg.**

