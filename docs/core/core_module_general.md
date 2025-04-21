# Modul neve: Backend API

## Funkció

A Backend API a rendszer központi kiszolgáló rétege. REST végpontokat biztosít a frontend felület és más modulok számára, valamint kezeli (majd) a felhasználói regisztrációt, PDF generálást, számítási logikát és külső API kapcsolódásokat (pl. Google API).

## Technológiák

- Python 3.x
- Flask (WSGI entry point: `wsgi.py`)
- Docker & Docker Compose
- MariaDB (külön inicializáló és séma betöltő scriptekkel)
- HTML/CSS/JS frontend beépítve (statikus fájlokon keresztül)

## Belső felépítés

```
flask_app/
├── Dockerfile                # Backend konténer definíció
├── requirements.txt          # Python függőségek
├── wsgi.py                   # WSGI entry point
├── app/
│   ├── __init__.py           # Flask app inicializálás
│   ├── main.py               # Fő konfiguráció / run logic
│   ├── routes/
│   │   ├── __init__.py
│   │   ├── calculations_api.py  # Számítási végpontok
│   │   ├── google_api.py        # Google API kapcsolódás
│   │   ├── pdf_api.py           # PDF generálás
│   │   └── registration_api.py  # Regisztrációs logika
│   └── static/
│       ├── index.html
│       ├── styles.css
│       ├── script.js
│       └── pdf.js
```

Adatbázis inicializálás:

```
db/
├── init/
│   ├── core.user.generator.sh   # DB user létrehozása
│   └── db.user.sync.sh          # DB user szinkronizáció
├── schema/
│   ├── db.sync.sql              # teljes adatbázis szinkronizálás
│   └── schema_loader.sql        # sémák betöltése
```

Docker Compose:

```
compose/
└── docker-compose.core.yml
```

## Kapcsolódási pontok

| Kapcsolódó modul   | Kapcsolat típusa | Leírás |
|--------------------|------------------|--------|
| `frontend`          | statikus fájl    | `index.html` kiszolgálása |
| `db`                | SQL kapcsolat    | saját user + séma betöltés |
| `utils/smtp`        | SMTP hívások     | opcionális regisztrációs visszaigazolás |
| `villamcsapas/query-logic` | HTTP API | ha igénybe veszi a backend egyik szolgáltatását |
| `config-manager`    | Docker env       | beállítások konténer szinten |

## Használat

Indítás Docker Compose segítségével:
```bash
cd compose
docker-compose -f docker-compose.core.yml up --build
```

A szolgáltatás elérhető:
- `http://localhost:5000/` – statikus frontend
- `http://localhost:5000/api/registration`
- `http://localhost:5000/api/pdf`
- `http://localhost:5000/api/calculations`
- `http://localhost:5000/api/google`

## Tesztelés

Jelenleg manuális tesztelés támogatott:
- API endpointok tesztelése pl. Postman vagy curl segítségével
- Statikus UI betöltés böngészőben
- MariaDB inicializálás külön scriptekkel (`db/init/*.sh`)

Tervek között szerepel egységtesztek hozzáadása `pytest`-tel.

## Tervezett bővítések

- API autentikáció (JWT vagy session)
- Logging és audit trail
- API dokumentáció (Swagger vagy ReDoc)
- CI/CD pipeline integráció
