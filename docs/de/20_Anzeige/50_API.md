---
title: API
---

Die API wird vom Server unter dem Pfad `/api/v1/` bereitgestellt.
Wenn der Server der Anzeige unter der IP-Adresse _192.168.1.5_ auf Port 4711 läuft, ist die API unter `http://192.168.1.5:4711/api/v1/` erreichbar.
Eine Liste der Endpunkte folgt weiter unten.

## Authentifikation
Alle Endpunkte – mit ganz vereinzelten Ausnahmen – sind nur mit Authentifikation benutzbar.
Dies kann über zwei verschiedene Verfahren erfolgen:

### JWT
Mit einem `POST`-Request gegen den Endpunkt `/authentication` kann ein [JWT](https://jwt.io/) erworben werden.
Der Request muss folgendes Format haben:
```json
{
  "strategy": "local",
  "email": "test@example.org",
  "password": "super-secret"
}
```
Die Antwort enthält ein `accessToken`, das bei künftigen Requests im HTTP-Header `Authorization` als `Bearer`-Token verwendet werden kann.
Das Token ist ab Erhalt für 24 Stunden gültig.

### API-Key
Es kann auch ein statischer API-Key verwendet werden, z. B. zur Verwendung in Mikrocontrollern oder eigenen Skripten.
Der Key muss im HTTP-Header `x-api-key` übermittelt werden.

Erzeugt werden API-Keys in der Console unter Administration > API-Keys.
Ein API-Key wird nach dem Anlegen nur einmalig angezeigt und muss sofort notiert werden.
Diese Keys sind bis auf Widerruf gültig.

## Endpunkte
Es folgt eine Auflistung der verschiedenen Ressourcen, die über die API verwaltet werden können.
Mittelfristig soll diese Liste durch eine _Open API Specification_ abgelöst werden.

### `/authentication`
Abruf eines JWT

### `/api/v1/announcements`
Die Ankündigungen

### `/api/v1/api-keys`
API-Keys

### `/api/v1/calendar-feeds`
Die abonnierten Kalender-Feeds

### `/api/v1/calendar-items`
Kalendereinträge aus den Feeds (read-only)

### `/api/v1/content-slot-options`
Optionen für einzelne Content Slots

### `/api/v1/content-slots`
Die Content Slots von Ansichten

### `/api/v1/displays`
Die Displays

### `/api/v1/incidents`
Die Einsätze

### `/api/v1/key-requests`
Anfragen von Displays nach API-Keys

### `/api/v1/locations`
Örtlichkeiten von Einsätzen

### `/api/v1/settings`
Allgemeine Einstellungen

### `/api/v1/users`
Die Benutzer

### `/api/v1/views`
Ansichten der Displays
