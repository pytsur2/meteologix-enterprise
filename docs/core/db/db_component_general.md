# Komponens neve: Adatbázis (MariaDB)

**Modul:** core

## Funkció

Ez a modul felelős az adatbázis inicializálásáért, a felhasználói jogosultságok beállításáért, valamint az adattáblák és sémák betöltéséért.

A rendszer MariaDB-t használ, és Docker Compose-on keresztül futtatott konténerben érhető el. A jelszavak és titkos adatok Docker secrets segítségével kerülnek átadásra.

## Technológiák

- MariaDB 10.11
- Bash scriptek SQL parancsokkal
- Docker secrets (`/run/secrets/...`)
- SQL migráció fájlokon keresztül

## Belső felépítés

```
db/
├── init/
│   ├── core.user.generator.sh   # új adatbázis felhasználó létrehozása
│   └── db.user.sync.sh          # meglévő user jogosultságainak frissítése
├── schema/
│   ├── db.sync.sql              # teljes séma újraépítése
│   └── schema_loader.sql        # gyors séma betöltés fejlesztéshez
```

## Kapcsolódási pontok

| Kapcsolódó komponens   | Kapcsolat típusa | Leírás |
|--------------------|------------------|--------|
| `backend`          | DB kapcsolat     | DB_HOST, DB_USER, DB_NAME környezeti változók |
| `compose`          | konténer definiálás | `docker-compose.core.yml` definiálja az image-t, volume-okat és secrets |
| `utils/config-manager` | közvetett      | azonosítás és szinkron titkos fájlok alapján |

## Használat

A `docker-compose.core.yml` fájl indítja el az adatbázis konténert automatikusan. A scriptek kézzel is futtathatók:

```bash
# MariaDB root user létrehozása
bash db/init/core.user.generator.sh

# Felhasználói jelszavak és jogosultságok frissítése
bash db/init/db.user.sync.sh

# Teljes séma újratöltése
mysql -u root -p < db/schema/db.sync.sql
```

A scriptek feltételezik, hogy a jelszavak a `/run/secrets/` mappában találhatók (Docker environment).

## Tervezett bővítések

- Automatikus séma verifikáció (`mariadb --dry-run`)
- Inkrementális sémafrissítések verziószámozott SQL fájlokkal
- Egységes migrációs framework integráció (Flyway, Liquibase, stb.)
