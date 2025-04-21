# Komponens: Frontend

**Modul:** villamcsapas

## Funkció

Ez a komponens biztosítja a villamcsapas.hu nyilvános, térképes felhasználói felületét.  
A célja, hogy vizuálisan jelenítse meg az aktuális és múltbeli villámcsapás-adatokat, egyszerűen, gyorsan és közérthetően.

Statikus weboldalként működik, amely JavaScripten keresztül hívja a rendszer backend API-ját vagy a lekérdezésből generált statikus JSON fájlokat.

---

## Technológiák

- HTML, CSS, JavaScript (Vanilla vagy később Vite/TS)
- Leaflet.js vagy MapLibre (térképi megjelenítés)
- JSON alapú adatbeolvasás
- Opcionálisan: Alpine.js, Tailwind (dizájn és dinamika)

---

## Funkcionális felépítés

```
villamcsapas/frontend/
├── index.html            # fő belépési oldal
├── style.css             # megjelenés
├── main.js               # térképes logika, fetch JSON adatok
└── assets/               # ikonok, statikus fájlok
```

---

## Kapcsolódási pontok

| Modul / Komponens       | Kapcsolat típusa | Leírás |
|-------------------------|------------------|--------|
| `villamcsapas/json-data`| fájlalapú fetch  | JSON fájlok betöltése térképi rétegként |
| `core/backend`          | HTTP API         | villámadatok lekérdezése (alternatíva JSON helyett) |
| `utils/config-manager`  | konfiguráció     | API_URL vagy JSON_PATH megadása környezeti változóként |

---

## Használat

A frontend bármely webszerverrel kiszolgálható:

```bash
# statikus kiszolgálás lokálisan
python3 -m http.server 8080
```

Vagy reverse proxy mögött (NGINX):

```
server {
    server_name villamcsapas.hu;
    root /var/www/villamcsapas/frontend;
    index index.html;
}
```

---

## Tervezett bővítések

- Térképréteg váltás (pl. hőtérkép, cluster)
- Helyalapú értesítés UI
- Reszponzív dizájn mobilra
- Marker animációk (villanás-effektus)
