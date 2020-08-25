---
title: API
---

Die API wird vom Server unter dem Pfad `/api/v1/` bereitgestellt.
Wenn der Server der Alarmanzeige unter der IP-Adresse _192.168.1.5_ auf Port 4711 läuft, ist die API unter `http://192.168.1.5:4711/api/v1/` erreichbar.

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
Es kann auch ein statischer API-Key verwendet werden, z. B. zur Verwendung in Mikrocontrollern.
Der Key muss im HTTP-Header `x-api-key` übermittelt werden.

Erzeugt werden API-Keys in der Console unter Administration > API-Keys.
Ein API-Key wird nach dem Anlegen nur einmalig angezeigt und muss sofort notiert werden.
Diese Keys sind bis auf Widerruf gültig.
