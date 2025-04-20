# Meteologix – Komponens-térkép

Ez a dokumentum a teljes rendszer komponens-szintű térképe.  
Célja, hogy átláthatóvá tegye, milyen fő egységekből áll a Meteologix, ezek milyen célt szolgálnak, milyen állapotban vannak, és hogyan kapcsolódnak egymáshoz.

---

## Komponenslista

### `data_pipeline`
**Szerepe:**  
Külső adatok letöltése, feldolgozása, szétválasztása és adatbázisba betöltése.

**Státusz:**  
Működő, rendkívül érzékeny rendszer, több scriptből áll. Most dokumentálás és reflexió alatt.  
Újraépítés *csak megfelelő körültekintéssel* és előzetes teljes feltérképezéssel lehetséges.

**Kapcsolódás:**  
- `core_database` (output)
- `api_core` (indirekt kiszolgálás)

---

### `core_database`
**Szerepe:**  
Adatbázis sémák definiálása: konstans és dinamikus meteorológiai adatok, user adatmodell, jogosultságok, API kulcsok.

**Státusz:**  
Részben létező, történetileg kialakult struktúra. Újrafeltérképezés és dokumentálás alatt.

**Kapcsolódás:**  
- `data_pipeline` (input)
- `api_core`, `user_auth` (lekérdezés)

---

### `api_core`
**Szerepe:**  
Központi REST API kiszolgáló, amely strukturált hozzáférést biztosít az adatokhoz.

**Státusz:**  
Alap backend működik. Most indul az újraépítés, dokumentált, moduláris formában.

**Kapcsolódás:**  
- `core_database`
- `user_auth`
- `frontend`

---

### `user_auth`
**Szerepe:**  
Felhasználókezelés, jogosultság, auditálás, session kontroll, API védelem (JWT, kulcs, szerepkör).

**Státusz:**  
Még nem létezik. Teljesen új, nulláról épülő modul – a jövő egyik kulcsfejlesztése.

**Kapcsolódás:**  
- `api_core`
- `core_database`
- `frontend`

---

### `frontend`
**Szerepe:**  
Felhasználói felület (operátori és ügyfél oldalon), lekérdezésvezérlés, eredmények megjelenítése.

**Státusz:**  
Létező frontend működik, de újraépítésre szorul (kompatibilitás, UX, strukturáltság).

**Kapcsolódás:**  
- `api_core`
- `user_auth`

---

### `infrastructure`
**Szerepe:**  
Rendszerszintű háttér: Docker-compose, VPN, tűzfal, naplózás, jogosultságkezelés, deployment.

**Státusz:**  
Saját használatra működő környezet. Most kerül strukturált formába: újraépítés, dokumentálás, újraintegrálás.

**Kapcsolódás:**  
- **Minden komponenshez**

---

### `meta`
**Szerepe:**  
Dokumentációk, döntésnaplók, filozófia, komponens térképek, roadmap – a projekt tudati tere.

**Státusz:**  
Aktív. Innen indul a gondolkodás, itt formálódik a fejlesztési kultúra.

**Kapcsolódás:**  
- Összes többi modulhoz – mint gondolati és stratégiai háttér

---

## Kapcsolódási mátrix

| Komponens     | Függ tőle →             | Használja →             |
|---------------|--------------------------|--------------------------|
| `data_pipeline` | –                        | `core_database`          |
| `core_database` | `data_pipeline`          | `api_core`, `user_auth`  |
| `api_core`      | `core_database`, `user_auth` | `frontend`           |
| `user_auth`     | `core_database`          | `api_core`, `frontend`   |
| `frontend`      | `api_core`, `user_auth`  | –                        |
| `infrastructure`| –                        | **minden modul**         |
| `meta`          | –                        | **minden modul**         |

---

## Következő lépés

- [ ] Minden modul kapjon saját `00_summary.md` fájlt
- [ ] Roadmap készítés a komponensek alapján
- [ ] Kapcsolódási pontok részletes dokumentálása

