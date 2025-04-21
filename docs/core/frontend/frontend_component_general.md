# Komponens: Frontend

**Modul:** core

## Funkció

A Frontend komponens biztosítja a rendszer felhasználói felületét. Ez egy statikus webes felület, amelyet a backend szolgál ki, és amely AJAX-on keresztül hívja az API végpontokat. Alkalmas alapvető vizualizációra, adatbeküldésre és egyszerű adminisztrációs funkciókra.

## Technológiák

- HTML5, CSS3, JavaScript
- Statikus fájlkiszolgálás Flask backendből
- (opcionálisan) Leaflet.js vagy MapLibre a térképes megjelenítéshez

## Belső felépítés

```
flask_app/app/static/
├── index.html        # Fő belépési pont
├── styles.css        # Alapstílusok
├── script.js         # Interakciók, API hívások
└── pdf.js            # PDF fájlok megjelenítése
```

## Kapcsolódási pontok

| Modul / Komponens         | Kapcsolat típusa    | Leírás |
|---------------------------|---------------------|--------|
| `core/backend`            | statikus kiszolgálás | HTML/JS/CSS fájlokat szolgál ki |
| `core/backend`            | AJAX API hívások     | adatlekérdezés és -küldés |
| `user-auth/auth-api`      | opcionális auth      | bejelentkezés, jogosultság |
| `utils/config-manager`    | közvetett            | API URL konfigurálása környezeti változóból (pl. `API_URL`) |

## Használat

A frontend nem külön konténer, hanem a backend szolgálja ki a `static/` mappából. Böngészőből egyszerűen elérhető:

```
http://localhost:5000/
```

A `script.js` JavaScript kód a `core/backend` által nyújtott API-kat használja (pl. `GET /api/lightning` vagy `POST /api/registration`).

## Tesztelés

- Böngészős ellenőrzés (Chrome/Firefox)
- DevTools használata (AJAX hívások, konzol)
- HTML, CSS, JS statikus validálás (pl. W3C)

## Tervezett bővítések

- Egységesített UI/UX dizájn (Bootstrap vagy Tailwind)
- Térképes komponens (Leaflet vagy MapLibre)
- Reaktív architektúra (Vue vagy Vite alapú frontend különválasztva)
