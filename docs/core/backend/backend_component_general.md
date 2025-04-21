# Komponens: Backend

**Modul:** core

## Funkció

A Backend komponens a rendszer központi adatkapcsolati rétege. REST végpontokat biztosít más komponensek és kliensek (frontend, lekérdező logikák, admin interfészek) számára. Feladata a villámcsapás-adatok, regisztrációk, PDF generálás és külső API kapcsolatok kiszolgálása.

## Technológiák

- Python 3.x
- Flask (WSGI belépési pont: `wsgi.py`)
- Docker & Docker Compose
- MariaDB (DB kapcsolat, környezeti változókon keresztül)
- HTML/CSS/JS statikus kiszolgálás frontendhez

## Belső felépítés

```
flask_app/
├── Dockerfile
├── requirements.txt
├── wsgi.py
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── routes/
│   │   ├── __init__.py
│   │   ├── calculations_api.py
│   │   ├── google_api.py
│   │   ├── pdf_api.py
│   │   └── registration_api.py
│   └── static/
│       ├── index.html
│       ├── styles.css
│       ├── script.js
│       └── pdf.js
```

## Kapcsolódási pontok

| Modul / Komponens         | Kapcsolat típusa | Leírás |
|---------------------------|------------------|--------|
| `core/db`                 | MariaDB kapcsolat | `DB_HOST`, `DB_NAME`, `DB_USER`, `DB_PASSWORD_FILE` |
| `core/frontend`           | statikus kiszolgálás | HTML/JS/CSS |
| `user-auth/auth-api`      | opcionális integráció | token ellenőrzés (később) |
| `utils/smtp`              | opcionális SMTP | pl. regisztráció visszaigazolás |
| `villamcsapas/query-logic`| HTTP API | lekérdezésekhez REST hívások |
| `utils/config-manager`    | közvetett | konténer szintű konfig betöltés |

## Használat

Indítás:

```bash
cd compose
docker-compose -f docker-compose.core.yml up --build
```

Elérhetőség:

- `http://localhost:5000/` – statikus UI
- `http://localhost:5000/api/registration`
- `http://localhost:5000/api/pdf`
- `http://localhost:5000/api/calculations`
- `http://localhost:5000/api/google`

Környezeti változók (Docker Compose definiálja):
- `DB_HOST`, `DB_NAME`, `DB_USER`, `DB_PASSWORD_FILE`
- `GOOGLE_API_KEY_FILE`, `GOOGLE_MAP_ID_FILE`

## Tesztelés

- Jelenleg manuális tesztelés ajánlott (Postman, curl, böngésző)
- Tervek: `pytest` + mockolt adatbázis, CI bevezetése

## Tervezett bővítések

- JWT alapú autentikáció
- Swagger vagy ReDoc dokumentáció
- Role-alapú jogosultság (RBAC)
- CI/CD integráció
