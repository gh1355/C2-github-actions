# 🌦 WeatherWise – Web Wetter App

Eine moderne, responsive Wetter-Web-Applikation als Single Page Application (SPA), erweitert zu einer Multi-Service-Architektur mit Docker Compose.

---

## 📌 Projektbeschreibung

Mit WeatherWise können Benutzer aktuelle Wetterdaten und Vorhersagen für beliebige Städte weltweit abrufen.
Die Anwendung wurde zusätzlich im Rahmen des Deployment-Moduls um eine containerisierte Multi-Service-Architektur erweitert.

---

## 🎯 Ziel der Anwendung

Die Anwendung dient dazu, Wetterdaten effizient bereitzustellen.
Durch den Einsatz eines Caching-Mechanismus mit Redis werden externe API-Aufrufe reduziert, was die Performance verbessert und die Systemlast verringert.

Die Multi-Service-Architektur ermöglicht eine klare Trennung der Verantwortlichkeiten zwischen Frontend, Backend und Datenhaltung.

Ziel ist es, moderne Deployment-Praktiken umzusetzen:

* Containerisierung mit Docker
* Orchestrierung mit Docker Compose
* Service-Kommunikation
* Caching mit Redis
* Produktionsnahes Setup

---

## 👥 Gruppenmitglieder

| Name                 | Rolle             |
| -------------------- | ----------------- |
| Oguzhan Saydam       | Frontend & Design |
| Gholamreza Aghakhani | API & Deployment  |
| Mehmet Ali Gür       | Routing & Testing |

---

## 🏗 Architektur

Die Anwendung besteht aus drei Services:

| Service      | Beschreibung                                 |
| ------------ | -------------------------------------------- |
| **frontend** | React-App, ausgeliefert über Nginx           |
| **backend**  | Node.js API zur Verarbeitung von Wetterdaten |
| **cache**    | Redis zur Zwischenspeicherung (Caching)      |

---

## 🔗 Datenfluss

```
User → Frontend (Nginx)
        ↓
     Backend API
        ↓
     Redis Cache
        ↓
 External Weather API
```

---

## ⚙️ Setup Anleitung

### Voraussetzungen

* Docker installiert
* Docker Compose verfügbar

### Anwendung starten

```bash
docker compose up --build
```

### Anwendung stoppen

```bash
docker compose down
```

### Logs anzeigen

```bash
docker compose logs
```

---

## 🌐 Zugriff

Die Anwendung ist erreichbar unter:

http://localhost:3000

---

## 🧪 API Beispiel

```bash
curl http://localhost:3000/api/weather?city=Zurich
```

---

## 💡 Hauptfeatures

### Frontend

* Stadtsuche weltweit
* Geolokalisierung
* 5-Tage-Vorhersage
* Stündliche Prognose
* Favoriten (LocalStorage)
* Responsive Design

### Backend

* API-Endpunkt `/api/weather`
* Integration externer Wetter-API
* Fehlerbehandlung

### Deployment

* Multi-Service-Architektur
* Redis Caching zur Performance-Optimierung
* Healthchecks für Services
* Restart-Policies für Stabilität
* Custom Docker Netzwerke

---

## 💾 Persistenz

Redis verwendet ein Named Volume:

redis-data

Dies stellt sicher, dass Daten Container-Neustarts überleben.

---

## ❤️ Health Checks

| Service | Prüfung            |
| ------- | ------------------ |
| Backend | `/health` Endpoint |
| Redis   | `redis-cli ping`   |

---

## 🔁 Restart-Verhalten

Alle Services nutzen:

restart: unless-stopped

Das bedeutet:

* Automatischer Neustart bei Fehlern
* Hohe Verfügbarkeit der Anwendung

---

## 📊 Logging

Das Backend verwendet strukturierte Logs:

{
"timestamp": "...",
"level": "info",
"message": "Weather served from cache"
}

Logs können eingesehen werden mit:

docker compose logs

---

## 🔐 Umgebungsvariablen

Definiert in `.env.example`:

REDIS_URL=redis://cache:6379
CACHE_TTL_SECONDS=300
PORT=3000

---

## 🔧 Wichtige Konfigurationen

### docker-compose.yml

* Definiert alle Services
* Nutzt Healthchecks und depends_on
* Verwendet separate Netzwerke

### Backend (server.js)

* Stellt `/api/weather` bereit
* Nutzt Redis als Cache
* Reduziert externe API-Aufrufe

### nginx.conf

* Leitet `/api` Anfragen an das Backend weiter
* Liefert Frontend-Dateien aus

---

## 🧠 Architektur-Entscheidungen

* Redis für schnelles Caching gewählt
* Nginx als stabiler Webserver
* Docker Compose für einfache Orchestrierung
* Multi-Stage Builds für kleinere Images

---

## 🧠 Reflexion

Während der Umsetzung habe ich gelernt:

* Aufbau von Multi-Service-Architekturen
* Nutzung von Docker Compose
* Service-Kommunikation zwischen Containern
* Performance-Optimierung durch Caching
* Debugging containerisierter Anwendungen

Rückblickend würde ich:

* Eine Datenbank (z.B. PostgreSQL) hinzufügen
* Eine CI/CD Pipeline integrieren
* Deployment in die Cloud durchführen

---

## 📂 Projektstruktur

backend/
src/
public/
docker-compose.yml
Dockerfile

---

## 📜 Lizenz

Dieses Projekt wurde im Rahmen des Moduls WEB2 / DEP an der GIBB Bern erstellt.
